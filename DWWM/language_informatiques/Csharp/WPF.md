# Introduction [WPF](vocabulaire-formation) 
Elle permet de créer des **applications desktop modernes** avec :
- Interfaces riches (animations, styles, thèmes)
- Gestion avancée des graphiques 2D/3D
- Liaison de données (data binding)
- Séparation claire entre interface et logique (MVVM)

# À quoi ça sert ?

WPF sert à développer :
- Applications professionnelles (gestion, outils internes)
- Logiciels métiers
- Interfaces complexes sous Windows

Exemples d’environnements :
- Développement avec **C#**
- Projet créé via Visual Studio
- Fichier projet : `.csproj`

## Comment ça fonctionne ?
WPF utilise :
### 1. XAML

Un langage XML pour décrire l’interface :

<Button Content="Clique moi" Width="100"/>

### 2. 'C#'

Pour gérer la logique :

```cs
private void Button_Click(object sender, RoutedEventArgs e)  
{  
    MessageBox.Show("Bonjour");  
}
```

---
## WPF vs autres technologies

| Technologie | Plateforme         | Type                  |
| ----------- | ------------------ | --------------------- |
| WPF         | Windows uniquement | Desktop               |
| WinForms    | Windows            | Desktop (plus ancien) |
| ASP.NET     | Web                | Site web              |
| MAUI        | Multi-plateforme   | Mobile + Desktop      |