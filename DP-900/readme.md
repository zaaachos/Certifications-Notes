# Microsoft Certified: Azure Data Fundamentals (DP-900)

Demonstrate foundational knowledge of core data concepts related to Microsoft Azure data services.

- ### Microsoft Learn [link](https://learn.microsoft.com/en-us/credentials/certifications/azure-data-fundamentals/?practice-assessment-type=certification)

## [Microsoft Azure Data Fundamentals: Explore core data concepts](https://learn.microsoft.com/en-us/training/paths/azure-data-fundamentals-explore-core-data-concepts/)

- ### [Explore core data concepts](https://learn.microsoft.com/en-us/training/modules/explore-core-data-concepts/)

  - **Types of Data**
    1. Structured Data
       - Adheres to a fixed schema.
       - Organized in tabular format (rows = entity instances, columns = attributes).
       - Commonly stored in relational databases using key values to link tables.
        **Example Table:**

            | CustomerID | Name  | Email          |
            |------------|-------|----------------|
            | 1          | Joe   | <joe@email.com>  |

    2. Semi-Structured Data
       - Has some structure but allows variation between entities.
       - JSON is a common format.
       - Fields can differ between records.

       **Example JSON:**

        ```json
        {
        "firstName": "Joe",
        "contact": [
                { "type": "email", "address": "joe@litware.com" }
            ]
        }
        ```

    3. Unstructured Data
       - No predefined format or schema.
       - Examples: text documents, images, audio files, videos, binary data.
       - More complex to store, query, and analyze.

  - **Data Stores**
    - **File Stores**: Store unstructured and semi-structured data (e.g., documents, media files).
    - **Databases**: Store structured data (and some semi-structured data in modern systems).

- ### [Explore data roles and services](https://learn.microsoft.com/en-us/training/modules/explore-roles-responsibilities-world-of-data/)

## [Microsoft Azure Data Fundamentals: Explore relational data in Azure](https://learn.microsoft.com/en-us/training/paths/azure-data-fundamentals-explore-relational-data/)

## [Microsoft Azure Data Fundamentals: Explore non-relational data in Azure](https://learn.microsoft.com/en-us/training/paths/azure-data-fundamentals-explore-non-relational-data/)

## [Microsoft Azure Data Fundamentals: Explore data analytics in Azure](https://learn.microsoft.com/en-us/training/paths/azure-data-fundamentals-explore-data-warehouse-analytics/)
