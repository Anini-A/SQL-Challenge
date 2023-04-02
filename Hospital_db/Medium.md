## Database: Hospital

<img width="632" alt="Screenshot 2023-03-31 at 10 17 40 PM" src="https://user-images.githubusercontent.com/25376135/229263328-e4519a02-dbc0-43ab-b38c-8088f76cdbfe.png">

### Difficulty level: Medium 🟡

#### Question 1
Show unique birth years from patients and order them by ascending.
   ```
select distinct(year(birth_date))
From patients
order by birth_date ASC
  ```

#### Question 2
Show unique first names from the patients table which only occurs once in the list.
For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.

   ```
select first_name
From patients
group by first_name
having count(first_name) = 1
  ```
  
#### Question 3
Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
   ```
SELECT
  patient_id,
  first_name
FROM patients
where first_name like 's%s' and len(first_name)>=6;
  ```
  
#### Question 4
Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.

Primary diagnosis is stored in the admissions table.
   ```
SELECT
  patients.patient_id,
  first_name,
  last_name
from patients
  inner Join admissions on admissions.patient_id = patients.patient_id
where diagnosis = 'Dementia'
  ```
   
#### Question 5
Display every patient's first_name.
Order the list by the length of each name and then by alphbetically
   ```
SELECT first_name
from patients
order by len(first_name), first_name ASC;
  ```
  
#### Question 6
Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.
   ```
SELECT
  SUM(gender = 'M') as Male,
  SUM(gender = 'F') as Female
from patients
  ```

#### Question 7
Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.
   ```
SELECT
  first_name,
  last_name,
  allergies
from patients
where
  allergies = 'Penicillin'
  or allergies = 'Morphine'
order by
  allergies,
  first_name,
  last_name
  ```

#### Question 8
Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.
   ```
SELECT
  patient_id,
  diagnosis
FROM admissions
GROUP BY
  patient_id,
  diagnosis
HAVING count(*) > 1
ORDER BY patient_id;
  ```
   
#### Question 9
Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.
   ```
SELECT
  city,
  count(*) as num_patients
from patients
group by city
order by
  num_patients desc,
  city asc
  ```
  
#### Question 10
Show first name, last name and role of every person that is either patient or doctor.
The roles are either "Patient" or "Doctor"
   ```
SELECT
  first_name,
  last_name,
  'Patient' as role
FROM patients
UNION all
SELECT
  first_name,
  last_name,
  'Doctor' as role
FROM doctors
  ```
  
#### Question 11
Show all allergies ordered by popularity. Remove NULL values from query.
   ```
SELECT
  allergies,
  count(allergies) as total_diagnosic
from patients
where allergies is not null
group by allergies
order by total_diagnosic desc
  ```
  
#### Question 12
Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.
   ```
SELECT
  first_name,
  last_name,
  birth_date
from patients
where year(birth_date) between 1970 and 1979
order by birth_date asc
  ```
  
#### Question 13
We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order
EX: SMITH,jane
```
SELECT
  concat(upper(last_name), ',', lower (first_name)) as Full_name
from patients
order by first_name desc
```

#### Question 14
Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.
```
SELECT
  province_id,
  SUM(height) as sum_height
from patients
group by province_id
having sum_height > 7000
```

#### Question 15
Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'
```
SELECT
  max(weight) - min(weight) as weight_delta
from patients
where last_name = 'Maroni'
```

#### Question 16
Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.
```
SELECT
  Day(admission_date) as date_number,
  count(admission_date) as number_of_admissions
from admissions
group by date_number
Order by number_of_admissions desc
```

#### Question 17
Show all columns for patient_id 542's most recent admission_date.
```
SELECT *
from admissions
where patient_id = 542
group by patient_id
having max(admission_date)
```

#### Question 18
Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:
1 patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
2 attending_doctor_id contains a 2 and the length of patient_id is 3 characters.
```
select
  patient_id,
  attending_doctor_id,
  diagnosis
FROM admissions
where
  (
    patient_id % 2 <> 0
    and attending_doctor_id in ('1', '5', '19')
  )
  Or (
    attending_doctor_id like '%2%'
    and len(patient_id) = 3
  )
```

#### Question 19
Show first_name, last_name, and the total number of admissions attended for each doctor.
Every admission has been attended by a doctor.
```
select
  first_name,
  last_name,
  count(attending_doctor_id) as admissions_total
FROM doctors
  JOIN admissions ON doctors.doctor_id = admissions.attending_doctor_id

group by
  first_name,
  last_name
```

#### Question 20
For each doctor, display their id, full name, and the first and last admission date they attended.
```
select
  doctor_id,
  concat(first_name, ' ', last_name) as full_name,
  min(admission_date) as first_admission_date,
  max (admission_date) as last_admission_date
FROM doctors
  join admissions on doctors.doctor_id = admissions.attending_doctor_id
group by doctor_id
```

#### Question 21
Display the total amount of patients for each province. Order by descending.
```
select
  count(patient_id) as total_patients,
  province_name
from patients
  join province_names on patients.province_id = province_names.province_id
group by province_name
order by total_patients desc
```

#### Question 22
For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.
```
select
  concat(
    patients.first_name,
    ' ',
    patients.last_name
  ) as patient_full_name,
  diagnosis,
  concat(
    doctors.first_name,
    ' ',
    doctors.last_name
  ) as doctor_full_name
from patients
  join admissions on patients.patient_id = admissions.patient_id
  join doctors on doctor_id = attending_doctor_id
```

#### Question 23
Display the number of duplicate patients based on their first_name and last_name.
```
select
  first_name,
  last_name,
  count(patient_id) as num_of_duplicate
FROM patients
group by
  first_name,
  last_name
having count(patient_id) > 1
```

#### Question 24
Display patient's full name,
height in the units feet rounded to 1 decimal,
weight in the unit pounds rounded to 0 decimals,
birth_date,
gender non abbreviated.

Convert CM to feet by dividing by 30.48.
Convert KG to pounds by multiplying by 2.205.
```
SELECT
  CONCAT(first_name, ' ', last_name) AS full_name,
  ROUND(height / 30.48, 1) AS height_feet,
  ROUND(weight * 2.205, 0) AS weight_pounds,
  birth_date,
  CASE gender
    WHEN 'M' THEN 'Male'
    WHEN 'F' THEN 'Female'
    ELSE 'Unknown'
  END AS gender
FROM patients;
```
