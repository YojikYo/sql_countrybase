# Countrybase

Here are the eight most populous countries in the world: 

| Id | Name           | Area      | Population    | Source                     |
|----|----------------|-----------|---------------|----------------------------|
| 18 |  India         | 3,287,240 | 1,348,834,400 | Based on 2011 census       |
| 27 |  Bangladesh    | 143,998   | 166,774,136   | —                          |
| 34 |  Pakistan      | 803,940   | 205,095,217   | Official population clock  |
| 42 |  Nigeria       | 923,768   | 200,962,000   | UN projection              |
| 46 |  United States | 9,833,517 | 329,424,894   | Official population clock  |
| 54 |  Brazil        | 8,515,767 | 210,076,263   | —                          |
| 59 |  China         | 9,640,821 | 1,397,906,480 | Official estimate          |
| 60 |  Indonesia     | 1,904,569 | 268,074,600   | Official annual projection |

1. Using your favorite DB client, design and create a database table called `countries` that would store the information presented above (create a database first if you don’t have any existing ones to play with). Don’t bother with creating any keys or indices for now, just create the five columns. Copy and paste the SQL query generated by the client below (it should start with `create table` or something similar; if it is difficult to find the query generated by your client, ask for assistance):

    ```postgresql
    CREATE TABLE countries
    (
        id INT2 NOT NULL,
        name VARCHAR NOT NULL,
        area INTEGER NOT NULL,
        population INTEGER NOT NULL,
        source TEXT
    );
    ```

2. **Manually** create a query or a series of queries that would fill the table with the information above. Put the query/queries below:

    ```postgresql
    INSERT INTO countries (id, name, area, population, source) VALUES
        (18, 'India', 3287240, 1348834400, 'Based on 2011 census'),
        (27, 'Bangladesh', 143998, 166774136, DEFAULT),
        (34, 'Pakistan', 803940, 205095217, 'Official population clock'),
        (42, 'Nigeria', 923768, 20096000, 'UN projection'),
        (46, 'United States', 9833517, 329424894, 'Official population clock'),
        (54, 'Brazil', 8515767, 210076263, DEFAULT),
        (59, 'China', 9640821, 1397906480, 'Official estimate'),
        (60, 'Indonesia', 1904569, 268074600, 'Official annual projection');
    ```

3. Create a query that would return everything from the table:

    ```postgresql
    SELECT * FROM countries;
    ```

4. Create a query that would return a single row: the country with the ID of 46.

    ```postgresql
    SELECT * FROM countries WHERE id = 46 LIMIT 1;
    ```

5. Create a query that would return the four countries with the following IDs: 18, 34, 54, 59.

    ```postgresql
    SELECT * FROM countries WHERE id IN (18, 34, 54, 59);
    ```

6. Create a query that would return all the countries except the country with the ID of 27 (`Bangladesh`).

    ```postgresql
    SELECT * FROM countries WHERE NOT id = 27;
    ```

7. Create a query that would select the names and sources for the countries whose area is over 1,000,000 km<sup>2</sup>:

    ```postgresql
    SELECT name, source FROM countries WHERE area > 1000000;
    ```
    
8. Create a query that would select the IDs of the countries with missing sources:

    ```postgresql
    SELECT id FROM countries WHERE source IS NULL;
    ```
    
9. Create a query that would return the area, population, and population density (a computed column aliased `density`) of every country that has a source.

    ```postgresql
    SELECT area, population, (population / area) AS density FROM countries WHERE source IS NOT NULL;
    ```
    
10. Create a query that would return the list of all sources, without repetition:

    ```postgresql
    SELECT DISTINCT source FROM countries WHERE source IS NOT NULL;
    ```

11. Create a query that would select the countries whose source is official (starting with `Official`) or the area is below 1,000,000 km<sup>2</sup>:

    ```postgresql
    SELECT * FROM countries WHERE source LIKE 'Official%' OR area < 1000000;
    ```

12. Create a query that would select the countries whose source is official (starting with `Official`) and the area is below 1,000,000 km<sup>2</sup>:

    ```postgresql
    SELECT * FROM countries WHERE source LIKE 'Official%' AND area < 1000000;
    ```
    
13. Create a query that would select all the countries except those whose source is official (starting with `Official`):

    ```postgresql
    SELECT * FROM countries WHERE source NOT LIKE 'Official%' OR source IS NULL;
    ```
    
14. Create a query that would select the countries whose names start with an `N`, `O`, `P`, ..., `X`, `Y`, or `Z`:

    ```postgresql
    SELECT * FROM countries WHERE name ~ '^[N-Z]';
    ```
    
15. Create a query that would return all the countries sorted by their name alphabetically:

    ```postgresql
    SELECT * FROM countries ORDER BY name ASC;
    ```

16. Create a query that would return the population _density_ figures of the countries sorted in the descending order. The column should be aliased `density`.

    ```postgresql
    SELECT (population / area) AS density FROM countries ORDER BY density DESC;
    ```

17. Create a query that would return the countries sorted by their source alphabetically, and then (if two or more countries share the same source) by their name in the reverse alphabetical order:

    ```postgresql
    SELECT * FROM countries ORDER BY source ASC, name DESC;
    ```
    
18. Set all sources to `NULL`:

    ```postgresql
    UPDATE countries SET source = DEFAULT;
    ```
    
19. Update the sources for the countries with the population over 1,000,000,000 to `Official`:

    ```postgresql
    UPDATE countries SET source = 'Official' WHERE population > 1000000000;
    ```
    
20. Multiply the area by 100 and add 10 to the population for every country whose ID is greater than 50:

    ```postgresql
    UPDATE countries SET (area, population) = (area * 100, population + 10) WHERE id > 50;
    ```

21. Delete from the table every country whose population is less than 300,000,000:

    ```postgresql
    DELETE FROM countries WHERE population < 300000000;
    ```

22. Delete all countries from the table:

    ```postgresql
    TRUNCATE countries;
    ```
    
Don’t forget to create a pull request.
