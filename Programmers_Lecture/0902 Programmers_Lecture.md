# ๊ฐ์ ์ ๋ฆฌ ๐
___

> 2021.09.02 SpringBoot Part1

## ๊ณต๋ถํ ๋ด์ฉ

- ### ๋ชจ๋  ๊ฒ์ ๊ณต์๋ฌธ์์ ํจ๊ป!!! ###

- ### SPA ###
    - Single-Page Application
    - ๋จ์ผ ํ์ด์ง ์น ์ดํ๋ฆฌ์ผ์ด์
        - ์ฌ์ฉ์ ์ธํฐ๋ ์์ ์ํด URL์ด ๋ณ๊ฒฝ ์ ํ๋ฉด ์ ์ฒด์ ๋ก๋๊ฐ ์์ด ํ๋ฉด์ ์ผ๋ถ๋ถ๋ง ๋์ ์ผ๋ก ๋ ๋๋งํ์ฌ ๋ฐ์คํฌํ ์ดํ๋ฆฌ์ผ์ด์๊ณผ ๋น์ทํ ์ ์ ๊ฒฝํ์ ์ ๊ณตํ๋ค.
        - AJAX๋ฅผ ์ด์ฉํด์ ๋๋ถ๋ถ์ ๋ฆฌ์์ค๋ค์ ์ดํ๋ฆฌ์ผ์ด์ ๋ก๋์ ํ๋ฒ ์ฝ๋๋ค.
        - JSON๊ณผ ๊ฐ์ ๋ฐ์ดํฐ๋ง ์ดํ๋ฆฌ์ผ์ด์ ์คํ์ค์ ์ฝ์ด์ค๊ณ  ๊ด๋ จ๋ ํ๋ฉด์ ์ฝ์ด์จ๋ค.
        - URL ๋ณ๊ฒฝ์ ํน์  ์์ญ๋ง ๋ ๋๋ง ๋๋ค. ์ฃผ๋ก ์ด๋ DOM ์กฐ์์ ํตํ์ฌ ๋ ๋๋ง์ด ์ด๋ฃจ์ด์ง๊ฒ ๋๋ค.
        1. ์๋ฒ์ฌ์ด๋ ๋ผ์ฐํ ์ฒ๋ฆฌ
            - ์์ฒญ๋ฐ๋ URL์ ๋ฐ๋ฅธ ๋ฆฌ์์ค๋ฅผ ๋ฐํ
            - ์ผ๋ฐ์ ์ธ ์น์ฌ์ดํธ์์ ์ฌ์ฉ์์ URL์ ํด๋นํ๋ ์น ํ์ด์ง๋ฅผ ๋ฐํํ๋ ํ์๋ก ๋ณผ ์ ์๋ค.

        2. ํด๋ผ์ด์ธํธ ๋ผ์ฐํ ์ฒ๋ฆฌ
            - SPA ํน์ฑ์ ํด๋ผ์ด์ธํธ์์ ๋์ ์ผ๋ก ๋ ๋๋งํ๊ธฐ๋๋ฌธ์ URL์ ๋ณํ์ ๋ฐ๋ผ ํ๋ฉด ์ํ๋ฅผ ๋ณ๊ฒฝ
            - HTML5 ํ์คํ ๋ฆฌ API๋ฅผ ์ด์ฉํ  ์ ์๋ค.
            - #(ํด์ฌ) ๋๋ $!(ํด์ฌ๋ฑ)์ฒ๋ฆฌ๋ฅผ ์ด์ฉํ  ์ ์๋ค.

- ### CORS ###
    - ๋ค์ํ ๋ฆฌ์์ค, ๋ค์ํ ํธ์คํธ์ ์ ๊ทผํ๋ ํ๊ฒฝ์ด๋ค. 
    - ์์์ ์ธ ์ ๊ทผ ๋ฐฉ์ง
    - ๋์ผํ ์ถ์ฒ๋ง ํ์ฉ (ํ๋กํ ์ฝ, ํฌํธ, ํธ์คํธ๊ฐ ๋ค๋ฅผ ๊ฒฝ์ฐ CORS ์ค๋ฅ๊ฐ ๋ฐ์ํ๋ค.)
    - ์๋น ์์ฒญ(pre flight)์ด ๋ณด๋ด๋ / ์๋ณด๋ด๋์ ๊ฒฝ์ฐ์ ๋ฐ๋ผ ๋๋์ด์ง๋ค.
    
    - ๋จ์ ์์ฒญ์ ์๋น ์์ฒญ์ ๋ณด๋ด์ง ์๊ณ  ๋ฐ๋ก ๋ณธ์์ฒญ๋ง ๋ณด๋ธ๋ค.
    - ์ปจํธ๋กค๋ฌ ๊ธฐ๋ฐ ํน์ ์ ์ญ๊ธฐ๋ฐ์ผ๋ก ์ค์ ์ ํตํด ํด๊ฒฐํ  ์ ์๋ค.

    - ### ๋ฆฌ์กํธ์ ์ฐ๋ํ๋ ์ค์ต ์ค์ (CORS๋ฅผ ์ค์ ์ผ๋ก) ###

### (์ถ๊ฐ) validation์ ์ํฐํฐ์ ์๋ ๊ฒ์ด ์ข๋ค. ###
            