## 🧠 Sommaire – Base de données _Memoria_

### 📌 Fondamentaux

- [[#Liste des données importantes]]
- [[#SQL vs NoSQL]]
- [[#Glossaire pour la base de données]]
---
### 🔐 Sécurité & bonnes pratiques

- [[#Règles de sécurité et bonnes pratiques]]
    
    - [[#Ne JAMAIS connecter l'application avec le rôle postgres]]
        
    - [[#Toujours hasher les mots de passe]]
        
    - [[#RGPD Cascade et droit à l'oubli]]
        

---

### 📊 Performance & indexation

- [[#Règles d'indexation Performance]]
    
    - [[#Index automatiques PostgreSQL]]
        
    - [[#Quand créer un index manuel]]
        
    - [[#Index spécialisés]]
        
    - [[#Index conditionnels]]
        
    - [[#Éviter la sur-indexation]]
        

---

### 🎯 Types de données

- [[#Règles sur les types de données]]
    
    - [[#ENUM vs VARCHAR CHECK]]
        
    - [[#CITEXT pour email et pseudo]]
        
    - [[#JSONB vs JSON]]
        
    - [[#UUID v7 pour les identifiants]]
        

---

### 🔄 Relations & intégrité

- [[#Règles sur les relations cardinalités]]
    
    - [[#Vérifier les cardinalités métier]]
        
    - [[#ON DELETE CASCADE vs SET NULL]]
        

---

### ⚡ Automatisation

- [[#Règles d'automatisation]]
    
    - [[#Trigger pour updated_at]]
        
    - [[#Valeurs par défaut intelligentes]]
        

---

### 🔍 Recherche avancée

- [[#Règles de recherche]]
    
    - [[#Full-text search]]
        
    - [[#Recherche floue Trigram]]
        

---

### 📋 Préparation production

- [[#Checklist avant mise en production]]
    
    - [[#Sécurité]]
        
    - [[#Performance]]
        
    - [[#Intégrité]]
        
    - [[#Documentation]]
        

---

### 🐼 Philosophie de conception

- [[#Principe KISS appliqué à la DB]]
    
    - [[#Faire simple]]
        
    - [[#Over-engineering]]
        
    - [[#Quand complexifier]]
## Liste des données importantes

Voici une liste non-exhaustive de quelques données qu’il est judicieux d’enregistrer dans la plupart des tables d’une base de données :

- Un identifiant unique,  “ID”, qui sert de clé primaire (PRIMARY KEY)
- Un élément aléatoire lié à la sécurité, tel qu’un “hash”, un “salt” ou une “key”. Il peut s’agir d’une chaîne aléatoire encodée en MD5 (ou SHA1) par exemple à utiliser en complément de l’identifiant unique pour éviter les failles CSRF (Cross-Site Request Forgery)
- Les informations lors de l’ajout de la ligne :
    - La date d’ajout sous la forme d’un DATETIME local ou GMT ou d’un TIMESTAMP
    - Si applicable : une clé étrangère (cf. FOREIGN KEY) liée au compte ou à l’utilisateur qui a ajouté la donnée
    - Si applicable : l’adresse IP de la personne qui ajoute l’information
    - Si applicable : le hostname de cette adresse IP
    - Si applicable : le user agent
    - Si applicable : le détail pour savoir si la ligne a été modifiée à partir de l’interface utilisateur, de l’interface administrateur, d’un CRON ou toute autre interface
- Les mêmes informations lors de la dernière modification de la ligne
- Un commentaire privé destiné à se souvenir des détails concernant cette ligne
- Une information pour savoir si la ligne est active ou si elle a été supprimée, tel que “is_active” ou “is_deleted”. Cela permet de conserver la données tout en la supprimant artificiellement au yeux des utilisateurs en filtrant sur cette valeur

| **SQL (Relationnelle)**            | **NoSQL (not SQL = non structuré)**                       |
| ---------------------------------- | --------------------------------------------------------- |
| - A besoin d'être structuré        | - stocker dans sa base de données sous forme de document  |
| - recherche beaucoup plus direct   | - utilisé pour des produit/settings/                      |
| - Pas besoin de dupliquer les clés | - Stock et lit des JSON                                   |
| -  *+* puissant                    | - relation clé -> valeur                                  |
|                                    | - *+* pratique pour un chat  ou pour afficher des données |
|                                    | - est limité                                              |


# Guide de mise en œuvre de la base de données "Memoria"

## Glossaire pour la base de données

- **DCL (Data Control Language) :** Commandes pour gérer les droits et l'accès (ex: `CREATE USER`, `GRANT`). C'est de la sécurité.

- **DDL (Data Definition Language) :** Commandes pour définir la structure (ex: `CREATE TABLE`, `ALTER`). C'est de l'architecture.

- **DML (Data Manipulation Language) :** Commandes pour manipuler les données (ex: `SELECT`, `INSERT`, `UPDATE`, `DELETE`). C'est le contenu.
---
## 🔐 Règles de sécurité et bonnes pratiques


### **1. Ne JAMAIS connecter l'application avec le rôle `postgres`**

```sql

-- ❌ DANGEREUX : Utiliser postgres en production

DATABASE_URL=postgresql://postgres:password@localhost/memoria_db

  

-- ✅ CORRECT : Créer un rôle applicatif dédié

CREATE ROLE app_memoria WITH LOGIN PASSWORD 'unpandarouxquidort';

GRANT ALL PRIVILEGES ON DATABASE memoria_db TO app_memoria;

  

-- Dans l'application :

DATABASE_URL=postgresql://app_memoria:unpandarouxquidort@localhost/memoria_db

```

**Pourquoi ?**

- `postgres` = super-admin → Peut supprimer TOUTE la base

- `app_memoria` = droits limités → Risques réduits en cas de faille

---
### **2. Toujours hasher les mots de passe (côté backend)**

```sql

-- ❌ JAMAIS stocker en clair

INSERT INTO users (password) VALUES ('monmotdepasse123');

  

-- ✅ TOUJOURS hasher avec bcrypt (côté applicatif Node.js/PHP/Python/Java)

const bcrypt = require('bcrypt');

const hash = await bcrypt.hash('monmotdepasse123', 10);

INSERT INTO users (password_hash) VALUES ($1);  -- $1 = hash

```

**Algorithmes recommandés :**

- **bcrypt** (standard, 10-12 rounds)

- **Argon2** (plus moderne, recommandé OWASP 2024)

---
### **3. RGPD : Cascade et droit à l'oubli**

```sql

-- ✅ Si un user est supprimé, tout doit disparaître

CREATE TABLE items (

    user_id UUID REFERENCES users(id_user) ON DELETE CASCADE

);

  

-- ❌ Sans CASCADE, la suppression échoue si l'utilisateur a des données liées

```

**Article RGPD concerné :** Article 17 (Droit à l'effacement)

---
## 📊 Règles d'indexation (Performance)

### **1. PostgreSQL crée automatiquement des index pour :**

| **Contrainte** | **Index auto ?** | **Type** |

|---|---|---|

| `PRIMARY KEY` | ✅ OUI | B-tree UNIQUE |

| `UNIQUE` | ✅ OUI | B-tree UNIQUE |

| `FOREIGN KEY` | ❌ NON | *Aucun* (à créer manuellement) |


```sql

-- ❌ REDONDANT : email est déjà UNIQUE

CREATE TABLE users (email CITEXT UNIQUE);

CREATE INDEX idx_users_email ON users (email);  -- Inutile !

  

-- ✅ NÉCESSAIRE : Foreign Key (pas d'index auto)

CREATE TABLE items (user_id UUID REFERENCES users(id_user));

CREATE INDEX idx_items_user ON items (user_id);  -- Obligatoire !

```
---
### **2. Quand créer un index manuel ?**

#### **✅ Index obligatoires**

  

```sql

-- Foreign Keys (jamais d'index auto)

CREATE INDEX idx_items_user ON items (user_id);

  

-- Colonnes souvent filtrées (WHERE)

CREATE INDEX idx_items_type ON items (content_type);

  

-- Colonnes souvent triées (ORDER BY ... DESC)

CREATE INDEX idx_items_created ON items (created_at DESC);

```

#### **✅ Index spécialisés**

```sql

-- Recherche full-text (français)

CREATE INDEX idx_items_search ON items USING gin (

    to_tsvector('french', title || ' ' || content)

);

  

-- Recherche floue (Trigram)

CREATE INDEX idx_items_title_trgm ON items USING gin (title gin_trgm_ops);

  

-- JSONB (métadonnées flexibles)

CREATE INDEX idx_items_metadata ON items USING gin (metadata);

```

#### **✅ Index conditionnels (partial index)**

```sql

-- Index uniquement pour les événements utilisateurs (ignore les NULL)

CREATE INDEX idx_events_user ON app_events (user_id)

WHERE user_id IS NOT NULL;

```

**Avantage :** Index 50% plus petit (meilleures performances)

---
### **3. Éviter la sur-indexation**
#### **❌ Mauvaises pratiques**

```sql

-- Index sur TOUTES les colonnes (over-engineering)

CREATE INDEX idx_users_created ON users (created_at);  -- Jamais utilisé

CREATE INDEX idx_users_updated ON users (updated_at);  -- Jamais utilisé

  

-- Index sur des colonnes rarement filtrées

CREATE INDEX idx_items_source_author ON items (source_author);  -- Rare

```

**Coût d'un index inutile :**

- +10-30% de stockage

- +5-15% de temps sur INSERT/UPDATE

- Aucun gain sur SELECT

---
## 🎯 Règles sur les types de données

### **1. Utiliser ENUM au lieu de VARCHAR + CHECK**

```sql

-- ❌ MOINS PERFORMANT

event_category VARCHAR(20) CHECK (event_category IN ('analytics', 'audit'));

  

-- ✅ MEILLEUR (type natif PostgreSQL)

CREATE TYPE event_category_enum AS ENUM ('analytics', 'audit', 'monitoring', 'gdpr');

event_category event_category_enum NOT NULL;

```

**Avantages :**
- Typage fort (erreur claire si valeur invalide)

- Plus rapide (type natif vs contrainte)

- Autodocumenté (`\dT` dans psql)
---
### **2. CITEXT pour email et pseudo (insensibilité casse)**

```sql

-- ❌ Sensible à la casse (Panda@mail.com ≠ panda@mail.com)

email VARCHAR(255) UNIQUE;

  

-- ✅ Insensible à la casse (Panda@mail.com = panda@mail.com)

email CITEXT UNIQUE;

```

**Extension requise :**

```sql

CREATE EXTENSION IF NOT EXISTS "citext";

```

---
. JSONB vs JSON**

```sql

-- ❌ JSON : Texte brut, lent à interroger

settings JSON;

  

-- ✅ JSONB : Format binaire, indexable

settings JSONB NOT NULL DEFAULT '{}';

CREATE INDEX idx_users_settings ON users USING gin (settings);

```

**Différences :**

| **JSON** | **JSONB** |

|---|---|

| Stockage texte | Stockage binaire optimisé |

| Pas d'index possible | Indexable avec GIN |

| Préserve l'ordre des clés | Ordre non garanti |

| Plus rapide à insérer | Plus rapide à interroger |

---
### **4. UUID v7 pour les identifiants**

```sql

-- ❌ UUID v4 : Aléatoire (mauvais pour les index B-tree)

id_user UUID PRIMARY KEY DEFAULT gen_random_uuid();

  

-- ✅ UUID v7 : Contient un timestamp (trié naturellement)

id_user UUID PRIMARY KEY DEFAULT uuidv7();

```

**Avantages UUID v7 :**

- Tri naturel par date de création

- Meilleures performances d'index

- Compatible avec toutes les bases UUID
  
---
## 🔄 Règles sur les relations (cardinalités)
  
### **1. Vérifier les cardinalités métier**

```sql

-- ❌ FAUX : Un événement appartient toujours à un utilisateur

app_events (0,N) ──── (1,1) users

  

-- ✅ CORRECT : Un événement peut être système (sans user)

app_events (0,1) ──── (1,N) users

```

**En SQL :**

```sql

user_id UUID REFERENCES users(id_user) ON DELETE SET NULL  -- Nullable !

```

---
### **2. ON DELETE CASCADE vs SET NULL**

```sql

-- ✅ CASCADE : Supprimer les données liées (RGPD)

CREATE TABLE items (

    user_id UUID REFERENCES users(id_user) ON DELETE CASCADE

);

  

-- ✅ SET NULL : Garder l'historique (audit)

CREATE TABLE app_events (

    user_id UUID REFERENCES users(id_user) ON DELETE SET NULL

);

```

**Quand utiliser CASCADE ?**

- Données privées (items, tags)

- RGPD obligatoire

**Quand utiliser SET NULL ?**

- Logs/Événements (audit trail)

- Statistiques agrégées

---
## ⚡ Règles d'automatisation

  

### **1. Trigger pour updated_at**

```sql

-- Fonction réutilisable

CREATE OR REPLACE FUNCTION trigger_set_timestamp()

RETURNS TRIGGER AS $$

BEGIN

    NEW.updated_at = CURRENT_TIMESTAMP;

    RETURN NEW;

END;

$$ LANGUAGE plpgsql;

  

-- Application à chaque table

CREATE TRIGGER set_timestamp_users

BEFORE UPDATE ON users

FOR EACH ROW EXECUTE PROCEDURE trigger_set_timestamp();

```

**Pourquoi ?**

- Évite d'oublier de mettre à jour `updated_at` dans le code

- Cohérence garantie (base de données = source de vérité)

---
### **2. Valeurs par défaut intelligentes**

```sql

-- ✅ Timestamp automatique

created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP

  

-- ✅ UUID v7 automatique

id_user UUID PRIMARY KEY DEFAULT gen_random_uuid_v7()

  

-- ✅ JSONB vide par défaut

metadata JSONB NOT NULL DEFAULT '{}'

  

-- ✅ Rôle par défaut

role role_enum NOT NULL DEFAULT 'customer'

```

---
## 🔍 Règles de recherche

### **1. Full-text search (recherche textuelle)**

```sql

-- Index pour recherche en français

CREATE INDEX idx_items_search ON items USING gin (

    to_tsvector('french', coalesce(title, '') || ' ' || coalesce(content, ''))

);

  

-- Requête

SELECT * FROM items

WHERE to_tsvector('french', title || ' ' || content)

      @@ to_tsquery('french', 'panda & roux');

```

---
### **2. Recherche floue (Trigram)**

```sql

-- Extension requise

CREATE EXTENSION IF NOT EXISTS "pg_trgm";

  

-- Index

CREATE INDEX idx_items_title_trgm ON items USING gin (title gin_trgm_ops);

  

-- Requête (trouve "panda" même si on tape "penda")

SELECT * FROM items

WHERE title % 'penda'  -- Similarité floue

ORDER BY similarity(title, 'penda') DESC;

```

---
## 📋 Checklist avant mise en production

### **✅ Sécurité**

- [ ] Rôle applicatif créé (pas `postgres`)

- [ ] Mots de passe hashés (bcrypt/Argon2)

- [ ] RGPD : `ON DELETE CASCADE` sur données privées

- [ ] HTTPS activé (certificat SSL)

- [ ] Variables d'environnement sécurisées (.env)

### **✅ Performance**

- [ ] Index sur toutes les Foreign Keys

- [ ] Pas d'index redondants (vérifier avec UNIQUE)

- [ ] Index GIN pour JSONB et full-text

- [ ] UUID v7 au lieu de v4

### **✅ Intégrité**

- [ ] Contraintes UNIQUE sur colonnes uniques

- [ ] Contraintes CHECK pour les valeurs limitées (ou ENUM)

- [ ] NOT NULL sur colonnes obligatoires

- [ ] Trigger `updated_at` sur toutes les tables

### **✅ Documentation**

- [ ] Commentaires SQL sur tables et colonnes

- [ ] Diagramme de relations (ERD)

- [ ] Guide d'utilisation (ce fichier !)


---
## 🐼 Principe KISS appliqué à la DB

> **"Keep It Simple, Stupid"**

### **✅ Faire simple**

```sql

-- Simple et efficace

email CITEXT UNIQUE NOT NULL

```
### **❌ Over-engineering**

```sql

-- Complexe sans bénéfice

CREATE TABLE email_validations (

    id UUID PRIMARY KEY,

    user_id UUID REFERENCES users(id_user),

    email_hash VARCHAR(64),

    validation_token VARCHAR(255),

    validated_at TIMESTAMPTZ,

    -- ...
);
```

**Quand complexifier ?**

- Besoin métier réel (pas "au cas où")

- Performance mesurée (pas "je suppose que")

- Sécurité exigée (RGPD, PCI-DSS)



