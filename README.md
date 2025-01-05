# -Employee-Management-System-EMS-Database-Implementation-
Proficient in SQL with experience in creating databases, tables, and views.   • Created a database named emp_details with tables Employee, Department, and Project.   • Developed complex SQL queries to retrieve and analyze data, including aggregations, joins, and subqueries. 
# Create the Database and Schema
-- Create database
CREATE DATABASE emp_details;

-- Use the database
USE emp_details;

-- Create Department table
CREATE TABLE Department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

-- Create Project table
CREATE TABLE Project (
    project_id INT PRIMARY KEY,
    project_name VARCHAR(50)
);

-- Create Employee table
CREATE TABLE Employee (
    name VARCHAR(50),
    job_title VARCHAR(50),
    phone_no VARCHAR(15),
    salary DECIMAL(10, 2),
    dept_id INT,
    project_id INT,
    FOREIGN KEY (dept_id) REFERENCES Department(dept_id),
    FOREIGN KEY (project_id) REFERENCES Project(project_id)
);
#2. Insert Data into Tablessql
-- Insert data into Department table
INSERT INTO Department (dept_id, dept_name)
VALUES
(101, 'Legal'),
(102, 'Services'),
(103, 'Support'),
(104, 'Marketing'),
(105, 'Sales');

-- Insert data into Project table
INSERT INTO Project (project_id, project_name)
VALUES
(201, 'Tresom'),
(202, 'Overhold'),
(203, 'Daltfresh'),
(204, 'Zontrax'),
(205, 'Ventosanzap');

-- Insert data into Employee table
INSERT INTO Employee (name, job_title, phone_no, salary, dept_id, project_id)
VALUES
('Cedric', 'Executive Secretary', '353-769-4671', 170000, 101, 201),
('Nicol', 'Electrical Engineer', '580-827-2074', 120000, 101, 202),
('Iolande', 'Graphic Designer', '992-810-6080', 130000, 101, 203),
('Balduin', 'Financial Advisor', '116-752-1163', 140000, 102, 204),
('Shelley', 'VP Accounting', '876-413-3680', 95000, 102, 205),
('Roddie', 'Graphic Designer', '835-244-2459', 97000, 102, 201),
('Husein', 'Analyst Programmer', '365-236-0502', 54000, 103, 202),
('Denver', 'Account Representative IV', '777-497-5955', 170000, 103, 203),
('Benjy', 'Data Coordinator', '483-972-8539', 137905, 103, 204),
('Enoch', 'Technical Writer', '107-509-5878', 120000, 104, 205),
('Helenka', 'Web Designer I', '147-925-7666', 110000, 104, 201),
('Kelsey', 'Civil Engineer', '968-936-2767', 79000, 104, 202),
('Binni', 'Civil Engineer', '736-983-0790', 160000, 105, 203),
('Nara', 'Research Assistant I', '531-584-1812', 59000, 105, 204),
('Omar', 'Marketing Manager', '435-129-2187', 149063, 105, 205);

#3. Write Queries
SELECT p.project_name, SUM(e.salary) AS total_salary
FROM Employee e
JOIN Project p ON e.project_id = p.project_id
GROUP BY p.project_name;
#b. Display details of employees with salaries greater than the department average
SELECT e.*
FROM Employee e
JOIN (
    SELECT dept_id, AVG(salary) AS avg_salary
    FROM Employee
    GROUP BY dept_id
) d_avg ON e.dept_id = d_avg.dept_id
WHERE e.salary > d_avg.avg_salary;
#Generate email IDs for all employees
SELECT 
    LOWER(CONCAT(e.name, '@', p.project_name, '.', d.dept_name, '.com')) AS email_id
FROM Employee e
JOIN Department d ON e.dept_id = d.dept_id
JOIN Project p ON e.project_id = p.project_id;
#d. Display the number of employees in each department
SELECT d.dept_name, COUNT(e.name) AS employee_count
FROM Department d
LEFT JOIN Employee e ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
# 4 Create a Cross Join
SELECT *
FROM Employee e
CROSS JOIN Project p;
#5. Create a View
CREATE VIEW EmployeeView AS
SELECT name, phone_no, job_title
FROM Employee;










