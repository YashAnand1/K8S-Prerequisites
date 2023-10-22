<div align="center">


<!-- add technical charcha logo postgres session 3 -->
# PostgresSQL Session 4        
### — Task Documentation by Yash Anand —    
__________________________________________________________________________________

## Contents
</div>

## Contents

  - [**Overview**](#overview)
  - [**Task 1: Create Roles**](#task-1-create-roles)
    - [**1.1. Creating Three Roles**](#11-creating-three-roles)
    - [**1.2. Assigning Passwords**](#12-assigning-passwords)
  - [**Task 2: Grant Privileges**](#task-2-grant-privileges)
    - [**2.1. Creating DB: `ecommerce`**](#21-creating-db-ecommerce)
    - [**2.2 Assigning Privileges To Users**](#22-assigning-privileges-to-users)
      - [**2.2.1 All DB Privileges To `admin`**](#221-all-db-privileges-to-admin)
      - [**2.2.2 Read \& Write Table Privileges To `employee`**](#222-read--write-table-privileges-to-employee)
      - [**2.2.3 Read Table Privileges To `customer`**](#223-read-table-privileges-to-customer)
  - [**Task 3: Host Based Authentication**](#task-3-host-based-authentication)
    - [**3.1. Understanding `pg_hba.conf`**](#31-understanding-pg_hbaconf)
    - [**3.2 Connecting Localhost With All Roles**](#32-connecting-localhost-with-all-roles)
    - [**3.3 Allowing Admin To Connect From All IPs**](#33-allowing-admin-to-connect-from-all-ips)
  - [**Task 4: Table and Schema Creation**](#task-4-table-and-schema-creation)
    - [**4.1. Creating Product Schema**](#41-creating-product-schema)
    - [**4.2. Creating `products` Table**](#42-creating-products-table)
  - [**Task 5: Generate Self-Signed Certificates**](#task-5-generate-self-signed-certificates)
  - [**Task 6: Configure PostgreSQL**](#task-6-configure-postgresql)
  - [**Task 7: Configure pg\_hba.conf**](#task-7-configure-pg_hbaconf)
  - [**Task 8: Testing**](#task-8-testing)
  - [**Conclusion**](#conclusion)

_____________________________________________________________________________________     
<div align="center">

## **Task 1**
What is process, share the command so that we can identify resources utilisation according to process.
</div>

As per this task, we were to create 3 roles and assign passwords to each of them. The demonstration of how this task was executed has been provided below.


___________________________________________________

## **References**
</div>
Task 1: 
https://www.padok.fr/en/blog/docker-processes-container#:~:text=Each%20process%20can%20have%20child,you%20can%20imagine%20its%20importance.

Task 2:
https://www.reddit.com/r/docker/comments/119unid/docker_and_pid_1/

Task 7:
https://www.tutorialspoint.com/running-docker-container-as-a-non-root-user

Task 8:


--------
