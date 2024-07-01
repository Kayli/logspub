# sql related information

## basics

- sql (structured query language)
  - domain-specific language designed for managing and manipulating datasets
  - can be used to query relational (e.g. mssql) as well semi-structured data (e.g. spark)

- core components
  - ddl (data definition language)
    - commands that define the structure of the database schema
    - including create, alter, and drop statements for tables, views, indexes, and databases
  - dml (data manipulation language)
    - commands that deal with data management within tables
    - this includes select, insert, update, and delete statements
  - dcl (data control language)
    - commands related to permissions and access controls, like grant and revoke
  - tcl (transaction control language)
    - commands that deal with the transactional control of data, like commit and rollback


## common table expression (cte)

- temporary named result set
  - that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement

- similar to derived tables, but provide more readability and ease of use
  - especially for complex queries involving recursion or multiple steps

- can contain
  - multiple with ... as clauses
    - following clauses can use previously defined clauses within the same clauses list
  - explicit column names, providing
    - better clarity and readability
    - column aliasing
    - schema maintenance
    - reduced ambiguity

- example
  - link: https://www.db-fiddle.com/f/4Vhu6gM9iNVR6iivHyA8Rp/1
  ```sql
    with
      emp_depts (employee_name, department, salary) as (
        select e.name as employee_name, d.name as department, salary
          from Employees as e 
            join Departments as d on e.department_id=d.department_id
      ),
      dpt_salaries_avg as (
        select department, avg(salary) as avg_dpt_salary
          from emp_depts
          group by department
      )
    select employee_name, salary, e.department, avg_dpt_salary   
      from emp_depts as e
        join dpt_salaries_avg as d on e.department = d.department
      where e.salary > d.avg_dpt_salary
  ```

- dialects/versions support
  - mysql 8.0+
  - postgres 9.4+ (at least)
  - sqlite 3.26+ (at least)


## postgresql

- automatic migrations: liquibase


## useful links

- cloud sql editors
  - https://www.db-fiddle.com
    - just works, but somewhat rudimentary error highlighting capabilities
  
  - https://github.com/dbeaver/cloudbeaver
    - have to host locally in a docker container
