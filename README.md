# -operador-IN-en-Oracle-SQL-
#### se utiliza para averiguar si el valor de un registro esta incluido en una lista de valores especificada en el momento de enviarle una consulta a una tabla en la bd

```sql
 create table medicamentos(
  codigo number(6) not null,
  nombre varchar2(20),
  laboratorio varchar2(20),
  precio number(6,2),
  cantidad number(4),
  fechavencimiento date not null,
  primary key(codigo)
 );

 insert into medicamentos
  values(102,'Sertal','Roche',5.2,10,to_date('01/02/2020','dd/mm/yyyy'));
 insert into medicamentos 
  values(120,'Buscapina','Roche',4.10,200,to_date('01/12/2017','dd/mm/yyyy'));
 insert into medicamentos 
  values(230,'Amoxidal 500','Bayer',15.60,100,to_date('28/12/2017','dd/mm/yyyy'));
 insert into medicamentos
  values(250,'Paracetamol 500','Bago',1.90,20,to_date('01/02/2018','dd/mm/yyyy'));
 insert into medicamentos 
  values(350,'Bayaspirina','Bayer',2.10,150,to_date('01/12/2019','dd/mm/yyyy'));
 insert into medicamentos 
  values(456,'Amoxidal jarabe','Bayer',5.10,250,to_date('01/10/2020','dd/mm/yyyy'));
  ```
  
  >select * from medicamentos

 | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
 | 102 | Sertal |  Roche   | 5.2   | 10 | 01/02/2020|
 | 120 | Buscapina |  Roche   | 4.10   | 200 | 01/12/2017|
 | 230 | Amoxidal 500 |  Bayer   | 15.60   | 100 | 28/12/2017|
 | 250 | Paracetamol 500 |  Bago   | 1.90   | 20 | 01/02/2018| 
 | 350 | Bayaspirina |  Bayer   | 2.10   | 150 | 01/12/2019| 
 | 456 | Amoxidal jarabe |  Bayer   | 5.10   | 250 | 01/10/2020| 
 
 
 
 ```sql
 select * from medicamentos where laboratorio in ('Bayer', 'Bago');
 ```
 | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
  | 230 | Amoxidal 500 |  Bayer   | 15.60   | 100 | 28/12/2017|
 | 250 | Paracetamol 500 |  Bago   | 1.90   | 20 | 01/02/2018| 
 | 350 | Bayaspirina |  Bayer   | 2.10   | 150 | 01/12/2019| 
 | 456 | Amoxidal jarabe |  Bayer   | 5.10   | 250 | 01/10/2020| 
 
 
 > para excluir utilizamos el operador NOT IN
 
 ```sql
 select * from medicamentos where laboratorio not in ('Bayer', 'Bago');
 ```
  | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
 | 102 | Sertal |  Roche   | 5.2   | 10 | 01/02/2020|
 | 120 | Buscapina |  Roche   | 4.10   | 200 | 01/12/2017|
 
 
 #### la clausula IN tiene mucha similitud con la clausula between
 
```sql
select * from medicamentos where cantidad between 10 and 200 ;
```

 | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
  | 102 | Sertal |  Roche   | 5.2   | 10 | 01/02/2020|
 | 120 | Buscapina |  Roche   | 4.10   | 200 | 01/12/2017|
 | 230 | Amoxidal 500 |  Bayer   | 15.60   | 100 | 28/12/2017|
 | 250 | Paracetamol 500 |  Bago   | 1.90   | 20 | 01/02/2018| 
 | 350 | Bayaspirina |  Bayer   | 2.10   | 150 | 01/12/2019| 
 
 
 ```sql
select * from medicamentos where cantidad in( 10 , 200) ;
-- la clausula in solo nos trae los dos registros ya solo dos cumplen la condicion
```
 | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
 | 102 | Sertal |  Roche   | 5.2   | 10 | 01/02/2020|
 | 120 | Buscapina |  Roche   | 4.10   | 200 | 01/12/2017|
 
 ####Fechas de vencimiento
 ```sql
 select * from medicamentos where extract(year from fechavencimiento)  in (2019,2020);
 --- la clausula extract extrae el año desde el campo fecha vencimiento
 ```
 | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
 | 102 | Sertal |  Roche   | 5.2   | 10 | 01/02/2020|
 | 350 | Bayaspirina |  Bayer   | 2.10   | 150 | 01/12/2019| 
 | 456 | Amoxidal jarabe |  Bayer   | 5.10   | 250 | 01/10/2020| 
 
  ```sql
 select * from medicamentos where extract(month from fechavencimiento)  in (12, 10);
 --- la clausula extract extrae el mes desde el campo fecha vencimiento
 ```
 | codigo            | nombre           |   laboratorio   |  precio   |  cantidad   |  fechavencimiento  |
 | ------------------|:----------------:|----------------:| ---------:| -----------:| ------------------:|
 | 120 | Buscapina |  Roche   | 4.10   | 200 | 01/12/2017|
 | 230 | Amoxidal 500 |  Bayer   | 15.60   | 100 | 28/12/2017|
 | 350 | Bayaspirina |  Bayer   | 2.10   | 150 | 01/12/2019| 
 | 456 | Amoxidal jarabe |  Bayer   | 5.10   | 250 | 01/10/2020| 
