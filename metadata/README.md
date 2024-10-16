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
   - [nace_codes.csv](#nace_codecsv)
   - [classification_codes.csv](#classification_codecsv)
   - [type_of_enterprise.csv](#type_of_enterprisecsv)
   - [status.csv](#statuscsv)
   - [juridical_form.csv](#juridical_formcsv)
   - [account_codes.csv](#account_codescsv)

---

## firms.csv

Bevat kerninformatie over elke onderneming.

| Kolomnaam               | Beschrijving                                                                 |
|-------------------------|------------------------------------------------------------------------------|
| **enterprise_number**   | Unieke identificatie voor elke onderneming                                   |
| **denomination**        | Naam van de onderneming                                                     |
| **type_of_enterprise_code** | Code die het type onderneming aangeeft (verwijst naar `type_of_enterprise.csv`) |
| **status_code**         | Code die de status van de onderneming aangeeft (verwijst naar `status.csv`) |
| **start_date**          | Startdatum van de onderneming (YYYY-MM-DD)                                  |
| **juridical_form_code** | Code die de juridische vorm aangeeft (verwijst naar `juridical_form.csv`)    |

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

| Kolomnaam           | Beschrijving                                                                                  |
|---------------------|-----------------------------------------------------------------------------------------------|
| **enterprise_number** | Verwijzing naar `firms.csv`                                                                    |
| **activity_number**   | Volgnummer van de activiteit binnen de onderneming                                             |
| **nace_code**         | NACE-code voor de activiteit (verwijst naar `nace_codes.csv`)                                 |
| **classification_code** | Classificatiecode van de activiteit (verwijst naar `classification_codes.csv`)                |

---

## firm_change.csv

Bevat historische informatie over de juridische situatie van ondernemingen.

| Kolomnaam            | Beschrijving                                         |
|----------------------|------------------------------------------------------|
| **enterprise_number** | Verwijzing naar `firms.csv`                          |
| **year**              | Jaar van de juridische situatie                      |
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

| Kolomnaam                  | Beschrijving                       |
|----------------------------|------------------------------------|
| **type_of_enterprise_code** | Code voor het type onderneming     |
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

## Data Kwaliteit en Consistentie

- **Data Types**: Alle numerieke waarden zijn geconverteerd naar numerieke datatypes. Tekstvelden zijn in UTF-8 gecodeerd.
- **Missing Values**: Ontbrekende waarden zijn ingevuld met lege strings (`''`) om consistentie te waarborgen.
- **Naming Conventions**: Alle kolomnamen gebruiken snake_case voor consistentie en leesbaarheid.

## Compatibiliteit met Analyse Tools

De gestructureerde en genormaliseerde CSV-bestanden zijn geoptimaliseerd voor gebruik met Business Intelligence (BI) tools zoals Tableau en Power BI. Lookup tables maken het mogelijk om relaties te leggen tussen verschillende datasets, wat geavanceerde analyses en visualisaties mogelijk maakt.

## Documentatie en Onderhoud

- **Code Commentaar**: Het Python-script bevat uitgebreide commentaar om de stappen en de toegepaste aanbevelingen te verduidelijken.
- **ER Diagrammen**: Overweeg het maken van Entity-Relationship (ER) diagrammen om de relaties tussen de verschillende CSV-bestanden visueel weer te geven.
- **ReadMe Updates**: Houd deze README up-to-date met eventuele wijzigingen in de CSV-structuur of de verwerking van de data.

## Voorbeeld Gebruik

Hier is een kort overzicht van hoe de CSV-bestanden met elkaar verbonden zijn:

- **firms.csv** wordt verbonden met **addresses.csv** via `enterprise_number`.
- **firms.csv** wordt verbonden met **activities.csv** via `enterprise_number`.
- **activities.csv** gebruikt `nace_code` en `classification_code` die verwijzen naar **nace_codes.csv** en **classification_codes.csv**.
- **annual_accounts.csv** bevat financiële gegevens waarbij elke `code` verwijst naar **account_codes.csv**.
- **firms.csv** wordt verbonden met **firm_change.csv** via `enterprise_number`.
- **firms.csv** maakt gebruik van **type_of_enterprise.csv**, **status.csv**, en **juridical_form.csv** via respectievelijk `type_of_enterprise_code`, `status_code`, en `juridical_form_code`.

---

Door deze genormaliseerde structuur te volgen, wordt de data consistent, makkelijk te beheren en klaar voor geavanceerde analyses. Mocht je verdere vragen hebben of aanvullende documentatie wensen, aarzel dan niet om contact op te nemen.

---
