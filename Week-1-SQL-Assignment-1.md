## Deloitte Associate Analyst Weekly Assignement #1
*1. Write a query which will display the customer id, account type they hold, their account number and bank name.*
```sql
SELECT CUSTOMER_ID, ACCOUNT_TYPE, ACCOUNT_NO, BANK_NAME 
FROM ACCOUNT_INFO  
INNER JOIN  BANK_INFO  ON 
ACCOUNT_INFO.IFSC_CODE = BANK_INFO.IFSC_CODE;
```
**OUTPUT**

    | CUSTOMER_ID | ACCOUNT_TYPE |       ACCOUNT_NO | BANK_NAME |
    |-------------|--------------|------------------|-----------|
    |       C-001 |      SAVINGS | 1234567898765432 |      HDFC |
    |       C-002 |       SALARY | 1234567898765433 |       SBI |
    |       C-003 |      SAVINGS | 1234567898765434 |     ICICI |
    |       C-004 |       SALARY | 1234567898765435 |      HDFC |
    |       C-005 |      SAVINGS | 1234567898765436 |       SBI |
-----------------------------------------------------------------------------------
*2. Write a query which will display the customer id, account type and the account number of HDFC customers who registered after 12-JAN-2012 and before 04-APR-2012.*
```sql
SELECT CUSTOMER_ID, ACCOUNT_TYPE, ACCOUNT_NO
FROM ACCOUNT_INFO
INNER JOIN BANK_INFO
ON ACCOUNT_INFO.IFSC_CODE = BANK_INFO.IFSC_CODE
WHERE REGISTRATION_DATE BETWEEN '2012-01-13' AND '2012-04-03' 
AND BANK_NAME='HDFC';
 ```
-----------------------------------------------------------------------------------
*3. Write a query which will display the customer id, customer name, account no, account type and bank name where the customers hold the account.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
ACCOUNT_INFO.ACCOUNT_NO, 
ACCOUNT_INFO.ACCOUNT_TYPE, BANK_INFO.BANK_NAME
FROM BANK_INFO
INNER JOIN ACCOUNT_INFO AI
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE
INNER JOIN CUSTOMER_PERSONAL_INFO CPI
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID=ACCOUNT_INFO.CUSTOMER_ID
WHERE ACCOUNT_INFO.ACCOUNT_NO IS NOT NULL;
```
**OUTPUT**

    | CUSTOMER_ID | ACCOUNT_TYPE |       ACCOUNT_NO |
    |-------------|--------------|------------------|
    |       C-001 |      SAVINGS | 1234567898765432 |
-----------------------------------------------------------------------------------
*4.Write a query which will display the customer id, customer name, gender, marital status along with the unique reference string*
```sql
SELECT CUSTOMER_ID, CUSTOMER_NAME, GENDER, MARITAL_STATUS,
CONCAT(CUSTOMER_NAME,'_',GENDER,'_',MARITAL_STATUS) 
AS UNIQUE_REF_STRING
FROM CUSTOMER_PERSONAL_INFO; 
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME | GENDER | MARITAL_STATUS | UNIQUE_REF_STRING |
    |-------------|---------------|--------|----------------|-------------------|
    |       C-001 |          JOHN |      M |         SINGLE |     JOHN_M_SINGLE |
    |       C-002 |         JAMES |      M |        MARRIED |   JAMES_M_MARRIED |
    |       C-003 |       SUNITHA |      F |         SINGLE |  SUNITHA_F_SINGLE |
    |       C-004 |        RAMESH |      M |        MARRIED |  RAMESH_M_MARRIED |
    |       C-005 |         KUMAR |      M |         SINGLE |    KUMAR_M_SINGLE |
-----------------------------------------------------------------------------------
*5. Write a query which will display the account number, customer id, registration date, initial deposit amount of the customer whose initial deposit amount is within the range of Rs.15000 to Rs.25000.*
```sql
SELECT ACCOUNT_NO, CUSTOMER_ID, REGISTRATION_DATE, 
INITIAL_DEPOSIT
FROM ACCOUNT_INFO
WHERE INITIAL_DEPOSIT BETWEEN 15000 AND 25000;
```
**OUTPUT**

    |       ACCOUNT_NO | CUSTOMER_ID | REGISTRATION_DATE | INITIAL_DEPOSIT |
    |------------------|-------------|-------------------|-----------------|
    | 1234567898765434 |       C-003 |        2012-03-15 |           16000 |
    | 1234567898765436 |       C-005 |        2012-04-12 |           20000 |
-----------------------------------------------------------------------------------
*6.Write a query which will display customer id, customer name, date of birth, guardian name of the customers whose name starts with 'J'.*
```sql
SELECT CUSTOMER_ID, CUSTOMER_NAME, DATE_OF_BIRTH, GUARDIAN_NAME
FROM CUSTOMER_PERSONAL_INFO
WHERE CUSTOMER_NAME LIKE 'J%';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME | DATE_OF_BIRTH | GUARDIAN_NAME |
    |-------------|---------------|---------------|---------------|
    |       C-001 |          JOHN |    1984-05-03 |         PETER |
    |       C-002 |         JAMES |    1984-08-06 |        GEORGE |
-----------------------------------------------------------------------------------
*7. Write a query which will display customer id, account number and passcode.*
```sql
SELECT CUSTOMER_ID, ACCOUNT_NO, CONCAT(SUBSTRING(CUSTOMER_ID,-3),SUBSTRING(ACCOUNT_NO,-4))AS PASSCODE
FROM ACCOUNT_INFO;
```
**OUTPUT**

    | CUSTOMER_ID |       ACCOUNT_NO | PASSCODE |
    |-------------|------------------|----------|
    |       C-001 | 1234567898765432 |  0015432 |
    |       C-002 | 1234567898765433 |  0025433 |
    |       C-003 | 1234567898765434 |  0035434 |
    |       C-004 | 1234567898765435 |  0045435 |
    |       C-005 | 1234567898765436 |  0055436 |
-----------------------------------------------------------------------------------
*8. Write a query which will display the customer id, customer name, date of birth, Marital Status, Gender, Guardian name, contact no and email id of the customers whose gender is male 'M' and marital status is MARRIED.*
```sql
SELECT CUSTOMER_ID, CUSTOMER_NAME, DATE_OF_BIRTH, MARITAL_STATUS, GENDER, GUARDIAN_NAME, CONTACT_NO, MAIL_ID
FROM CUSTOMER_PERSONAL_INFO
WHERE GENDER='M' AND MARITAL_STATUS='MARRIED';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME | DATE_OF_BIRTH | MARITAL_STATUS | GENDER | GUARDIAN_NAME | CONTACT_NO |              MAIL_ID |
    |-------------|---------------|---------------|----------------|--------|---------------|------------|----------------------|
    |       C-002 |         JAMES |    1984-08-06 |        MARRIED |      M |        GEORGE | 9237893481 |  JAMES_123@gmail.com |
    |       C-004 |        RAMESH |    1985-12-11 |        MARRIED |      M |      KRISHNAN | 9235234534 | RAMESH_123@gmail.com |
-----------------------------------------------------------------------------------
*9. Write a query which will display the customer id, customer name, guardian name, reference account holders name of the customers who are referenced / referred by their 'FRIEND'.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
CUSTOMER_PERSONAL_INFO.GUARDIAN_NAME, 
CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NAME 
AS FRIEND
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN CUSTOMER_REFERENCE_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID = CUSTOMER_REFERENCE_INFO.CUSTOMER_ID;
 ```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME | GUARDIAN_NAME | FRIEND |
    |-------------|---------------|---------------|--------|
    |       C-001 |          JOHN |         PETER |    RAM |
    |       C-002 |         JAMES |        GEORGE | RAGHUL |
    |       C-003 |       SUNITHA |         VINOD |  GOKUL |
    |       C-004 |        RAMESH |      KRISHNAN | RAHMAN |
    |       C-005 |         KUMAR |         KIRAN |  VIVEK |
-----------------------------------------------------------------------------------
*10. Write a query to display the customer id, account number and interest amount in the below format with INTEREST_AMT as alias name. Example: $5 Hint: Need to prefix $ to interest amount and round the result without decimals.*
```sql
SELECT CUSTOMER_ID, ACCOUNT_NO, CONCAT('$',ROUND(INTEREST,0)) 
AS INTEREST_AMT
FROM ACCOUNT_INFO;
```
**OUTPUT**

    | CUSTOMER_ID |       ACCOUNT_NO | INTEREST_AMT |
    |-------------|------------------|--------------|
    |       C-001 | 1234567898765432 |           $5 |
    |       C-002 | 1234567898765433 |           $6 |
    |       C-003 | 1234567898765434 |           $4 |
    |       C-004 | 1234567898765435 |           $7 |
    |       C-005 | 1234567898765436 |           $8 |
-----------------------------------------------------------------------------------
*11. Write a query which will display the customer id, customer name, account no, account type, activation date, bank name whose account will be activated on '10-APR-2012'.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME,
ACCOUNT_INFO.ACCOUNT_NO, 
ACCOUNT_INFO.ACCOUNT_TYPE, 
ACCOUNT_INFO.ACTIVATION_DATE, 
BANK_INFO.BANK_NAME
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE
WHERE ACCOUNT_INFO.ACTIVATION_DATE='2012-04-10';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | ACCOUNT_TYPE | ACTIVATION_DATE | BANK_NAME |
    |-------------|---------------|------------------|--------------|-----------------|-----------|
    |       C-004 |        RAMESH | 1234567898765435 |       SALARY |      2012-04-10 |      HDFC |
-----------------------------------------------------------------------------------
*12. Write a query which will display account number, customer id, customer name, bank name, branch name, ifsc code, citizenship, interest and initial deposit amount of all the customers.*
```sql
SELECT ACCOUNT_INFO.ACCOUNT_NO, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
BANK_INFO.BANK_NAME, 
BANK_INFO.BRANCH_NAME, 
BANK_INFO.IFSC_CODE, 
CUSTOMER_PERSONAL_INFO.CITIZENSHIP, 
ACCOUNT_INFO.INTEREST, ACCOUNT_INFO.INITIAL_DEPOSIT
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE;
```
**OUTPUT**

    |       ACCOUNT_NO | CUSTOMER_ID | CUSTOMER_NAME | BANK_NAME |    BRANCH_NAME | IFSC_CODE | CITIZENSHIP | INTEREST | INITIAL_DEPOSIT |
    |------------------|-------------|---------------|-----------|----------------|-----------|-------------|----------|-----------------|
    | 1234567898765432 |       C-001 |          JOHN |      HDFC | VALASARAVAKKAM |  HDVL0012 |      INDIAN |        5 |           10000 |
    | 1234567898765433 |       C-002 |         JAMES |       SBI |         TNAGAR | SBITN0123 |      INDIAN |        6 |               0 |
    | 1234567898765434 |       C-003 |       SUNITHA |     ICICI |         TNAGAR | ICITN0232 |      INDIAN |        4 |           16000 |
    | 1234567898765435 |       C-004 |        RAMESH |      HDFC | VALASARAVAKKAM |  HDVL0012 |      INDIAN |        7 |               0 |
    | 1234567898765436 |       C-005 |         KUMAR |       SBI |       SAIDAPET | SBISD0113 |      INDIAN |        8 |           20000 |
-----------------------------------------------------------------------------------
*13. Write a query which will display customer id, customer name, date of birth, guardian name, contact number, mail id and reference account holder's name of the customers who has submitted the passport as an identification document.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
CUSTOMER_PERSONAL_INFO.DATE_OF_BIRTH, 
CUSTOMER_PERSONAL_INFO.GUARDIAN_NAME, 
CUSTOMER_PERSONAL_INFO.MAIL_ID, 
CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NAME
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN CUSTOMER_REFERENCE_INFO
ON 
CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=CUSTOMER_REFERENCE_INFO.CUSTOMER_ID
WHERE 
CUSTOMER_PERSONAL_INFO.IDENTIFICATION_DOC_TYPE
= 'PASSPORT';
```
**OUTPUT**

    |       ACCOUNT_NO | CUSTOMER_ID | CUSTOMER_NAME | BANK_NAME |    BRANCH_NAME | IFSC_CODE | CITIZENSHIP | INTEREST | INITIAL_DEPOSIT |
    |------------------|-------------|---------------|-----------|----------------|-----------|-------------|----------|-----------------|
    | 1234567898765432 |       C-001 |          JOHN |      HDFC | VALASARAVAKKAM |  HDVL0012 |      INDIAN |        5 |           10000 |
    | 1234567898765433 |       C-002 |         JAMES |       SBI |         TNAGAR | SBITN0123 |      INDIAN |        6 |               0 |
    | 1234567898765434 |       C-003 |       SUNITHA |     ICICI |         TNAGAR | ICITN0232 |      INDIAN |        4 |           16000 |
    | 1234567898765435 |       C-004 |        RAMESH |      HDFC | VALASARAVAKKAM |  HDVL0012 |      INDIAN |        7 |               0 |
    | 1234567898765436 |       C-005 |         KUMAR |       SBI |       SAIDAPET | SBISD0113 |      INDIAN |        8 |           20000 |
-----------------------------------------------------------------------------------
*14. Write a query to display the customer id, customer name, account number, account type, initial deposit, interest who have deposited maximum amount in the bank.*
```sql
SELECT A.CUSTOMER_ID,CUSTOMER_NAME,ACCOUNT_NO,
ACCOUNT_TYPE,INTEREST,INITIAL_DEPOSIT
FROM CUSTOMER_PERSONAL_INFO
A,ACCOUNT_INFO B WHERE A.CUSTOMER_ID=B.CUSTOMER_ID
AND 
INITIAL_DEPOSIT IN(SELECT MAX(INITIAL_DEPOSIT)
FROM ACCOUNT_INFO)
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | ACCOUNT_TYPE | INTEREST | INITIAL_DEPOSIT |
    |-------------|---------------|------------------|--------------|----------|-----------------|
    |       C-005 |         KUMAR | 1234567898765436 |      SAVINGS |        8 |           20000 |
-----------------------------------------------------------------------------------
*15. Write a query to display the customer id, customer name, account number, account type, interest, bank name and initial deposit amount of the customers who are getting maximum interest rate.*
```sql
SELECT ACCOUNT_INFO.CUSTOMER_ID,CUSTOMER_NAME,
ACCOUNT_NO,ACCOUNT_TYPE,INTEREST,BANK_NAME,
INITIAL_DEPOSIT
FROM CUSTOMER_PERSONAL_INFO ,ACCOUNT_INFO ,
BANK_INFO WHERE BANK_INFO.IFSC_CODE
=ACCOUNT_INFO.IFSC_CODE AND
CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID AND 
INTEREST=(SELECT MAX(INTEREST) FROM ACCOUNT_INFO)
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | ACCOUNT_TYPE | INTEREST | BANK_NAME | INITIAL_DEPOSIT |
    |-------------|---------------|------------------|--------------|----------|-----------|-----------------|
    |       C-005 |         KUMAR | 1234567898765436 |      SAVINGS |        8 |       SBI |           20000 |
-----------------------------------------------------------------------------------
*16. Write a query to display the customer id, customer name, account no, bank name, contact no and mail id of the customers who are from BANGALORE.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
ACCOUNT_INFO.ACCOUNT_NO, BANK_INFO.BANK_NAME,
BANK_INFO.BRANCH_NAME, 
CUSTOMER_PERSONAL_INFO.CONTACT_NO,
CUSTOMER_PERSONAL_INFO.MAIL_ID
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE
=ACCOUNT_INFO.IFSC_CODE
WHERE CUSTOMER_PERSONAL_INFO.ADDRESS 
LIKE '%BANGALORE';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | BANK_NAME |    BRANCH_NAME | CONTACT_NO |             MAIL_ID |
    |-------------|---------------|------------------|-----------|----------------|------------|---------------------|
    |       C-001 |          JOHN | 1234567898765432 |      HDFC | VALASARAVAKKAM | 9734526719 |  JOHN_123@gmail.com |
    |       C-002 |         JAMES | 1234567898765433 |       SBI |         TNAGAR | 9237893481 | JAMES_123@gmail.com |
    |       C-005 |         KUMAR | 1234567898765436 |       SBI |       SAIDAPET | 9242342312 | KUMAR_123@gmail.com |
-----------------------------------------------------------------------------------
*17. Write a query which will display customer id, bank name, branch name, ifsc code, registration date, activation date of the customers whose activation date is in the month of march (March 1'st to March 31'st).*
```sql 
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, 
BANK_INFO.BANK_NAME, BANK_INFO.BRANCH_NAME,
BANK_INFO.IFSC_CODE, ACCOUNT_INFO.REGISTRATION_DATE,
ACCOUNT_INFO.ACTIVATION_DATE 
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE
WHERE MONTH(ACTIVATION_DATE)=03;
```
**OUTPUT**

    | CUSTOMER_ID | BANK_NAME | BRANCH_NAME | IFSC_CODE | REGISTRATION_DATE | ACTIVATION_DATE |
    |-------------|-----------|-------------|-----------|-------------------|-----------------|
    |       C-002 |       SBI |      TNAGAR | SBITN0123 |        2012-03-12 |      2012-03-17 |
    |       C-003 |     ICICI |      TNAGAR | ICITN0232 |        2012-03-15 |      2012-03-20 |
-----------------------------------------------------------------------------------    
*18. Write a query which will calculate the interest amount and display it along with customer id, customer name, account number, account type, interest, and initial deposit amount.Hint :Formula for interest amount, calculate: ((interest/100) * initial deposit amt) with column name 'interest_amt' (alias)*
```sql
SELECT ((INTEREST/100)*INITIAL_DEPOSIT) 
AS INTEREST_AMT, CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME,
ACCOUNT_INFO.ACCOUNT_NO, ACCOUNT_INFO.ACCOUNT_TYPE,
ACCOUNT_INFO.INTEREST, 
ACCOUNT_INFO.INITIAL_DEPOSIT
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID;
```
**OUTPUT**

    | INTEREST_AMT | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | ACCOUNT_TYPE | INTEREST | INITIAL_DEPOSIT |
    |--------------|-------------|---------------|------------------|--------------|----------|-----------------|
    |          500 |       C-001 |          JOHN | 1234567898765432 |      SAVINGS |        5 |           10000 |
    |            0 |       C-002 |         JAMES | 1234567898765433 |       SALARY |        6 |               0 |
    |          640 |       C-003 |       SUNITHA | 1234567898765434 |      SAVINGS |        4 |           16000 |
    |            0 |       C-004 |        RAMESH | 1234567898765435 |       SALARY |        7 |               0 |
    |         1600 |       C-005 |         KUMAR | 1234567898765436 |      SAVINGS |        8 |           20000 |
-----------------------------------------------------------------------------------
*19. Write a query to display the customer id, customer name, date of birth, guardian name, contact number, mail id, reference name who has been referenced by 'RAGHUL'.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME,
CUSTOMER_PERSONAL_INFO.DATE_OF_BIRTH,
CUSTOMER_PERSONAL_INFO.GUARDIAN_NAME, 
CUSTOMER_PERSONAL_INFO.CONTACT_NO, 
CUSTOMER_PERSONAL_INFO.MAIL_ID, 
CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NAME
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN CUSTOMER_REFERENCE_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=CUSTOMER_REFERENCE_INFO.CUSTOMER_ID
WHERE CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NAME='RAGHUL';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME | DATE_OF_BIRTH | GUARDIAN_NAME | CONTACT_NO |             MAIL_ID | REFERENCE_ACC_NAME |
    |-------------|---------------|---------------|---------------|------------|---------------------|--------------------|
    |       C-002 |         JAMES |    1984-08-06 |        GEORGE | 9237893481 | JAMES_123@gmail.com |             RAGHUL |
-----------------------------------------------------------------------------------
*20. Write a query which will display the customer id, customer name and contact number with ISD code of all customers in below mentioned format. Sort the result based on the customer id in descending order. <BR>Format for contact number is : "+91-3digits-3digits-4digits" Example: +91-924-234-2312. Use CONTACT_ISD as alias name.*
```sql
SELECT CUSTOMER_ID, CUSTOMER_NAME,
CONCAT('+91-',SUBSTRING(CONTACT_NO,1,3),
'-',SUBSTRING(CONTACT_NO,4,3),'-',
SUBSTRING(CONTACT_NO,-4))
AS CONTACT_ISD
FROM CUSTOMER_PERSONAL_INFO
ORDER BY CUSTOMER_ID DESC;
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |      CONTACT_ISD |
    |-------------|---------------|------------------|
    |       C-005 |         KUMAR | +91-924-234-2312 |
    |       C-004 |        RAMESH | +91-923-523-4534 |
    |       C-003 |       SUNITHA | +91-943-897-8389 |
    |       C-002 |         JAMES | +91-923-789-3481 |
    |       C-001 |          JOHN | +91-973-452-6719 |
-----------------------------------------------------------------------------------
*21. Write a query which will display account number, account type, customer id, customer name, date of birth, guardian name, contact no, mail id, gender, reference account holders name, reference account holders account number, registration date, activation date, number of days between the registration date and activation date with alias name "NoofdaysforActivation", bank name, branch name and initial deposit for all the customers.*
```sql
SELECT ACCOUNT_INFO.ACCOUNT_NO,
ACCOUNT_INFO.ACCOUNT_TYPE, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_ID,
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME,
CUSTOMER_PERSONAL_INFO.DATE_OF_BIRTH,
CUSTOMER_PERSONAL_INFO.GUARDIAN_NAME, 
CUSTOMER_PERSONAL_INFO.CONTACT_NO,
CUSTOMER_PERSONAL_INFO.MAIL_ID,
CUSTOMER_PERSONAL_INFO.GENDER,
CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NAME, 
CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NO, 
ACCOUNT_INFO.REGISTRATION_DATE,
ACCOUNT_INFO.ACTIVATION_DATE, 
DATEDIFF(ACTIVATION_DATE,REGISTRATION_DATE)
AS NoofdaysforActivation,
BANK_INFO.BANK_NAME, BANK_INFO.BRANCH_NAME, 
ACCOUNT_INFO.INITIAL_DEPOSIT
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE
INNER JOIN CUSTOMER_REFERENCE_INFO
ON CUSTOMER_REFERENCE_INFO.CUSTOMER_ID
=CUSTOMER_PERSONAL_INFO.CUSTOMER_ID;
```
**OUTPUT**

    |       ACCOUNT_NO | ACCOUNT_TYPE | CUSTOMER_ID | CUSTOMER_NAME | DATE_OF_BIRTH | GUARDIAN_NAME | CONTACT_NO |               MAIL_ID | GENDER | REFERENCE_ACC_NAME | REFERENCE_ACC_NO | REGISTRATION_DATE | ACTIVATION_DATE | NoofdaysforActivation | BANK_NAME |    BRANCH_NAME | INITIAL_DEPOSIT |
    |------------------|--------------|-------------|---------------|---------------|---------------|------------|-----------------------|--------|--------------------|------------------|-------------------|-----------------|-----------------------|-----------|----------------|-----------------|
    | 1234567898765432 |      SAVINGS |       C-001 |          JOHN |    1984-05-03 |         PETER | 9734526719 |    JOHN_123@gmail.com |      M |                RAM |  987654321122345 |        2012-02-23 |      2012-02-28 |                     5 |      HDFC | VALASARAVAKKAM |           10000 |
    | 1234567898765433 |       SALARY |       C-002 |         JAMES |    1984-08-06 |        GEORGE | 9237893481 |   JAMES_123@gmail.com |      M |             RAGHUL |  987654321122346 |        2012-03-12 |      2012-03-17 |                     5 |       SBI |         TNAGAR |               0 |
    | 1234567898765434 |      SAVINGS |       C-003 |       SUNITHA |    1984-11-06 |         VINOD | 9438978389 | SUNITHA_123@gmail.com |      F |              GOKUL |  987654321122357 |        2012-03-15 |      2012-03-20 |                     5 |     ICICI |         TNAGAR |           16000 |
    | 1234567898765435 |       SALARY |       C-004 |        RAMESH |    1985-12-11 |      KRISHNAN | 9235234534 |  RAMESH_123@gmail.com |      M |             RAHMAN |  987654321122348 |        2012-04-05 |      2012-04-10 |                     5 |      HDFC | VALASARAVAKKAM |               0 |
    | 1234567898765436 |      SAVINGS |       C-005 |         KUMAR |    1983-04-26 |         KIRAN | 9242342312 |   KUMAR_123@gmail.com |      M |              VIVEK |  987654321122359 |        2012-04-12 |      2012-04-17 |                     5 |       SBI |       SAIDAPET |           20000 |
-----------------------------------------------------------------------------------
*22. Write a query which will display customer id, customer name, guardian name, identification doc type, reference account holders name, account type, ifsc code, bank name and current balance for the customers who has only the savings account. Hint: Formula for calculating current balance is add the intital deposit amount and interest and display without any decimals. Use ""CURRENT_BALANCE"" as alias name.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME,
CUSTOMER_PERSONAL_INFO.GUARDIAN_NAME,
CUSTOMER_PERSONAL_INFO.IDENTIFICATION_DOC_TYPE,
CUSTOMER_REFERENCE_INFO.REFERENCE_ACC_NAME, 
ACCOUNT_INFO.ACCOUNT_TYPE, BANK_INFO.IFSC_CODE,
BANK_INFO.BANK_NAME, 
TRUNCATE((INITIAL_DEPOSIT+INTEREST),0)
AS CURRENT_BALANCE
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE
INNER JOIN CUSTOMER_REFERENCE_INFO
ON CUSTOMER_REFERENCE_INFO.CUSTOMER_ID
=CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
WHERE ACCOUNT_TYPE='SAVINGS';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME | GUARDIAN_NAME | IDENTIFICATION_DOC_TYPE | REFERENCE_ACC_NAME | ACCOUNT_TYPE | IFSC_CODE | BANK_NAME | CURRENT_BALANCE |
    |-------------|---------------|---------------|-------------------------|--------------------|--------------|-----------|-----------|-----------------|
    |       C-001 |          JOHN |         PETER |                PASSPORT |                RAM |      SAVINGS |  HDVL0012 |      HDFC |           10005 |
    |       C-003 |       SUNITHA |         VINOD |                VOTER-ID |              GOKUL |      SAVINGS | ICITN0232 |     ICICI |           16004 |
    |       C-005 |         KUMAR |         KIRAN |                PASSPORT |              VIVEK |      SAVINGS | SBISD0113 |       SBI |           20008 |
-----------------------------------------------------------------------------------
*23. Write a query which will display the customer id, customer name, account number, account type, interest, initial deposit; check the initial deposit, if initial deposit is 20000 then display ""high"", if initial deposit is 16000 display 'moderate',if initial deposit is 10000 display 'average', if initial deposit is 5000 display 'low', if initial deposit is 0 display 'very low' otherwise display 'invalid'*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME,
ACCOUNT_INFO.ACCOUNT_NO, ACCOUNT_INFO.ACCOUNT_TYPE,
ACCOUNT_INFO.INTEREST, ACCOUNT_INFO.INITIAL_DEPOSIT,
CASE
WHEN INITIAL_DEPOSIT=20000 THEN 'high'
WHEN INITIAL_DEPOSIT=16000 THEN 'moderate'
WHEN INITIAL_DEPOSIT=10000 THEN 'average'
WHEN INITIAL_DEPOSIT=5000 THEN 'low'
WHEN INITIAL_DEPOSIT=0 THEN 'very low'
ELSE 'invalid' END DEPOSIT_STATUS
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID;
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | ACCOUNT_TYPE | INTEREST | INITIAL_DEPOSIT | DEPOSIT_STATUS |
    |-------------|---------------|------------------|--------------|----------|-----------------|----------------|
    |       C-001 |          JOHN | 1234567898765432 |      SAVINGS |        5 |           10000 |        average |
    |       C-002 |         JAMES | 1234567898765433 |       SALARY |        6 |               0 |       very low |
    |       C-003 |       SUNITHA | 1234567898765434 |      SAVINGS |        4 |           16000 |       moderate |
    |       C-004 |        RAMESH | 1234567898765435 |       SALARY |        7 |               0 |       very low |
    |       C-005 |         KUMAR | 1234567898765436 |      SAVINGS |        8 |           20000 |           high |
-----------------------------------------------------------------------------------    
*24. Write a query which will display customer id, customer name, account number, account type, bank name, ifsc code, initial deposit amount and new interest amount for the customers whose name starts with ""J"". Hint: Formula for calculating ""new interest amount"" is if customers account type is savings then add 10 % on current interest amount to interest amount else display the current interest amount. Round the new interest amount to 2 decimals. Use ""NEW_INTEREST"" as alias name for displaying the new interest amount. Example, Assume Jack has savings account and his current interest amount is 10.00, then the new interest amount is 11.00 i.e (10 + (10 * 10/100)).*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
ACCOUNT_INFO.ACCOUNT_NO, ACCOUNT_INFO.ACCOUNT_TYPE,
BANK_INFO.BANK_NAME, BANK_INFO.IFSC_CODE,
ACCOUNT_INFO.INITIAL_DEPOSIT,
CASE
WHEN ACCOUNT_TYPE='SAVINGS' 
THEN ROUND((INTEREST+(INTEREST*10/100)),2)
ELSE INTEREST END 'NEW INTEREST AMOUNT'
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO
ON CUSTOMER_PERSONAL_INFO.CUSTOMER_ID
=ACCOUNT_INFO.CUSTOMER_ID
INNER JOIN BANK_INFO
ON BANK_INFO.IFSC_CODE=ACCOUNT_INFO.IFSC_CODE
WHERE CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME LIKE 'J%';
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | ACCOUNT_TYPE | BANK_NAME | IFSC_CODE | INITIAL_DEPOSIT | NEW INTEREST AMOUNT |
    |-------------|---------------|------------------|--------------|-----------|-----------|-----------------|---------------------|
    |       C-001 |          JOHN | 1234567898765432 |      SAVINGS |      HDFC |  HDVL0012 |           10000 |                 5.5 |
    |       C-002 |         JAMES | 1234567898765433 |       SALARY |       SBI | SBITN0123 |               0 |                   6 |
-----------------------------------------------------------------------------------
*25.Write query to display the customer id, customer name, account no, initial deposit, tax percentage as calculated below.*
```sql
SELECT CUSTOMER_PERSONAL_INFO.CUSTOMER_ID, 
CUSTOMER_PERSONAL_INFO.CUSTOMER_NAME, 
ACCOUNT_INFO.ACCOUNT_NO, ACCOUNT_INFO.INITIAL_DEPOSIT,
CASE
WHEN INITIAL_DEPOSIT=0 THEN '0%'
WHEN INITIAL_DEPOSIT<=10000 THEN '3%'
WHEN INITIAL_DEPOSIT>10000 AND INITIAL_DEPOSIT<20000 
THEN '5%'
WHEN INITIAL_DEPOSIT>=20000 AND INITIAL_DEPOSIT<=30000 
THEN '7%'
WHEN INITIAL_DEPOSIT>30000 
THEN '10%' END 'TAX PERCENTAGE'
FROM CUSTOMER_PERSONAL_INFO
INNER JOIN ACCOUNT_INFO;
```
**OUTPUT**

    | CUSTOMER_ID | CUSTOMER_NAME |       ACCOUNT_NO | INITIAL_DEPOSIT | TAX PERCENTAGE |
    |-------------|---------------|------------------|-----------------|----------------|
    |       C-001 |          JOHN | 1234567898765432 |           10000 |             3% |
    |       C-002 |         JAMES | 1234567898765432 |           10000 |             3% |
    |       C-003 |       SUNITHA | 1234567898765432 |           10000 |             3% |
    |       C-004 |        RAMESH | 1234567898765432 |           10000 |             3% |
    |       C-001 |          JOHN | 1234567898765433 |               0 |             0% |
    |       C-002 |         JAMES | 1234567898765433 |               0 |             0% |
    |       C-003 |       SUNITHA | 1234567898765433 |               0 |             0% |
    |       C-004 |        RAMESH | 1234567898765433 |               0 |             0% |
    |       C-001 |          JOHN | 1234567898765434 |           16000 |             5% |
    |       C-002 |         JAMES | 1234567898765434 |           16000 |             5% |
    |       C-003 |       SUNITHA | 1234567898765434 |           16000 |             5% |
    |       C-004 |        RAMESH | 1234567898765434 |           16000 |             5% |
    |       C-001 |          JOHN | 1234567898765435 |               0 |             0% |
    |       C-002 |         JAMES | 1234567898765435 |               0 |             0% |
    |       C-003 |       SUNITHA | 1234567898765435 |               0 |             0% |
    |       C-004 |        RAMESH | 1234567898765435 |               0 |             0% |
    |       C-001 |          JOHN | 1234567898765436 |           20000 |             7% |
    |       C-002 |         JAMES | 1234567898765436 |           20000 |             7% |
    |       C-003 |       SUNITHA | 1234567898765436 |           20000 |             7% |
    |       C-004 |        RAMESH | 1234567898765436 |           20000 |             7% |
    |       C-005 |         KUMAR | 1234567898765432 |           10000 |             3% |
    |       C-005 |         KUMAR | 1234567898765433 |               0 |             0% |
    |       C-005 |         KUMAR | 1234567898765434 |           16000 |             5% |
    |       C-005 |         KUMAR | 1234567898765435 |               0 |             0% |
    |       C-005 |         KUMAR | 1234567898765436 |           20000 |             7% |
-----------------------------------------------------------------------------------
