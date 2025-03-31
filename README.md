<details>
  <summary>SPOILER WARNING! HOW I WENT THROUGH AND SOLVED THE <a href="https://mystery.knightlab.com">SQL MURDER MYSTERY</a></summary>

# SQL Murder Mystery Solution

A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a **murder** that occurred sometime on **Jan.15, 2018** and that it took place in **SQL City**. Start by retrieving the corresponding crime scene report from the police department’s database.

---

### Viewing the Murder Record
```sql
Select * from 'crime_scene_report'
where date='20180115' and type='murder' and city='SQL City'
```
![Crime Scene Report](Images/Pasted image 250331100113.png)

---

### Finding the First Witness
```sql
select * from 'person'
where address_street_name='Northwestern Dr'
order by address_number DESC
limit 1
```
![First Witness](Images/Pasted image 250331100242.png)

---

### First Witness Interview
```sql
select * from 'interview' 
where person_id=14887
```
![First Witness Statement](Images/Pasted image 250331100403.png)

---

### Searching for Get Fit Now Gym Members
```sql
select * from 'get_fit_now_member'
where membership_status='gold' and INSTR(id, '48Z')
```
![Gym Members](Images/Pasted image 250331100659.png)

---

### Checking Alibis (Gym Check-ins)
```sql
select * from 'get_fit_now_check_in'
where INSTR(membership_id, '48Z')
```
![Gym Check-ins](Images/Pasted image 250331101414.png)

```sql
select * from 'person'
where name in ('Joe Germuska','Jeremy Bowers')
```
![Suspects](Images/Pasted image 250331102629.png)

```sql
select * from 'facebook_event_checkin'
where person_id in (28819, 67318)
```
![Facebook Check-in](Images/Pasted image 250331102744.png)  
*Jeremy Bowers has a check-in on the night of the crime.*

---

### Checking Car Registrations
```sql
select * from 'drivers_license'
where instr(plate_number, 'H42W')
```
![Car Registrations](Images/Pasted image 250331103032.png)  
*The second record belongs to Jeremy Bowers.*

---

### Verifying Suspects' Income
```sql
select * from 'income'
where ssn in (138909730, 871539279)
```
![Income Records](Images/Pasted image 250331103402.png)  
*No income record for Joe Germuska.*

---

### Jeremy Bowers' Interview
```sql
select * from 'interview'
where person_id=67318
```
![Jeremy's Statement](Images/Pasted image 250331103821.png)  
*He claims the car and bag were his but denies committing the crime.*

---

### Finding the Woman Described
```sql
select * from 'drivers_license'
where (height between 65 and 67) and hair_color='red' and gender='female' and car_make='Tesla'
```
![Female Suspect](Images/Pasted image 250331105838.png)

---

### Checking Concert Attendees (3+ Visits in December)
```sql
select person_id, count(*) as visits from 'facebook_event_checkin'
where event_name='SQL Symphony Concert' and instr(date, '201712') 
group by person_id having visits > 2
```
![Concert Visits](Images/Pasted image 250331105047.png)

```sql
select * from 'person'
where id in (24556,99716)
```
![Concert Attendees](Images/Pasted image 250331105036.png)

---

### Verifying Miranda Priestly's Details
```sql
select * from 'income'
where ssn=987756388
```
![Miranda's Income](Images/Pasted image 250331105335.png)  
*She is wealthy* ✅

```sql
select * from 'drivers_license'
where id=202298
```
![Miranda's License](Images/Pasted image 250331110050.png)  
*She drives a Tesla Model S and matches the height* ✅  
![Concert Visits](Images/Pasted image 250331105047.png)  
*She attended the concert 3 times* ✅

---

### Second Witness: Annabel
```sql
select * from 'person'
where instr(name, 'Annabel') and address_street_name='Franklin Ave'
```
![Annabel](Images/Pasted image 250331111003.png)

```sql
select * from 'interview'
where person_id=16371
```
![Annabel's Statement](Images/Pasted image 250331111054.png)

---

### Checking Gym Check-ins (Jan 9, 2018)
```sql
select * from 'get_fit_now_check_in'
where check_in_date='20180109'
```
![Gym Check-ins](Images/Pasted image 250331111416.png)  
*Both Joe Germuska and Jeremy Bowers were present.*

---

### Final Conclusion: Miranda Priestly hired Jeremy Bowers to commit the murder.
![Solution](Images/Pasted image 250331112037.png)


</details>
