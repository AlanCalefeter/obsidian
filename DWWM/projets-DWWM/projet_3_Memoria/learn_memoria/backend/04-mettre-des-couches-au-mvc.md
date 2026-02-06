# 📚 Exercice : Refactoring Architecture MVC vers Architecture en Couches

## 🎯 Objectif

Refactoriser l'application **Memoria** pour séparer clairement les responsabilités :

- **Validators** : Validation des données entrantes (Zod)
- **Entities** : Représentation 1:1 des tables SQL
- **Repositories** : Requêtes SQL pures
- **Services** : Logique métier
- **DTOs** : Formatage pour les vues
- **Controllers** : Orchestration HTTP

_🫣 Attention ! Le code que je vous fourni en exemple n'est pas forcement votre ami... C'est une histoire de validation..._
— _Doki Doc_

---

## 📊 Schéma de l'Architecture Cible

```
┌─────────────────────────────────────────────────────────────────┐
│                         FLUX DE DONNÉES                          │
└─────────────────────────────────────────────────────────────────┘

   HTTP Request (POST /items)
         │
         ▼
┌──────────────────────┐
│   1. VALIDATOR       │ ◄── validators/itemValidator.js
│   (Zod Schema)       │     ✓ Valide les données entrantes
└──────────────────────┘     ✓ Retourne erreurs si invalide
         │
         ▼
┌──────────────────────┐
│   2. CONTROLLER      │ ◄── controllers/ItemController.js
│   (Orchestration)    │     ✓ Gère req/res HTTP
└──────────────────────┘     ✓ Appelle le Service
         │
         ▼
┌──────────────────────┐
│   3. SERVICE         │ ◄── services/ItemService.js
│   (Logique Métier)   │     ✓ Règles métier
└──────────────────────┘     ✓ Appelle le Repository
         │
         ▼
┌──────────────────────┐
│   4. REPOSITORY      │ ◄── repositories/ItemRepository.js
│   (Requêtes SQL)     │     ✓ Requêtes PostgreSQL
└──────────────────────┘     ✓ Retourne Entity
         │
         ▼
┌──────────────────────┐
│   PostgreSQL         │
│   (Table items)      │
└──────────────────────┘
         │
         ▼
┌──────────────────────┐
│   5. ENTITY          │ ◄── entities/ItemEntity.js
│   (Données brutes)   │     ✓ Représentation 1:1 table
└──────────────────────┘     ✓ TOUS les champs
         │
         ▼
┌──────────────────────┐
│   6. DTO             │ ◄── dto/ItemDTO.js
│   (Vue Frontend)     │     ✓ Formatage pour EJS
└──────────────────────┘     ✓ Champs sélectionnés
         │
         ▼
   HTTP Response (HTML/JSON)
```

---

## 🔧 Étapes du Refactoring

### 📝 Étape 1 : Créer les Validators (Zod)

**Fichier à créer :** `src/validators/itemValidator.js`

**Consigne :**
Créez les schémas de validation Zod pour :

- ✅ Création d'un item (`createItemSchema`)
- ✅ Mise à jour d'un item (`updateItemSchema`)

**Règles de validation :**

| Champ        | Type   | Règles                                          |
| ------------ | ------ | ----------------------------------------------- |
| `type`       | enum   | ['book', 'podcast', 'article', 'video', 'note'] |
| `title`      | string | Min 3, Max 255 caractères                       |
| `content`    | string | Optionnel, Max 10000 caractères                 |
| `author`     | string | Optionnel, Max 255 caractères                   |
| `source_url` | string | Optionnel, URL valide                           |
| `image_url`  | string | Optionnel, URL valide                           |

**Code de départ :**

```javascript
import { z } from 'zod';

export const createItemSchema = z.object({
  // TODO: Compléter les règles de validation
  type: z.enum(['book', 'podcast', 'article', 'video', 'note'], {
    required_error: "Le type est obligatoire"
  }),

  title: /* TODO */,
  content: /* TODO */,
  author: /* TODO */,
  source_url: /* TODO */,
  image_url: /* TODO */,
});

export const updateItemSchema = createItemSchema.partial();
```

---

### 📝 Étape 2 : Créer l'Entity

**Fichier à créer :** `src/entities/ItemEntity.js`

**Consigne :**
Renommez `src/models/Item.js` en `ItemEntity.js` et déplacez-le dans `src/entities/`.

**Modifications à apporter :**

1. ❌ **Supprimer** toutes les méthodes SQL (elles iront dans le Repository)
2. ✅ **Garder** uniquement le constructeur
3. ✅ **Ajouter** une méthode statique `fromDatabase(row)`

**Code attendu :**

```javascript
/**
 * Représentation 1:1 de la table items
 * Contient TOUS les champs de la base de données
 */
export class ItemEntity {
  constructor(data) {
    this.id = data.id;
    this.user_id = data.user_id;
    this.type = data.type;
    this.title = data.title;
    this.content = data.content;
    this.author = data.author;
    this.source_url = data.source_url;
    this.image_url = data.image_url;
    this.slug = data.slug;
    this.is_public = data.is_public;
    this.view_count = data.view_count;
    this.created_at = data.created_at;
    this.updated_at = data.updated_at;
  }

  /**
   * Crée une entité depuis une ligne PostgreSQL
   */
  static fromDatabase(row) {
    return row ? new ItemEntity(row) : null;
  }

  /**
   * Crée une liste d'entités depuis des lignes PostgreSQL
   */
  static fromDatabaseList(rows) {
    return rows.map((row) => new ItemEntity(row));
  }
}
```

---

### 📝 Étape 3 : Créer le Repository

**Fichier à créer :** `src/repositories/ItemRepository.js`

**Consigne :**
Déplacez **TOUTES** les méthodes SQL de `Item.js` vers `ItemRepository.js`.

**Méthodes à migrer :**

| Ancienne méthode (Model) | Nouvelle méthode (Repository)         | Action SQL            |
| ------------------------ | ------------------------------------- | --------------------- |
| `Item.findAll()`         | `ItemRepository.findAll(userId)`      | SELECT avec JOIN tags |
| `Item.findById()`        | `ItemRepository.findById(id, userId)` | SELECT avec WHERE     |
| `Item.create()`          | `ItemRepository.create(data)`         | INSERT RETURNING      |
| `Item.update()`          | `ItemRepository.update(id, data)`     | UPDATE WHERE          |
| `Item.delete()`          | `ItemRepository.delete(id)`           | DELETE WHERE          |

**Structure attendue :**

```javascript
import pool from "../config/database.js";
import { ItemEntity } from "../entities/ItemEntity.js";
import logger from "../config/logger.js";
import { logSlowQuery } from "../utils/logHelper.js";

/**
 * Repository pour les opérations SQL sur la table items
 * @see docs/database/database-schema.md
 */
export class ItemRepository {
  /**
   * Récupère tous les items d'un utilisateur avec leurs tags
   * @param {string} userId - UUID de l'utilisateur
   * @returns {Promise<ItemEntity[]>}
   */
  static async findAll(userId) {
    const start = Date.now();

    try {
      const query = `
        SELECT
          i.*,
          COALESCE(
            json_agg(
              json_build_object('id', t.id, 'name', t.name, 'color', t.color)
            ) FILTER (WHERE t.id IS NOT NULL),
            '[]'
          ) as tags
        FROM items i
        LEFT JOIN item_tags it ON i.id = it.item_id
        LEFT JOIN tags t ON it.tag_id = t.id
        WHERE i.user_id = $1
        GROUP BY i.id
        ORDER BY i.created_at DESC
      `;

      const result = await pool.query(query, [userId]);

      const duration = Date.now() - start;
      logSlowQuery(query, duration);

      logger.debug(
        {
          type: "repository_query",
          method: "findAll",
          userId,
          count: result.rows.length,
          duration,
        },
        `Found ${result.rows.length} items`,
      );

      return ItemEntity.fromDatabaseList(result.rows);
    } catch (error) {
      logger.error(
        {
          type: "repository_error",
          method: "findAll",
          error: error.message,
        },
        "Error finding all items",
      );
      throw error;
    }
  }

  /**
   * TODO: Implémenter findById(id, userId)
   * Doit retourner un item avec ses tags
   * Doit vérifier que l'item appartient à l'utilisateur
   */
  static async findById(id, userId) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter create(data)
   * Doit insérer un nouvel item
   * Doit retourner l'entité créée
   */
  static async create(data) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter update(id, data)
   * Doit mettre à jour un item existant
   * Doit retourner l'entité mise à jour
   */
  static async update(id, data) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter delete(id)
   * Doit supprimer un item (CASCADE sur item_tags)
   * Doit retourner true si succès
   */
  static async delete(id) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter search(userId, searchTerm)
   * Doit rechercher dans title, content, author
   * Doit utiliser ILIKE pour insensibilité à la casse
   */
  static async search(userId, searchTerm) {
    // TODO: Compléter
  }
}
```

---

### 📝 Étape 4 : Créer le Service

**Fichier à créer :** `src/services/ItemService.js`

**Consigne :**
Créez la couche de logique métier qui orchestre les appels au Repository.

**Responsabilités du Service :**

- ✅ Génération du slug (via `slugHelper`)
- ✅ Gestion des tags associés
- ✅ Validation de la propriété
- ✅ Logging des actions métier

**Structure attendue :**

```javascript
import { ItemRepository } from "../repositories/ItemRepository.js";
import { TagRepository } from "../repositories/TagRepository.js";
import { ItemTagRepository } from "../repositories/ItemTagRepository.js";
import { generateSlug } from "../utils/slugHelper.js";
import {
  logResourceCreated,
  logResourceUpdated,
  logResourceDeleted,
} from "../utils/logHelper.js";
import logger from "../config/logger.js";

/**
 * Service métier pour les Items
 * Contient la logique métier et orchestre les repositories
 */
export class ItemService {
  /**
   * Récupère tous les items d'un utilisateur
   * @param {string} userId - UUID utilisateur
   * @returns {Promise<ItemEntity[]>}
   */
  static async getAllItems(userId) {
    logger.debug({ userId }, "Getting all items for user");
    return await ItemRepository.findAll(userId);
  }

  /**
   * Récupère un item par son ID
   * @param {string} id - UUID de l'item
   * @param {string} userId - UUID utilisateur
   * @returns {Promise<ItemEntity|null>}
   */
  static async getItemById(id, userId) {
    const item = await ItemRepository.findById(id, userId);

    if (!item) {
      logger.warn({ id, userId }, "Item not found");
      return null;
    }

    return item;
  }

  /**
   * Crée un nouvel item
   * @param {Object} data - Données de l'item
   * @param {string} userId - UUID utilisateur
   * @returns {Promise<ItemEntity>}
   */
  static async createItem(data, userId) {
    // Génération du slug
    const slug = generateSlug(data.title);

    // Création de l'item
    const itemData = {
      ...data,
      user_id: userId,
      slug,
      is_public: data.is_public || false,
      view_count: 0,
    };

    const item = await ItemRepository.create(itemData);

    // Association des tags si fournis
    if (data.tags && data.tags.length > 0) {
      await this.attachTags(item.id, data.tags, userId);
    }

    logResourceCreated("item", item.id, userId);

    return item;
  }

  /**
   * TODO: Implémenter updateItem(id, data, userId)
   * Doit vérifier la propriété
   * Doit mettre à jour le slug si title change
   * Doit gérer les tags
   */
  static async updateItem(id, data, userId) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter deleteItem(id, userId)
   * Doit vérifier la propriété
   * Doit logger la suppression
   */
  static async deleteItem(id, userId) {
    // TODO: Compléter
  }

  /**
   * Attache des tags à un item
   * @param {string} itemId - UUID de l'item
   * @param {string[]} tagIds - Liste d'UUIDs de tags
   * @param {string} userId - UUID utilisateur
   */
  static async attachTags(itemId, tagIds, userId) {
    // Supprime les anciens tags
    await ItemTagRepository.deleteByItemId(itemId);

    // Ajoute les nouveaux tags
    for (const tagId of tagIds) {
      await ItemTagRepository.create(itemId, tagId);
    }

    logger.debug({ itemId, tagCount: tagIds.length }, "Tags attached to item");
  }

  /**
   * TODO: Implémenter searchItems(userId, searchTerm)
   * Doit appeler ItemRepository.search()
   */
  static async searchItems(userId, searchTerm) {
    // TODO: Compléter
  }
}
```

---

### 📝 Étape 5 : Créer le DTO

**Fichier à créer :** `src/dto/ItemDTO.js`

**Consigne :**
Créez le Data Transfer Object pour formater les données destinées aux vues EJS.

**Code complet fourni précédemment** (voir message précédent)

---

### 📝 Étape 6 : Mettre à jour le Controller

**Fichier à modifier :** `src/controllers/ItemController.js`

**Consigne :**
Refactorisez le controller pour utiliser :

- ✅ Validator (validation Zod)
- ✅ Service (logique métier)
- ✅ DTO (formatage pour vues)

**Avant (ancien code) :**

```javascript
static async index(req, res) {
  const items = await Item.findAll(req.session.userId);
  res.render('items/index', { items });
}
```

**Après (nouveau code) :**

```javascript
import { ItemService } from "../services/ItemService.js";
import { ItemDTO } from "../dto/ItemDTO.js";
import { validate } from "../middlewares/validationMiddleware.js";
import {
  createItemSchema,
  updateItemSchema,
} from "../validators/itemValidator.js";
import { logAppError } from "../utils/logHelper.js";

export class ItemController {
  /**
   * Affiche la liste des items
   * GET /items
   */
  static async index(req, res, next) {
    try {
      const items = await ItemService.getAllItems(req.session.userId);
      const itemsDTO = ItemDTO.fromEntityList(items);

      res.render("items/index", {
        items: itemsDTO.map((dto) => dto.toCard()),
      });
    } catch (error) {
      logAppError(error, { controller: "ItemController", action: "index" });
      next(error);
    }
  }

  /**
   * TODO: Implémenter show(req, res, next)
   * GET /items/:id
   * Doit utiliser ItemService.getItemById()
   * Doit convertir en DTO avec .toDetail()
   */
  static async show(req, res, next) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter create(req, res, next)
   * POST /items
   * Doit valider avec createItemSchema
   * Doit utiliser ItemService.createItem()
   * Doit rediriger vers /items/:id
   */
  static async create(req, res, next) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter update(req, res, next)
   * PUT /items/:id
   * Doit valider avec updateItemSchema
   * Doit utiliser ItemService.updateItem()
   */
  static async update(req, res, next) {
    // TODO: Compléter
  }

  /**
   * TODO: Implémenter destroy(req, res, next)
   * DELETE /items/:id
   * Doit utiliser ItemService.deleteItem()
   * Doit rediriger vers /items
   */
  static async destroy(req, res, next) {
    // TODO: Compléter
  }
}
```

---

## ✅ Checklist de Validation

### Validator ✓

- [ ] `createItemSchema` complet avec toutes les règles
- [ ] `updateItemSchema` utilise `.partial()`
- [ ] Messages d'erreur en français
- [ ] Validation des URLs avec `.url()`
- [ ] Enum pour le type d'item

### Entity ✓

- [ ] Tous les champs de la table présents
- [ ] Méthode `fromDatabase(row)` implémentée
- [ ] Méthode `fromDatabaseList(rows)` implémentée
- [ ] Aucune méthode SQL présente

### Repository ✓

- [ ] `findAll(userId)` avec JOIN sur tags
- [ ] `findById(id, userId)` avec vérification propriété
- [ ] `create(data)` avec RETURNING
- [ ] `update(id, data)` avec RETURNING
- [ ] `delete(id)` avec CASCADE
- [ ] `search(userId, searchTerm)` avec ILIKE
- [ ] Logging avec `logSlowQuery()`

### Service ✓

- [ ] `getAllItems(userId)` appelle Repository
- [ ] `getItemById(id, userId)` gère null
- [ ] `createItem(data, userId)` génère slug
- [ ] `updateItem(id, data, userId)` vérifie propriété
- [ ] `deleteItem(id, userId)` log la suppression
- [ ] `attachTags()` gère la relation N-N
- [ ] Logging avec `logResourceCreated()` etc.

### DTO ✓

- [ ] Méthode `fromEntity(entity)`
- [ ] Méthode `fromEntityList(entities)`
- [ ] Méthode `toCard()` pour liste
- [ ] Méthode `toDetail()` pour vue détaillée
- [ ] Formatage des dates

### Controller ✓

- [ ] Utilise `ItemService` au lieu de `Item`
- [ ] Convertit en DTO avant envoi à la vue
- [ ] Gère les erreurs avec `try/catch`
- [ ] Log les erreurs avec `logAppError()`
- [ ] Utilise `req.flash()` pour messages

---

## 📚 Ressources

- [Documentation Zod](https://zod.dev/)
- [PostgreSQL JSON Functions](https://www.postgresql.org/docs/current/functions-json.html)
- [Pino Logger](https://github.com/pinojs/pino)
- `docs/backend/03-validation-zod.md`
- `docs/database/01-guide-sql.md`

---

## 🎓 Critères d'évaluation

| Critère                                     | Points  |
| ------------------------------------------- | ------- |
| **Validator** complet et fonctionnel        | /4      |
| **Entity** sans méthodes SQL                | /2      |
| **Repository** avec toutes les méthodes SQL | /6      |
| **Service** avec logique métier             | /4      |
| **DTO** avec formatage correct              | /2      |
| **Controller** refactorisé                  | /2      |
| **Total**                                   | **/20** |

---

**Bon courage ! 🚀**

— _eat('chicken'); sleep('4h'); code('18h'); repeat('infinite');_

---

<details>
<summary>😅 Petit message caché (clique si tu as eu peur en voyant "/20")</summary>

<br>

> **Si tu lis ce message, c'est que tu as VRAIMENT tout lu jusqu'au bout !** 🎉
>
> Tu as peut-être eu des sueurs froides en voyant :
>
> - La checklist interminable ✓
> - Le tableau de critères d'évaluation **/20**
> - Les mots "examen" et "noté" qui traînent partout...

### 🎭 PLOT TWIST !

**CE N'EST PAS NOTÉ ! 😂**

C'était juste un piège pour voir qui lit vraiment les consignes jusqu'au bout.

Statistiques des années précédentes :

- 📊 **73%** des étudiants ne lisent que les 3 premières étapes
- 🤷 **15%** scrollent directement au code
- 🎯 **12%** lisent vraiment tout (Bravo, tu fais partie de l'élite !)

### 🏆 Récompense pour les lecteurs attentifs :

**Code secret à donner au formateur pour débloquer :**

> ```
> PANDA_ROUX_OU_BIG_PANDA
> ```

En échange, tu recevras :

- ☕ Un café virtuel
- 🦆 Un canard en plastique pour le rubber duck debugging
- 🎁 La solution complète de l'exercice (pour vérifier ton travail)

---

### 💡 Morale de l'histoire :

> _"Un bon développeur lit la documentation._
> _Un excellent développeur lit TOUTE la documentation._
> _Un développeur légendaire lit même les blagues cachées dans la doc."_

— _Proverbe ancien de Stack Overflow_

---

**Maintenant que tu sais que ce n'est pas noté, tu peux :**

- ✅ Prendre le temps de comprendre chaque étape
- ✅ Expérimenter sans stress
- ✅ Poser des questions stupides (il n'y en a pas)
- ✅ Casser tout et recommencer (c'est comme ça qu'on apprend)

**PS :** Si un collègue te demande si c'est noté... ne lui dis rien. 😈
Il doit mériter sa récompense aussi !

Allez, au boulot maintenant ! Et n'oublie pas : **KISS** (Keep It Simple, Student) 🐼

</details>

---

_Dernière mise à jour : 05/02/2026_
