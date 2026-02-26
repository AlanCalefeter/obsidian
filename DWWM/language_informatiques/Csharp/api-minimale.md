[# Tutoriel : Créer une API minimale avec ASP.NET Core](https://learn.microsoft.com/fr-fr/aspnet/core/tutorials/min-web-api?view=aspnetcore-10.0&tabs=visual-studio)
[Explorateur de points de terminaison](https://learn.microsoft.com/fr-fr/aspnet/core/test/http-files?view=aspnetcore-10.0#use-endpoints-explorer)

*Nom* : TodoApi
*Techno* : ASP.NET CORE + C#
*Objectif* :

| API                       | Description                            | Corps de la requête                | Corps de réponse             |
| ------------------------- | -------------------------------------- | ---------------------------------- | ---------------------------- |
| `GET /todoitems`          | Obtenir toutes les tâches              | None                               | Tableau de tâches            |
| `GET /todoitems/complete` | Obtenir les tâches terminées           | None                               | Tableau de tâches            |
| `GET /todoitems/{id}`     | Obtenir un élément par ID              | None                               | Élément de tâche à effectuer |
| `POST /todoitems`         | Ajouter un nouvel élément              | Élément de tâche à effectuer       | Élément de tâche à effectuer |
| `PUT /todoitems/{id}`     | Mettre à jour un élément existant      | Élément de tâche à effectuer       | None                         |
| `PATCH /todoitems/{id}`   | Mettre à jour partiellement un élément | Élément de liste de tâches partiel | None                         |
| `DELETE /todoitems/{id}`  | Supprimer un élément                   | None                               | None                         |

# Créer un projet d’API

- choisir ASP.NET Core vide
- Nommez le projet *TodoApi*
- Dans la boîte de dialogue **Informations supplémentaires** :
	- Sélectionnez **.NET 9.0**
	- Décochez la case **Ne pas utiliser d’instructions de niveau supérieur**
	- Sélectionnez **Créer**

# Exécuter l'application

- CRTL + F5
- Accepter les deux certificats

## Ajouter des packages NuGet

- Les packages NuGet doivent être ajoutés pour prendre en charge la base de données et les diagnostics utilisés dans ce tutoriel : 
	- Outils -> Gestionnaire de package NuGet > Gérer les packages NuGet pour la solution.
	- Parcourir -> cocher "Inclure la version préliminaire"
	- Entrez Microsoft.EntityFrameworkCore.InMemory dans la zone de recherche, puis sélectionnez `Microsoft.EntityFrameworkCore.InMemory`.
	- Cochez la case **Projet** dans le volet droit, puis sélectionnez **Installer**

- Faire pareil pour `Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore`.

## Création du modèle Todo

- Dans le dossier du projet, créer un fichier nommé `Todo.cs`  :
```cs
public class Todo
{
    public int Id { get; set; }
    public string? Name { get; set; }
    public bool IsComplete { get; set; }
}
```
- Un _modèle_ est un ensemble de classes qui représentent les données gérées par l’application. coucou

## Création de base de données

- Dans le dossier du projet, créer `TodoDb.cs` :
```cs
using Microsoft.EntityFrameworkCore;

class TodoDb : DbContext
{
    public TodoDb(DbContextOptions<TodoDb> options)
        : base(options) { }
        
    public DbSet<Todo> Todos => Set<Todo>();
}
```
- Le précédent code définit le _contexte de base de données_, qui est la classe principale qui coordonne les fonctionnalités d’[Entity Framework](https://learn.microsoft.com/fr-fr/ef/core/) pour un modèle de données. Cette classe dérive de la classe [Microsoft.EntityFrameworkCore.DbContext](https://learn.microsoft.com/fr-fr/dotnet/api/microsoft.entityframeworkcore.dbcontext).

## Ajouter le code de l’API

- Remplacez le contenu du fichier `Program.cs` par le code suivant :

```cs
using Microsoft.EntityFrameworkCore;

var builder = WebApplication.CreateBuilder(args);
builder.Services.AddDbContext<TodoDb>(opt => opt.UseInMemoryDatabase("TodoList"));
builder.Services.AddDatabaseDeveloperPageExceptionFilter();
var app = builder.Build();

app.MapGet("/todoitems", async (TodoDb db) =>
    await db.Todos.ToListAsync());

app.MapGet("/todoitems/complete", async (TodoDb db) =>
    await db.Todos.Where(t => t.IsComplete).ToListAsync());

app.MapGet("/todoitems/{id}", async (int id, TodoDb db) =>
    await db.Todos.FindAsync(id)
        is Todo todo
            ? Results.Ok(todo)
            : Results.NotFound());

app.MapPost("/todoitems", async (Todo todo, TodoDb db) =>
{
    db.Todos.Add(todo);
    await db.SaveChangesAsync();

    return Results.Created($"/todoitems/{todo.Id}", todo);
});

app.MapPut("/todoitems/{id}", async (int id, Todo inputTodo, TodoDb db) =>
{
    var todo = await db.Todos.FindAsync(id);

    if (todo is null) return Results.NotFound();

    todo.Name = inputTodo.Name;
    todo.IsComplete = inputTodo.IsComplete;

    await db.SaveChangesAsync();

    return Results.NoContent();
});

app.MapDelete("/todoitems/{id}", async (int id, TodoDb db) =>
{
    if (await db.Todos.FindAsync(id) is Todo todo)
    {
        db.Todos.Remove(todo);
        await db.SaveChangesAsync();
        return Results.NoContent();
    }

    return Results.NotFound();
});

app.Run();
```

- Le var builder ajoute le contexte de base de données au conteneur [d’injection de dépendances (DI)](https://learn.microsoft.com/fr-fr/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-10.0) et active l’affichage d’exceptions liées à la base de données.

- Le conteneur d’injection de dépendances donne accès au contexte de base de données et à d’autres services.

- aller dans Affichage -> autres fenêtres -> Explorateur de points de terminaison
	-  Si un fichier `.http` portant le nom du projet en tant que nom de fichier existe, la requête est ajoutée à ce fichier.
	- Sinon, un fichier `.http` est créé avec le nom du projet comme nom de fichier et la requête est ajoutée à ce fichier.

## Tester les données de validations 

- Le app.MapPost dans `Program.cs`, crée un point de terminaison HTTP POST `/todoitems` qui ajoute des données à la base de données en mémoire.

- Exécutez l'application. Le navigateur affiche une erreur 404, car il n’y a plus de point de terminaison `/`.
- Le point de terminaison POST sera utilisé pour ajouter des données à l’application.

- click-droit sur POST -> Generate Request
- ça crée le fichier `TodoApi.http` comme ceci : 
```cs
  @TodoApi_HostAddress = https://localhost:7031

POST {{TodoApi_HostAddress}}/todoitems

###
```
- La première ligne crée une variable qui est utilisée pour tous les points de terminaison.
- La ligne suivante définit une requête POST.
- La ligne de triple hashtag (`###`) est un délimiteur de requête : ce qui suit est pour une autre requête.

- La requête POST a besoin d’en-têtes et d’un corps. Pour définir ces parties de la requête, ajoutez les lignes suivantes immédiatement après la ligne de requête POST :
```cs
Content-Type: application/json
{
  "name":"walk dog",
  "isComplete":true
}
```
- Le code précédent ajoute un en-tête Content-Type et un corps de la demande JSON.
- Exécutez l'application.
- Sélectionnez le lien **Envoyer une demande** au-dessus de la `POST` ligne de requête.
- La requête POST est envoyée à l’application et la réponse s’affiche dans le volet **Réponse**.
- 



