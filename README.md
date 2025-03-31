<details>
  <summary>SPOILER WARNING! HOW I WENT THROUGH AND SOLVED THE <a href="https://mystery.knightlab.com">SQL MURDER MYSTERY</a></summary>
  
  
A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a **​murder​** that occurred sometime on ​**Jan.15, 2018​** and that it took place in ​**SQL City​**. Start by retrieving the corresponding crime scene report from the police department’s database.


#### Vendo o registro do assassinato criado
```sql
Select * from 'crime_scene_report'
where date='20180115' and type='murder' and city='SQL City'
```
![[Pasted image 20250331100113.png]]

#### Procurando a primeira testemunha
```sql
select * from 'person'
where address_street_name='Northwestern Dr'
order by address_number DESC
limit 1
```
![[Pasted image 20250331100242.png]]

#### Vendo o que a primeira testemunha disse
```sql
select * from 'interview' 
where person_id=14887
```
![[Pasted image 20250331100403.png]]

#### Procurando pessoas que possuem adesão ao Get Fit Now Gym
```sql
select * from 'get_fit_now_member'
where membership_status='gold' and INSTR(id, '48Z')
```
![[Pasted image 20250331100659.png]]

#### Vendo se qualquer um dos dois havia feito check-in no dia (ver se algum deles tinha um alibi)
```sql
select * from 'get_fit_now_check_in'
where INSTR(membership_id, '48Z')
```
![[Pasted image 20250331101414.png]]

```sql
select * from 'person'
where name in ('Joe Germuska','Jeremy Bowers')
```
![[Pasted image 20250331102629.png]]

```sql
select * from 'facebook_event_checkin'
where person_id in (28819, 67318)
```
![[Pasted image 20250331102744.png]]
*Jeremy Bowers tem um check-in na noite do crime*

#### Verificando registro de carros por carteiras de habilitação
```sql
select * from 'drivers_license'
where instr(plate_number, 'H42W')
```
![[Pasted image 20250331103032.png]]
*O segundo registro é o de Jeremy Bowers*
#### Verificando renda dos suspeitos
```sql
select * from 'income'
where ssn in (138909730, 871539279)
```
![[Pasted image 20250331103402.png]]
*sem registro da renda de Joe Germuska*

#### Vendo se ocorreu interrogação com Jeremy Bowers
```sql
select * from 'interview'
where person_id=67318
```
![[Pasted image 20250331103821.png]]
*Ao que da a entender o carro realmente era dele e a bolsa também, mas ele não cometeu o crime*

#### Encontrando a mulher descrita
```sqlite
select * from 'drivers_license'
where (height between 65 and 67) and hair_color='red' and gender='female' and car_make='Tesla'
```
![[Pasted image 20250331105838.png]]

*Vendo quais pessoas visitaram o concerto 3 vezes em dezembro*
```sql
select person_id, count(*) as visits from 'facebook_event_checkin'
where event_name='SQL Symphony Concert' and instr(date, '201712') 
group by person_id having visits > 2
```
![[Pasted image 20250331105047.png]]

```sql
select * from 'person'
where id in (24556,99716)
```
![[Pasted image 20250331105036.png]]

#### Verificando se informações batem sobre Mirando Priestly
```sql
select * from 'income'
where ssn=987756388
```
![[Pasted image 20250331105335.png]]
*Ela possui muito dinheiro* ✅
```sql
select * from 'drivers_license'
where id=202298
```
![[Pasted image 20250331110050.png]]
*Ela dirige um Tesla Model S e tem a altura certa* ✅
![[Pasted image 20250331105047.png]]
*Ela foi ao concerto 3 vezes* ✅

#### Verificando a segunda testemunha
```sql
select * from 'person'
where instr(name, 'Annabel') and address_street_name='Franklin Ave'
```
![[Pasted image 20250331111003.png]]

#### Verificando o que Annabel disse no interrogatório
```sql
select * from 'interview'
where person_id=16371
```
![[Pasted image 20250331111054.png]]

#### Vendo quais pessoas treinaram na data de 9 de Janeiro de 2018
```sql
select * from 'get_fit_now_check_in'
where check_in_date='20180109'
```
![[Pasted image 20250331111416.png]]
*Ambos Joe Germuska quanto Jeremy Bowers possuem check-in no dia*

Evidencias apontam cada vez mais para Jeremy Bowers

### Solução final: Miranda Priestly contratou Jeremy Bowers para realizar o assassinato
![[Pasted image 20250331112037.png]]

</details>
