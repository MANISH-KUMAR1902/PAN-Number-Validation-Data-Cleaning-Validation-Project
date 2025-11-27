# PAN-Number-Validation-Data-Cleaning-Validation-Project
This project focuses on cleaning, validating, and categorizing PAN (Permanent Account Number) data according to the official Indian PAN format. The objective is to ensure data quality by detecting incorrect, malformed, or incomplete PAN entries within a dataset.

-- 1. Identify and handle missing data
select * from pan_card where pan_numbers is null; 


-- 2. Check for duplicates
select pan_numbers, count(1) 
from pan_card 
where pan_numbers is not null
group by pan_numbers
having count(1) > 1; 

select distinct * from pan_card;


-- 3. Handle leading/trailing spaces
select *
from pan_card 
where pan_numbers <> trim(pan_numbers)


-- 4. Correct letter case
select *
from pan_card 
where pan_numbers <> upper(pan_numbers)

select * from pan_card
-- New cleaned table:
create table pan_card_cleaned
as
select distinct upper(trim(pan_numbers)) as pan_numbers
from pan_card
where pan_numbers is not null
and TRIM(pan_numbers) <> ''

select * from pan_card_cleaned
