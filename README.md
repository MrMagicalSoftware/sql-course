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

Questo mi restituisce un errore :<br>



![Schermata 2023-04-11 alle 11 26 21](https://user-images.githubusercontent.com/98833112/231116813-9cd49ae2-7aee-4c3c-bf04-f45ea6892540.png)



TIPS : backtic OPTION + 9


```
SELECT SaleDate, Amount, Boxes, weekday(SaleDate) as 'w'
FROM sales
where weekday(SaleDate) = 4
```


# More Example TABLES


```
select * from people;

```


```
select * from people where team='Delish' or team='Jucies';

```

# in clause

Posso usare in clause che mi riduce la scrittura dell'or

```
select * from people where team in ('Delish', 'Jucies');

```


# Pattern Matching :


```
select * from people where salesperson like 'B%'

```

Contiene una lettera B


```
select * from people where salesperson like '%B%'

```


# Case Operator 

```
select SaleDate, Amount ,
     case when amount < 1000 then 'Under 1k'
          when amount < 5000 then 'Under 5k'
          when amount < 10000 then 'under 10k'
         
          else  '10k or more'
     end as 'Amount Category'
 
from sales;
```




# Joins SQL 


```

select s.saleDate , s.amount, p.Salesperson
from sales s 
join people p on p.SPID = s.SPID

```


In SQL, il left join è un tipo di join che restituisce tutte le righe della tabella di sinistra (left table) e le righe corrispondenti della tabella di destra (right table). Se non ci sono corrispondenze nella tabella di destra, i valori dei campi di quella tabella saranno NULL nella riga risultante.

La sintassi di un left join è la seguente:

SELECT colonna1, colonna2, ...
FROM tabella_sinistra
LEFT JOIN tabella_destra
ON condizione_di_corrispondenza;

La condizione di corrispondenza è solitamente un'espressione booleana che stabilisce come le righe delle due tabelle devono essere abbinati.


Supponiamo di avere due tabelle:


<pre>
Employee:
+----+------+-------+
| ID | Name | DepId |
+----+------+-------+
| 1  | John | 1     |
| 2  | Bob  | 2     |
| 3  | Jane | NULL  |
+----+------+-------+

Department:
+-------+------------+
| DepId | DepName    |
+-------+------------+
| 1     | IT         |
| 2     | Marketing  |
| 3     | HR         |
+-------+------------+

</pre>





Se volessimo ottenere tutti i dipendenti e il nome del loro dipartimento, incluso quelli che non appartengono ad alcun dipartimento, potremmo usare un left join:

```
SELECT Employee.Name, Department.DepName
FROM Employee
LEFT JOIN Department
ON Employee.DepId = Department.DepId;
```


Il risultato sarebbe:

<pre>

+------+------------+
| Name | DepName    |
+------+------------+
| John | IT         |
| Bob  | Marketing |
| Jane | NULL       |
+------+------------+


</pre>

Come si può vedere, l'ultimo dipendente Jane non ha un valore nella colonna DepName perché non appartiene a un dipartimento.


# Left join Example 


```

select s.saleDate, s.amount, pr.Product
from sales s
left join products pr on pr.pid = s.pid

```


# Multiple Join
```
select s.saleDate, s.amount, p.Salesperson ,p.team
from sales s
join people p on p.SPID = s.SPID
join products pr on pr.PID = s.SPID
```


# Conditions with Joins

```
select s.saleDate, s.amount, p.Salesperson ,p.team
from sales s
join people p on p.SPID = s.SPID
join products pr on pr.PID = s.SPID
where s.amount < 500 and p.Team='Delish';
```

```
select s.saleDate, s.amount, p.Salesperson ,p.team
from sales s
join people p on p.SPID = s.SPID
join products pr on pr.PID = s.SPID
where s.amount < 500 and p.Team='';
```


```
select s.saleDate, s.amount, p.Salesperson ,p.team
from sales s
join people p on p.SPID = s.SPID
join products pr on pr.PID = s.SPID
joint geo g on g.geoid = s.geoid
where s.amount < 500 and p.Team='' and g.geo in ('New Zealand' ,'India')
order by saleDate;
```


# Using group by

```
select geoID , sum(amount)
from sales
group by geoID

```



![Schermata 2023-04-11 alle 13 16 24](https://user-images.githubusercontent.com/98833112/231144566-2cc444ac-6a31-44be-8a02-d3362b277e16.png)


La clausola GROUP BY in SQL viene utilizzata per raggruppare le righe di una tabella in base ai valori in una o più colonne. In altre parole, viene usata per creare un insieme di risultati unico per ogni combinazione di valori dell'attributo specificato nella clausola.

La sintassi di base della clausola GROUP BY è la seguente:

<pre>
SELECT colonna1, colonna2, aggregazione(colonnaN)
FROM nome_tabella
GROUP BY colonna1, colonna2
</pre>

Dove:

    colonna1, colonna2, …, colonnaN sono le colonne che vogliamo usare per raggruppare i dati.
    aggregazione(colonnaN) è un'operazione aggregata, come COUNT, SUM, AVG, MIN e MAX, che viene applicata alla colonna in questione.

Ad esempio, se abbiamo una tabella clienti con i campi id, nome, cognome e paese, e vogliamo contare il numero di clienti per ogni paese, possiamo utilizzare la clausola GROUP BY in questo modo:

<pre>

SELECT paese, COUNT(*) as numero_clienti
FROM clienti
GROUP BY paese
</pre>


Il comando qui sopra ci darà i risultati sotto forma di gruppi di paesi e il numero di clienti di ogni paese.



# Example

```
select g.geo , sum(amount) , avg(amount) , sum(boxes)
from sales s
join geo g on s.geoID = g.geoID
group by g.geo

```

```
select pr.category , p.team , sum(boxes) , sum(amount)
from sales s
join people p on p.spid = s.spid
join products pr on p.pid = s.pid
where p.team <> ''
group by pr.category , p.team
order by  pr.category , p.team;

```




