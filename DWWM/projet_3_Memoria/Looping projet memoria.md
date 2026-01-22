# Modele E/A (entité / association)
---

![[Looping_memoria_EA.png]]

# Modele UML (Unified Modeling Language)
	- Utile pour les créations de classes 
---

![[Looping_memoria_UML.png]]

# Modèle MLD [[vocabulaire-formation]]
	- Création des cléfs etrangeres 
---

![[Looping_memoria_MLD.png]]


# rendu mld écrit 
---


```js
users = (id_user UUID_v7, email VARCHAR(100) , password_hash VARCHAR(255) , pseudo VARCHAR(50) , role_name enum (customer, admin et super_admin), auth_provider enum(local, google, azure, apple), settings_user JSONB, gdpr_consent BOOLEAN, gdpr_consent_date TIMESTAMP, created_at TIMESTAMP, updated_at TIMESTAMP);
tags = (id_tag UUID v7, tag_name VARCHAR(50) , created_at TIMESTAMP, updated_at TIMESTAMP, #user_id);
Pépites = (id_item UUID v7, type Enum (Livre,  Podcast, Article, Vidéo, Note), title VARCHAR(100) , slug VARCHAR(255) , content text ou blob, source_author VARCHAR(50) , metadata JSONB, created_at TIMESTAMP, updated_at TIMESTAMP, thumbnail_url VARCHAR(255) , #user_id);
shares = (id_share UUID v7, recipient_email VARCHAR(100) , share_token VARCHAR(255) , access_config JSONB, created_at TIMESTAMP, updated_at TIMESTAMP, #id_item);
Etiqueter = (#id_tag, #id_item);

```


# rendu LDD écrit 
---

![[rendu LDD.png.png]]