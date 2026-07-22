# Opintorekisteri REST API (Tietokannat ja rajapinnat -harjoitustyö)

Tämä on Node.js/Express- ja MySQL/MariaDB-pohjainen REST API -sovellus, joka toteuttaa opintorekisterin hallinnan (CRUD-operaatiot) sekä JWT-pohjaisen käyttäjän autentikoinnin.

## 📽️ Esittelyvideo
[Katso esittelyvideo tästä (YouTube / Vimeo / Google Drive linkki)](TÄHÄN_SINUN_VIDEOLINKKI)

---

## 🛠️ Sovelluksen rakenne ja teknologiat

Sovellus noudattaa **MVC-arkkitehtuuria** (Model-View-Controller):

* **Backend:** Node.js & Express
* **Tietokanta:** MySQL / MariaDB
* **Autentikointi:** JSON Web Token (JWT) & bcrypt (salasanojen kryptaus)
* **Tietokantayhteys:** `mysql2/promise`

### Tietokannan rakenne (ER-diagrammi)

Tietokanta `opintorekisteri` koostuu neljästä taulusta:

1. **`opiskelija`**: Opiskelijoiden tiedot (`opiskelijanumero` PK, `etunimi`, `sukunimi`).
2. **`opintojakso`**: Kurssitiedot (`kurssikoodi` PK, `nimi`, `opintopisteet`).
3. **`arviointi`**: Arvosanatiedot (`id` PK, `opiskelijanumero` FK, `kurssikoodi` FK, `arvosana`, `paivamaara`).
4. **`user`**: Autentikointikäyttäjät (`id` PK, `kayttajatunnus`, `salasana`).

```mermaid
erDiagram
    OPISKELIJA ||--o{ ARVIOINTI : "saa"
    OPINTOJAKSO ||--o{ ARVIOINTI : "sisältää"

    OPISKELIJA {
        string opiskelijanumero PK
        string etunimi
        string sukunimi
    }

    OPINTOJAKSO {
        string kurssikoodi PK
        string nimi
        int opintopisteet
    }

    ARVIOINTI {
        int id PK
        string opiskelijanumero FK
        string kurssikoodi FK
        int arvosana
        date paivamaara
    }

    USER {
        int id PK
        string kayttajatunnus
        string salasana
    }



<img width="1035" height="770" alt="image" src="https://github.com/user-attachments/assets/942d297e-c6e9-4d57-9a44-3495ce211c3d" />

