Download Link: https://assignmentchef.com/product/solved-ece356-lab-1-sql-queries
<br>
<h1>1           Database setup</h1>

You will use the mysql command line utility to connect to a MySQL DBMS on the server manta.uwaterloo.ca. You will then create some tables, add some data, and use SQL statements to manipulate this database.

Using SSH, you should first connect to ecetesla0.uwaterloo.ca or ecetesla3.uwaterloo.ca with your Nexus user name and password.<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> Once you are connected by SSH, you can access the DBMS via the following command:

mysql -h manta -u user_&lt;nexususerid&gt; -p

For example, for user x12cool, the command will be:

mysql -h manta -u user_x12cool -p

Each student has a temporary MySQL password of the following form:

user <em>&lt;</em>nexususerid<em>&gt; </em>HeLLo<em>&lt;</em>&amp;F20!

For example, for user x12cool, the temporary password is:

user x12cool HeLLo<em>&lt;</em>&amp;F20!

Please change your temporary password as soon as possible. To do so, use a command of the following form:

set password = ’myCleverNewPassword’;

Remember to replace ‘myCleverNewPassword’ with your own clever password.

The mysql utility provides a command line interface to the DBMS running on manta. A DBMS may store many databases, and so upon connecting to the DBMS, you must first specify the database that you will be working with. This is accomplished by executing a command of the following form:

use ece356db_&lt;nexususerid&gt;;

For example, for user x12cool, the command will be:

use ece356db_x12cool;

Once you have chosen the correct database, you can create the required tables and add data to these tables. We provide a script for this purpose, called createTables.sql. Examine this file to familiarize yourself with the tables and data that your database will contain. The logical schema is illustrated below in Figure 1 for your convenience.

Figure 1: Enterprise schema for Lab 1.

To create the schema, first copy the createTables.sql script to the host where you are running the mysql utility (e.g., ecetesla0 or ecetesla1). This can be accomplished using tools like scp or sftp. Next, execute the script using the following command:

source createTables.sql;

Verify that the script ran to completion without producing any errors, and check that the required tables now exist in your database by running the following command:

show tables;

Please contact a TA as soon as possible if you experience any technical difficulties with the setup. The names and email addresses of the TAs are in the course syllabus, which is available in LEARN.

<h1>2           Submission guidelines</h1>

Your mission for Lab 1 is to write SQL code that solves the problems posed in Section 3. Please follow the submission guidelines in this section carefully before submitting your solution to the Lab 1 dropbox in LEARN, as otherwise your submission may break our grading script and lead to academic penalties.

First, download the provided lab1.sql template file from LEARN.

Write your answers in this file for each problem in the appropriate place, which is indicated by the block comments (/* … */).

Do <u>not </u>remove the separator lines, which start with four dashes (e.g., —- 1b). Similarly, do <u>not </u>add any new lines containing four dashes. Standard SQL comments use double dashes, and are allowed.

Submit your completed lab1.sql file to the Lab 1 dropbox in LEARN before the due date (as specified in the dropbox details). Note that only one file is accepted per dropbox submission, and each re-submission prior to the deadline overwrites the previous one.

<strong>Note 1: </strong>Submissions that do not comply with the above guidelines will be penalized up to 100%.

<strong>Note 2: </strong>The grading script will use the same schema as defined in createTables.sql, but with a different data set.

<h1>3           Problems</h1>

<strong>Note: </strong>The solution to each problem must be a <strong>single SQL statement terminated by a semicolon</strong>.

<h2>Single table queries</h2>

1a) Which departments are in located Cairo?

1b) How many people are employed in each job type in the company, ordered ascending by job type? The names of the output columns for the job type and number of people should be job and count, respectively. <strong>(Marked for submission)</strong>

1c) What are the names and salaries of the engineers?

1d) What is the average salary by job type?

1e) What is the ID of the department (or department(s) if there is tie) with the most engineers? The name of the output column should be deptID. <strong>(Marked for submission)</strong>

1f) For engineering departments, what is the percentage of engineers in each department (provide the corresponding department ID)?

1g) Return the empID of all employees earning the second-highest salary, as defined in Appendix A for <em>k </em>= 2. <strong>(Marked for submission)</strong>

<h2>Multi table queries</h2>

2a) What are the names and IDs of employees who are currently not assigned to any project? The names of the output columns should be empName and empID, respectively. <strong>(Marked for submission) </strong>2b) What are the names, jobs and roles of all employees whose role is different than their job?

2c) What is the number of employees, by job, whose role is identical to their job?

2d) What is the total of the salaries of all employees assigned to each project?

2e) Repeat (2d) but include an additional row for the total of the salaries of all employees not assigned to any project. The names of the output columns should be projectSalary and projID. The projID for the additional row representing employees without projects should be the SQL null value. <strong>(Marked for submission) </strong>2f) Identify the employees (if any), by name and ID, who are assigned to more than one project.

<h2>Data insertion, deletion, and update</h2>

To ensure that your results are reproducible, please ensure that you reload your database (i.e., rerun the provided SQL script) before running the code for each of the following problems.

3a) Raise the salary of everyone working on the compiler project by 10%. <strong>(Marked for submission)</strong>

3b) Raise the salary of all janitors by 5%, and all Waterloo employees by 8%; if there are any janitors in Waterloo, their pay should be raised by 8%, not by 13%. <strong>(Marked for submission)</strong>

3c) Add a nullable column shift of type VARCHAR(5) to the Employee table. <strong>(Marked for submission)</strong>

3d) Populate the shift column created in part (3c) with a value for each employee that satisfies the criteria defined in Figure 2. <strong>(Marked for submission)</strong>

Figure 2: Criteria for values in the new column shift.

<h1>A         Definition of <em>k</em>th-highest salary</h1>

This appendix defines the meaning of <em>k</em>th-highest salary, taking into account cases where multiple employees may share the same salary. Consider the table shown below in Figure 3:

Figure 3: Projection of Employee table onto employee ID and salary.

Next, consider the distinct salaries in descending order, as shown in Figure 4:

Figure 4: Salaries sorted in descending order.

The <em>k</em>th-highest salary is then defined as the value in the <em>k</em>th row of the table in Figure 4. (We will assume that there are at least <em>k </em>distinct salaries in the Employee table.) For example, when <em>k </em>= 1, the <em>k</em>th-highest salary is the highest salary, or 50000. Similarly, when <em>k </em>= 2, the <em>k</em>th-highest salary is the second-highest salary, or 45000.

Note that when asked to compute the IDs of employees earning the <em>k</em>th-highest salary, the result set may contain more than one row. For example, for <em>k </em>= 1, two employees are tied for first place, as shown in Figure 5:

Figure 5: IDs of employees with highest salary (<em>k </em>= 1).

For <em>k </em>= 2, there is a three-way tie, as shown in Figure 6:

Figure 6: IDs of employees with second-highest salary (<em>k </em>= 2).

<a href="#_ftnref1" name="_ftn1">[1]</a> The firewall blocks access to the MySQL port from outside, and so you will need to use the campus VPN if you are working from home.