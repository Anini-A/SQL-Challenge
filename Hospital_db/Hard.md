## Database: Hospital

<img width="632" alt="Screenshot 2023-03-31 at 10 17 40 PM" src="https://user-images.githubusercontent.com/25376135/229263328-e4519a02-dbc0-43ab-b38c-8088f76cdbfe.png">

### Difficulty level: Hard 🔴

#### Question 1
Show all of the patients grouped into weight groups.
Show the total amount of patients in each weight group.
Order the list by the weight group decending.

For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.
   ```
select
  count (patient_id) as patient_in_group,
  floor (weight / 10) * 10 as weight_group
from patients
group by weight_group
order by weight_group desc;
  ```

#### Question 2
Show patient_id, weight, height, isObese from the patients table.
Display isObese as a boolean 0 or 1.
Obese is defined as weight(kg)/(height(m)2) >= 30.
weight is in units kg.
height is in units cm.
   ```
select
  patient_id,
  weight,
  height,
  CASE
    WHEN weight / POWER((height / 100.0), 2) >= 30 THEN 1
    ELSE 0
  END isObese
from patients
  ```
  
#### Question 3
Show patient_id, first_name, last_name, and attending doctor's specialty.
Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'

Check patients, admissions, and doctors tables for required information.
   ```
SELECT
  p.patient_id,
  p.first_name,
  p.last_name,
  d.specialty
FROM patients p
  JOIN admissions a ON p.patient_id = a.patient_id
  JOIN doctors d ON a.attending_doctor_id = d.doctor_id
WHERE
  a.diagnosis = 'Epilepsy'
  AND d.first_name = 'Lisa';
  ```
  
#### Question 4
All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.

The password must be the following, in order:
1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date
   ```
SELECT
  patient_id,
  CONCAT(
    patient_id,
    LENGTH(last_name),
    YEAR(birth_date)
  ) AS temp_password
FROM patients
WHERE patient_id IN (
    SELECT patient_id
    FROM admissions
  );
  ```
   
#### Question 5
Each admission costs $50 for patients without insurance, and $10 for patients with insurance. All patients with an even patient_id have insurance.

Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the admission_total cost for each has_insurance group.
   
   ```
SELECT
  CASE
    WHEN patient_id % 2 = 0 THEN 'Yes'
    ELSE 'No'
  END AS has_insurance,
  SUM(
    CASE
      WHEN patient_id % 2 = 0 THEN 10
      ELSE 50
    END
  ) AS admission_total
FROM admissions
GROUP BY has_insurance;
  ```
  
#### Question 6

xxxxxxxxxxxxxx

   ```

  ```

#### Question 7

xxxxxxxxxxxxxx

   ```

  ```

#### Question 8

xxxxxxxxxxxxxx

   ```

  ```
   
#### Question 9

xxxxxxxxxxxxxx

   ```

  ```
  
  
#### Question 10

xxxxxxxxxxxxxx

   ```

  ```
  
  
#### Question 11

xxxxxxxxxxxxxx

   ```

  ```
  
  
#### Question 12

xxxxxxxxxxxxxx

   ```

  ```
