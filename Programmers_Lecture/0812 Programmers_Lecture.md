# ๊ฐ์ ์ ๋ฆฌ ๐
___

> 2021.08.12 ์ค๋ฆฌ์ฝ๋ฐธ๋ฆฌ์์ ๋ ์์จ ๋ฐ์ดํฐ๋ฒ ์ด์ค(3)

## ๊ณต๋ถํ ๋ด์ฉ

- ### INSERT / UPDATE / DELETE ์ค๋ช ###
    - MySQL์์ ์ง์ํ๋ ์ปฌ๋ผ ํ์
        - Numeric Type
            - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT
            - DECIMAL, NUMERIC
            - FLAOT, DOUBLE, BIT
        - Date and Time Type
            - DATE, DATETIME, TIMESTAMP, TIME, YEAR
        - String Type
            - CHAR, VARCHAR, BINARY, VARBINARY, BLOB, TEXT, ENUM, SET
        - JSON Type
            - ๋ค์ํ JSON ์กฐ์ํจ์๋ฅผ ์ ๊ณตํจ
        - Spatial Type
            - ์์น ๊ด๋ จ ํ์

    - TIP
        - ๋๊ณผ ๊ด๋ จํด์๋ DECIMAL ํ์์, ์์์  ์ดํ ์ ๊ฒฝ์ ์ฐ์ง ์์ ๋๋ DECIMAL, NUMERIC
        - FLOAT๊ณผ DOUBLE์ ์ฐจ์ด
            - DOUBLE ํ์์ precision์ด ๋ ์ข๋ค. ๋ ์ํํ์ด ๊ฐ๋ฅํ๋ค. ํ์ง๋ง, storage๊ฐ ๋ ์ฐจ์งํ๋ค. 
            - FLOAT์ ๋ฐ๋๋ก storage๊ฐ ๋ ์ฐจ์งํ๋ค.

        - VARCHAR vs CHAR
            - CHAR : ๊ณ ์ ๋ ๊ธธ์ด
            - ๋ ๋ค ํ์คํธ ๊ธธ์ด์ ์ ํ์ด ์๊ธฐ ๋๋ฌธ์ ๊ธด ํ์คํธ์ผ ๊ฒฝ์ฐ TEXT ํ์์ ์จ์ผํ๋ค.

    - INSERT
        - EX)
            - INSERT INTO prod.vital(user_id, vital_id, date, weight) VALUES(100, 1, '2020-01-01', 75);
            - INSERT INTO prod.alert VALUES(1, 4, 'WeightIncrease', '2020-01-02', 101);

    - DELETE
        - EX)
            - DELETE FROM prod.vital WHERE weight <= 0;
        - DELETE vs TRUNCATE
            - DELETE๋ WHERE ์กฐ๊ฑด๋ฌธ์ ์ฌ์ฉํ  ์ ์๋ค. ๋์  ์๋๊ฐ ๋๋ฆฌ๋ค.
            - TRUNCATE๋ WHERE ์กฐ๊ฑด๋ฌธ์ ์ฌ์ฉํ  ์ ์๋ค. ๋์  ์๋๊ฐ ๋น ๋ฅด๋ค. ๋ํ ํธ๋์ ์ ์ฌ์ฉ์ ๋กค๋ฐฑ์ด ๋ถ๊ฐ๋ฅํ๋ค.

    - UPDATE
        - EX)
            - UPDATE prod.vital SET weight = 92 WHERE vital_id = 4;


- ### INSERT/ UPDATE / DELETE ์ค์ต ###
    - MySQL Workbench๋ก ์ค์ต

- ### ๋ค์ํ JOIN ์ดํด๋ณด๊ธฐ
    - JOIN์ด๋?
        - SQL ์กฐ์ธ์ ๋ ๊ฐ ์ด์์ ํ์ด๋ธ๋ค์ ๊ณตํต ํ๋๋ฅผ ๊ฐ์ง๊ณ  ํตํฉ
        - JOIN์ ๊ฒฐ๊ณผ๋ก ์์ชฝ์ ํ๋๋ฅผ ๋ชจ๋ ๊ฐ์ง ์๋ก์ด ํ์ด๋ธ์ด ๋ง๋ค์ด์ง.

        ![image](https://user-images.githubusercontent.com/73347933/129161279-5743ebec-22af-485a-8f74-cc52507d948e.png)


    - JOIN ๋ฌธ๋ฒ
        - MySQL์ FULL ์กฐ์ธ์ ์ง์ํ์ง ์๋๋ค.
        - SELECT A.*, B.* FROM raw_data.table1 A ____ JOIN raw_data.table2 B ON A. key1 = B.key1 and A.key2 = B.key2 WHERE A.ts >= '2019-01-01';

    - JOIN์ ๊ณ ๋ คํด์ผํ  ์ 
        - ์ค๋ณต ๋ ์ฝ๋๊ฐ ์๊ณ  PK์ ์ ์ผ์ฑ์ด ๋ณด์ฅ๋๋ ์ง๋ฅผ ์ฒดํฌ
        - ์กฐ์ธํ๋ ํ์ด๋ธ๋ค๊ฐ์ ๊ด๊ณ๋ฅผ ๋ชํํ๊ฒ ์ ์ -> ์ด๋ ํ์ด๋ธ์ FROM ์ ์ ์ฌ์ฉํ ์ง ๊ฒฐ์ 
    
    - JOIN ์ค๋ช
        - INNER JOIN
            - ์์ชฝ ํ์ด๋ธ์์ ๋งค์น๊ฐ ๋๋ ๋ ์ฝ๋๋ง ๋ฆฌํดํจ
            - ์์ชฝ ํ์ด๋ธ์ ํ๋๊ฐ ๋ชจ๋ ์ฑ์์ง ์ํ๋ก ๋ฆฌํด๋๋ค.
        - LEFT JOIN
            - ์ผ์ชฝ ํ์ด๋ธ(BASE)(FROM ์ ์ ์ฌ์ฉ)์ ๋ชจ๋  ๋ ์ฝ๋๋ค์ ๋ฆฌํดํจ
            - ์ค๋ฅธ์ชฝ ํ์ด๋ธ์ ํ๋๋ ์ผ์ชฝ ํ์ด๋ธ์ ๋ ์ฝ๋์ ์ผ์นํ๋ ๊ฒฝ์ฐ์๋ง ์ฑ์์ง๊ณ  ๋๋จธ์ง๋ NULL๋ก ๋ฆฌํด๋๋ค.
        - FULL JOIN
            - ์ผ์ชฝ ํ์ด๋ธ๊ณผ ์ค๋ฅธ์ชฝ ํ์ด๋ธ์ ๋ชจ๋  ๋ ์ฝ๋๋ค์ ๋ฆฌํดํจ
            - ๋งค์นญ๋๋ ๊ฒฝ์ฐ์๋ง ์ฑ์์ง๊ณ  ๋๋จธ์ง๋ NULL๋ก ๋ฆฌํดํจ
        - CROSS JOIN
            - ์ผ์ชฝ ํ์ด๋ธ๊ณผ ์ค๋ฅธ์ชฝ ํ์ด๋ธ์ ๋ ์ฝ๋์ ๋ชจ๋  ์กฐํฉ์ ๋ฆฌํดํจ
        - SELF JOIN
            - ๋์ผํ ํ์ด๋ธ์ ALIAS๋ฅผ ๋ค๋ฅด๊ฒ ํด์ ์๊ธฐ ์์ ๊ณผ ์กฐ์ธํจ


- ### JOIN ์ค์ต ###
    - MySQL workbench๋ก ์ค์ต