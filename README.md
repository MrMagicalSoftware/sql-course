# sql-course


Per visionare le tabelle è possibile usare il comando 

```
show tables;
```
![Schermata 2023-04-11 alle 10 54 45](https://user-images.githubusercontent.com/98833112/231108637-5e59552c-2448-4232-8afa-3181d7da7545.png)



Per visionare cosa è disponile in una particolare tabella si può usare :

```
 desc sales
```

![Schermata 2023-04-11 alle 10 56 30](https://user-images.githubusercontent.com/98833112/231109103-55590566-aa1d-4da3-8087-8291bfc3e4c8.png)



Comando di Select 

```
select * from sales
```
![Schermata 2023-04-11 alle 11 00 42](https://user-images.githubusercontent.com/98833112/231110460-147b3eee-82ce-4468-b260-a990834f9661.png)


tips :

Meglio scrivere select from sales,
e poi usare l'autocompletamento per farsi suggerire le colonne ecc..

```
select SaleDate,Amout from sales

```


# Sql Calculations :

Posso fare anche dei calcoli in sql , usando 

```
select SaleDate,Amout , Boxes , Amout/boxes from sales

```


![Schermata 2023-04-11 alle 11 06 18](https://user-images.githubusercontent.com/98833112/231111854-4a5efb7d-aac5-4808-9f73-80f7ba1219ab.png)


Se volessi dare un nome alla colonna ho 2 diverse alternative 


```
select SaleDate,Amout , Boxes , Amout/boxes as 'NomeColonna' from sales

```


```
select SaleDate,Amout , Boxes , Amout/boxes 'NomeColonna' from sales

```

# Clausula Where  Filtering:


```
select * from sales where amount > 10000

```


# Order by :

Posso usare come ulteriori opzioni desc oppure asc

```
select * from sales where amount > 10000 ordber by amount desc

```

```
select * from sales where amount > 10000 ordber by amount asc

```


