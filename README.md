# BerndsBlog
Repo für Web Engineering

---

## Dev

### Installation (dev, unter Windows)
 * `PS> npm install` -> Pakete installieren
 * `PS> start nodemon` -> Server starten, nodemon lädt automatisch neu wenn Dateien geändert wurden
 
### Testen

Manuell mit der PowerShell: `PS> curl http://localhost:8082/api/V1/<...>`

Oder mit [Postman](https://www.getpostman.com/) und der passenden [Collection](https://raw.githubusercontent.com/PalatinCoder/DieBernds/master/BerndBlog.postman_collection.json) zum Importieren. Die Collection enthält alle beschriebenen Szenarien für alle Endpunkte.


## API Dokumentation

### Allgemein
* Die einzelnen Endpoints werden mit dem Pfadpräfix `/api/V1` angesprochen.
* Der Header `Content-Type` ist anzugeben wenn Parameter im Request Body übertragen werden. Parameter können als JSON (`application/json`) oder als Key/Value (`application/x-www-form-urlencoded`) übertragen werden.
* Soll der Request authentifiziert sein, muss das Token im Header `x-bernd-token` angegeben werden. Das Token wird über den Endpunkt `/login` geliefert.

### Endpoints

#### User

##### Login
* Endpoint: `PUT /login`
* Parameter:
  * `username`
  * `password`

 
 ##### Passwort ändern
 * Endpoint: `PUT /passwordRecovery`
 * Authentifizierung: ja
 * Parameter:
   * `password`
   * `newPassword`
  
#### Blog

##### Alle Blogeinträge
* Endpoint `GET /blog`
* Authentifizierung:
  * ja: Alle Blogeinträge werden zurückgegeben
  * nein: Nur die öffentlichen Blogeinträge werden zurückgegeben

##### Bestimmer Blogeintrag
* Endpoint `GET /blog/:id`
* Authentifizierung
  * Für nicht-öffentliche Blogeinträge muss der Request authentifiziert sein, oder es wird HTTP 401 zurückgegeben.

##### Blogeintrag löschen
* Endpoint `DELETE /blog/:id`
* Authentifizierung
  * Für nicht-öffentliche Blogeinträge muss der Request authentifiziert sein, oder es wird HTTP 401 zurückgegeben.
  
##### Blogeintrag anlegen
* Endpoint `POST /blog`
* Authentifizierung: benötigt
* Parameter (alle Parameter werden benötigt)
  * `title`
  * `picture`
  * `picture`
  * `author`
  * `about`
  * `released`
  * `hidden`
  * `tags[]`

##### Blogeintrag bearbeiten
* Endpoint `PUT /blog/:id`
* Authentifizierung
  * Für nicht-öffentliche Blogeinträge muss der Request authentifiziert sein, oder es wird HTTP 401 zurückgegeben.
* Parameter (alle Parameter sind optional, nicht angegebene Attribute werden nicht geändert):
  * `title`
  * `picture`
  * `picture`
  * `author`
  * `about`
  * `released`
  * `hidden`
  * `tags[]`
