---
# Financial Data CSV Structuur

Deze README beschrijft de structuur van de gegenereerde CSV-bestanden die voortkomen uit de verwerking van JSON-gegevens. De data is genormaliseerd om redundantie te verminderen en de bruikbaarheid voor data-analyse te verbeteren.

## Overzicht van CSV-bestanden

1. [firms.csv](#firmscsv)
2. [addresses.csv](#addressescsv)
3. [activities.csv](#activitiescsv)
4. [firm_change.csv](#firm_changecsv)
5. [annual_accounts.csv](#annual_accountscsv)
6. [Lookup Tables](#lookup-tables)
   - [nace_codes.csv](#nace_codescsv)
   - [classification_codes.csv](#classification_codescsv)
   - [type_of_enterprise.csv](#type_of_enterprisecsv)
   - [status.csv](#statuscsv)
   - [juridical_form.csv](#juridical_formcsv)
   - [account_codes.csv](#account_codescsv)

---

## firms.csv

Bevat kerninformatie over elke onderneming.

| Kolomnaam                   | Beschrijving                                                                 |
|-----------------------------|------------------------------------------------------------------------------|
| **enterprise_number**       | Unieke identificatie voor elke onderneming                                   |
| **denomination**            | Naam van de onderneming                                                     |
| **type_of_enterprise_code** | Code die het type onderneming aangeeft (verwijst naar `type_of_enterprise.csv`) |
| **status_code**             | Code die de status van de onderneming aangeeft (verwijst naar `status.csv`) |
| **start_date**              | Startdatum van de onderneming (YYYY-MM-DD)                                  |
| **juridical_form_code**     | Code die de juridische vorm aangeeft (verwijst naar `juridical_form.csv`)    |

*Let op: Adresinformatie is verplaatst naar `addresses.csv`.*

---

## addresses.csv

Bevat adresinformatie voor elke onderneming.

| Kolomnaam           | Beschrijving                            |
|---------------------|-----------------------------------------|
| **enterprise_number** | Verwijzing naar `firms.csv`              |
| **street**           | Straatnaam                              |
| **house_number**     | Huisnummer                              |
| **box**              | Busnummer (indien van toepassing)       |
| **zipcode**          | Postcode                                |
| **city**             | Stad                                    |
| **country**          | Land                                    |

---

## activities.csv

Bevat activiteiteninformatie voor elke onderneming.

| Kolomnaam               | Beschrijving                                                                                  |
|-------------------------|-----------------------------------------------------------------------------------------------|
| **enterprise_number**   | Verwijzing naar `firms.csv`                                                                    |
| **activity_number**     | Volgnummer van de activiteit binnen de onderneming                                             |
| **nace_code**           | NACE-code voor de activiteit (verwijst naar `nace_codes.csv`)                                 |
| **classification_code** | Classificatiecode van de activiteit (verwijst naar `classification_codes.csv`)                |

---

## firm_change.csv

Bevat historische informatie over de juridische situatie van ondernemingen.

| Kolomnaam              | Beschrijving                                         |
|------------------------|------------------------------------------------------|
| **enterprise_number**   | Verwijzing naar `firms.csv`                          |
| **year**                | Jaar van de juridische situatie                      |
| **juridical_situation** | Beschrijving van de juridische situatie in dat jaar   |

---

## annual_accounts.csv

Bevat financiële jaarrekeningen in een breed formaat, waarbij elke kolom een financiële metriek vertegenwoordigt.

| Kolomnaam           | Beschrijving                                                                          |
|---------------------|---------------------------------------------------------------------------------------|
| **enterprise_number** | Verwijzing naar `firms.csv`                                                           |
| **year**              | Jaar van de financiële gegevens                                                      |
| **[code]**            | Waarde van de financiële metriek geïdentificeerd door de code (bijv. `10`, `13`, `14`, ...) |

*Voorbeeldkolommen:* `10`, `13`, `14`, `17`, `22/27`, `28`, `29/58`, `40/41`, `54/58`, `630`, `640/8`, `65/66B`, `9900`, `9901`, `9903`, `9904`, `9905`, `9906`, etc.

---

## Lookup Tables

### nace_codes.csv

Bevat de beschrijvingen van NACE-codes.

| Kolomnaam   | Beschrijving                      |
|-------------|-----------------------------------|
| **nace_code**   | NACE-code                        |
| **description**  | Beschrijving van de NACE-code      |

### classification_codes.csv

Bevat de beschrijvingen van classificatiecodes.

| Kolomnaam               | Beschrijving                           |
|-------------------------|----------------------------------------|
| **classification_code** | Classificatiecode                      |
| **classification_description** | Beschrijving van de classificatiecode  |

### type_of_enterprise.csv

Bevat de types van ondernemingen.

| Kolomnaam                      | Beschrijving                       |
|--------------------------------|------------------------------------|
| **type_of_enterprise_code**    | Code voor het type onderneming     |
| **type_of_enterprise_description** | Beschrijving van het type onderneming |

### status.csv

Bevat de statusinformatie van ondernemingen.

| Kolomnaam        | Beschrijving                   |
|------------------|--------------------------------|
| **status_code**  | Code voor de status            |
| **status_description** | Beschrijving van de status        |

### juridical_form.csv

Bevat de juridische vormen van ondernemingen.

| Kolomnaam               | Beschrijving                             |
|-------------------------|------------------------------------------|
| **juridical_form_code** | Code voor de juridische vorm             |
| **juridical_form_description** | Beschrijving van de juridische vorm      |

### account_codes.csv

Bevat de beschrijvingen van financiële accountcodes.

| Kolomnaam | Beschrijving                                 |
|-----------|----------------------------------------------|
| **code**      | Financiële accountcode                        |
| **description** | Beschrijving van de financiële accountcode    |

---

## Entity-Relationship (ER) Diagram

Hieronder vind je het ER-diagram dat de relaties tussen de verschillende CSV-bestanden visueel weergeeft. Gebruik een Markdown-editor die Mermaid ondersteunt om het diagram correct te renderen.

### Gebruik met Fenced Code Blocks

```mermaid
erDiagram
    FIRMS {
        string enterprise_number PK
        string denomination
        string type_of_enterprise_code FK
        string status_code FK
        date start_date
        string juridical_form_code FK
    }

    ADDRESSES {
        string enterprise_number PK
        string street
        string house_number
        string box
        string zipcode
        string city
        string country
    }

    ACTIVITIES {
        string enterprise_number PK, FK
        int activity_number PK
        string nace_code FK
        string classification_code FK
    }

    FIRM_CHANGE {
        string enterprise_number PK, FK
        int year PK
        string juridical_situation
    }

    ANNUAL_ACCOUNTS {
        string enterprise_number PK, FK
        int year PK
        string code FK
        float value
    }

    NACE_CODES {
        string nace_code PK
        string description
    }

    CLASSIFICATION_CODES {
        string classification_code PK
        string classification_description
    }

    TYPE_OF_ENTERPRISE {
        string type_of_enterprise_code PK
        string type_of_enterprise_description
    }

    STATUS {
        string status_code PK
        string status_description
    }

    JURIDICAL_FORM {
        string juridical_form_code PK
        string juridical_form_description
    }

    ACCOUNT_CODES {
        string code PK
        string description
    }

    FIRMS ||--|| ADDRESSES : "heeft"
    FIRMS ||--o{ ACTIVITIES : "heeft"
    FIRMS ||--o{ FIRM_CHANGE : "heeft"
    FIRMS ||--o{ ANNUAL_ACCOUNTS : "heeft"

    ACTIVITIES }|..|{ NACE_CODES : "gebruikt"
    ACTIVITIES }|..|{ CLASSIFICATION_CODES : "gebruikt"

    FIRMS }|..|{ TYPE_OF_ENTERPRISE : "is van type"
    FIRMS }|..|{ STATUS : "heeft status"
    FIRMS }|..|{ JURIDICAL_FORM : "heeft juridische vorm"

    ANNUAL_ACCOUNTS }|..|{ ACCOUNT_CODES : "gebruikt"
