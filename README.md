# pysert

A python script that can be used to generate arbitrary formatted data.

For a more complex solution, please check www.mockneat.com - a Java library that does exactly what this script does, and much more.

_(Note: Initially written the script around 2012, found it in the google code archives)._

# Using the script

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

# Supported datasets

The supported datasets you can use are: 

* `RandomNumber`:
  - `"name"`: `<string value>`
  - `"floating"` : `"<boolean value>"`
  - `"min"`: `"<integer value>"`
  - `"max"`: `"<integer value>"`
* `LoremIpsum`:
  - `"name"` : `<string value>`
  - `"length"` : `"<integer value>"`
* `PersonalName`:
  - `"name"` : `<string value>`
  - `"firstname"` : `"<boolean value>"`
  - `"lastname"` : `"<boolean value>"`
* `Sequence` :
  - `"name"` : `<string value>`
  - `"start"` : `"<integer value>"`
  - `"increment"` : `"<integer value>"`
  
# Adding your own data set:

All you have to do is to:
1. Extend the class `AbstractDataSet`
2. Override the method `def validation_list(self):` by including the properties of the DataSet - script will validate the input `xml` based on that.
3. Overtide the method `def next_value(self):`. Here you define the "arbitrary" / "random" behavior of the data set.


