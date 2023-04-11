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


![Schermata 2023-04-11 alle 11 14 51](https://user-images.githubusercontent.com/98833112/231114065-aefdf1d4-91fa-4445-bd25-16fbb0f71f70.png)


# Clausula Where :


Per le date il formato di sql è YY-MM-DD

```
select * from sales where amount > 10000 and saleDate >= '2022-01-01'

```

Posso usare anche delle funzioni build in in sql che mi permettono ad esempio di estrarre
la data .

Es : la funzione year()

```
select * from sales where amount > 10000 and year(saleDate) = 2022 order by amount
```


# Between condition :


```
select * from sales where boxes > 0 and boxes <=50

```


```
select * from sales where boxes between 0 and 50
```

Questo mi restituisce un errore :
![Schermata 2023-04-11 alle 11 26 21](https://user-images.githubusercontent.com/98833112/231116813-9cd49ae2-7aee-4c3c-bf04-f45ea6892540.png)



TIPS : backtic OPTION + 9


```
SELECT SaleDate, Amount, Boxes, weekday(SaleDate) as 'w'
FROM sales
where weekday(SaleDate) = 4
```



