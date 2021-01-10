# pysert

A python script that can be used to generate arbitrary formatted data.

_(Note: Initially written the script around 2012, found it in the google code archives)._

#How to

To be used with `python3`:

```python
python3 pysert.py -i tmpl.xml -o out.txt
```

`tmpl.xml` is the template based on which the script will generate the data:

```xml
<pysert iterations="20">
	<!--  Declarative area -->
	<dataset name="id" type="Sequence" start="300" increment="1"/>
	<dataset name="fname" type="PersonalName" firstname="True" lastname="False"/>
	<dataset name="lname" type="PersonalName" firstname="False" lastname="True"/>
	<dataset name="jobid" type="RandomNumber" floating="False" min="100" max="200"/>
	<dataset name="salary" type="RandomNumber" floating="False" min="1000" max="15000"/>
	<!--  Actual template to be converted -->
	<template>
INSERT INTO EMPLOYEES
	(EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, JOB_ID, SALARY)
VALUES
	(#{id}, '#{fname}', '#{lname}', '#{fname}_#{lname}@domain.com', #{jobid},
	#{salary})
	</template>
 </pysert>
```

After running the above command, a fille called `out.txt` will be generated.
The contents of the file are actual SQL Inserts:

```SQL
INSERT INTO EMPLOYEES
	(EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, JOB_ID, SALARY)
VALUES
	(300, 'Paula', 'Chehachkov', 'Paula_Chehachkov@domain.com', 175,
	8439)


INSERT INTO EMPLOYEES
	(EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, JOB_ID, SALARY)
VALUES
	(301, 'Gabriel', 'Vlas', 'Gabriel_Vlas@domain.com', 183,
	11362)


INSERT INTO EMPLOYEES
	(EMPLOYEE_ID, FIRST_NAME, LAST_NAME, EMAIL, JOB_ID, SALARY)
VALUES
	(302, 'Mia', 'Fugger', 'Mia_Fugger@domain.com', 181,
	2080)

// (... and so on)  
```

# Notes

The supported datasets you can use are: 

* `RandomNumber`: 
  - `"name" : <string value>`
  - ``"floating" : "<boolean value>"`
  - `"min": "<integer value>"
  - `"max": "<integer value>"`

