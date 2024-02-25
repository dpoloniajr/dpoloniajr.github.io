---
permalink: /enhancementthree/
title: "Enhancement Three: Databases"
modified: 2024-02-23
---

## Animal Shelter Database Enhancement

The artifact selected for enhancement in the database is the CrudModule class file, part of the Grazioso Salvare Project in the Advanced Programming Concepts course (CS340). The artifact, developed using Python, was created in December 2022, to authenticate access to the database and implement the CRUD (create, read, update, and delete) functionality for the database. The project consisted of the import of the mongoimport tool for accessing the database, the creation of an administrator and user account, a PY file, using object-oriented programming methodology, to enable the CRUD functionality, and a Python module to test and ensure each account type could be accessed and each part of the CRUD module operated properly.


### Weaknesses and Limitations

1. Authentication and database access are limited to live data only which puts the data at risk
2. None of the files include a header, which should include the programmer, version, and a description of the file's purpose
3. While there is a print function for displaying exceptions, they do not give additional details which slows error handling


### Enhancements Made

1.	Incorporating a test mode configuration parameter within the AnimalShelter Python file, which runs the instance in test mode if test mode = true.
2.	Importing the use of Mongomock in the CrudModule class file, which is used for in-memory database access in testing environments.
3.	 Incorporating test credentials for database access authentication.
4.	Separate test scripts for testing in production and development environments.
5.	The replacement of the printing statement for logging, which is a more suitable solution for the use of development and production environments, making outputs cleaner.
6.	The replacement of block exceptions with catch-specific exceptions, which helps with debugging by providing more information on errors as they arise.

The enhancements made to the CrudModule class file, and its associated files, exceeded the planned enhancement proposed in Module One. The plan originally focused on just the CrudModule class file, but while incorporating improvements, files associated with the CrudModule class file needed to reflect the enhancements made in incorporating the test configuration and test instance. As a result of the enhancement, the outcome-coverage plan was updated to include separate files for production and development testing.  


### Lessons Learned

Implementing a test configuration and test instance in the CrudModule, Dashboard, and test script class files was important in learning additional concepts in database-driven applications. For example, one concept learned is designing software in modular components to allow swapping between production and test instances. Additionally, keeping in mind additional enhancements, using a method to toggle between instances allows the enhancements to be tested in a development environment before it’s deployed. The main challenge faced in incorporating the enhancement was consistency between the files, but code reviews and documentation helped detect inconsistency in the enhancement. 


### Skills and Abilities Showcased

1.	Database management by creating database schemas for different environments and designing test data that reflects production data structures without using real data.
2.	Database system design by creating a modular design that allows switching between different configurations, in this case, a test configuration and instance.
3.	Database collaboration by documenting code files in a way to allows for cross-functional team collaboration for development, security, and operations.


### Course Outcomes Demonstrated

### 1.	Employment strategies for building collaborative environments that enable diverse audiences to support organizational decision-making in the field of computer science by:

a.	Using a test instance for privacy and data protection
b.	Using a test instance to simulate cyber attacks
c.	Using a test instance for learning and innovation

### 2.	The development of a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources by:

a.	Promoting secure development lifecycle practices
b.	Enforcing the principle of least privilege
c.	Facilitating test environments for security audits and penetration testing

Original and enhanced technical files can be found in the course repository [CS340 Advanced Programming Concepts](https://github.com/dpoloniajr/CS-340-Advanced-Programming-Concepts/tree/main).
