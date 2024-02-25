---
permalink: /enhancementone/
title: "Enhancement One: Software Engineering and Design"
modified: 2024-02-23
---

## Task Service Application Enhancement

The artifact selected for enhancement in the database is the CrudModule class file, part of the Grazioso Salvare Project in the Advanced Programming Concepts course (CS340). The artifact, developed using Python, was created in December 2022, to authenticate access to the database and implement the CRUD (create, read, update, and delete) functionality for the database. The project consisted of the import of the mongoimport tool for accessing the database, the creation of an administrator and user account, a PY file, using object-oriented programming methodology, to enable the CRUD functionality, and a Python module to test and ensure each account type could be accessed and each part of the CRUD module operated properly.


### Weaknesses and Limitations

1. Authentication and database access are limited to live data only which puts the data at risk
2. None of the files include a header, which should include the programmer, version, and a description of the file's purpose
3. While there is a print function for displaying exceptions, they do not give additional details which slows error handling


```python
from pymongo import MongoClient
from bson.objectid import ObjectId

class AnimalShelter(object):
    """CRUD OPERATIONS for Animal Collection in MongoDB"""
    
    def __init__(self, user, password):
        #self.client = MongoClient('mongodb://localhost:53598')
        #self.client = MongoClient('mongodb://127.0.0.1:37300/?authSource=AAC&compressors=disabled&gssapiServiceName=mongodb' % (user, password))
        self.client = MongoClient('mongodb://%s:%s@localhost:53598/AAC' % (aacuser, UserCS340))
        self.database = self.client['AAC']
        print("Connected to Database")
}

  #Implement create in Crud
    def create(self, data):
        try:
            if data is not None:
                insert_result = self.database.animals.insert_one(data) #data should be dictionary
                print(insert_result)
                return True
            else:
                #Raise error
                raise Exception("Nothing to save, data is empty")
        except:
            return False # return false for bool requirement
```


### Enhancements Made

1.	Incorporating a test mode configuration parameter within the AnimalShelter Python file, which runs the instance in test mode if test mode = true.
2.	Importing the use of Mongomock in the CrudModule class file, which is used for in-memory database access in testing environments.
3.	 Incorporating test credentials for database access authentication.
4.	Separate test scripts for testing in production and development environments.
5.	The replacement of the printing statement for logging, which is a more suitable solution for the use of development and production environments, making outputs cleaner.
6.	The replacement of block exceptions with catch-specific exceptions, which helps with debugging by providing more information on errors as they arise.

The enhancements made to the CrudModule class file, and its associated files, exceeded the planned enhancement proposed in Module One. The plan originally focused on just the CrudModule class file, but while incorporating improvements, files associated with the CrudModule class file needed to reflect the enhancements made in incorporating the test configuration and test instance. As a result of the enhancement, the outcome-coverage plan was updated to include separate files for production and development testing.  


```python
# ==================================================================
# File: CRUD Class 
# Programmer Name: Domingo Polonia Jr
# Created For: Advanced Programming Concepts CS340
# Creation Date: December 2022
# Course: CS499 Capstone
# Date: 02-21-2024
# Version: 2.2
# Description: This Python class file is to capture the logic for
# Create, Read, Update, and Delete operations. For testing purposes
# this file also imports a mongomock library, used for in-memory
# database access, logging for debugging purposes, and detailed error
# handling, to catch specific exceptions.
# ==================================================================

from pymongo import MongoClient
from bson.objectid import ObjectId
import mongomock
import logging

# Configure logging
logging.basicConfig(level=logging.INFO)

class AnimalShelter(object):
    """CRUD OPERATIONS for Animal Collection in MongoDB"""
    
    def __init__(self, user, password, aacuser, UserCS340, db_connection=None):
        # If a mock database connection is provided, use it
        # Otherwise, establish a new MongoDB connection with the given credentials
        if db_connection:
            self.database = db_connection
        else:
            # Original connection string modified to accept credentials
            self.client = MongoClient('mongodb://%s:%s@localhost:53598/AAC' % (aacuser, UserCS340))
            self.database = self.client['AAC']

        print("Connected to Database")

        # Usage in test environment
        # Assuming a test environment is required and mongomock needs to be used
        
    def test_setup():
        mock_db = mongomock.MongoClient().AAC
        animal_shelter = AnimalShelter(user="dummyUser", password="dummyPassword", aacuser="dummyAacuser", UserCS340="dummyUserCS340", db_connection=mock_db)
        # The animal_shelter class can now be used with a mocked database for testing

  #Implement Create in Crud
    def create(self, data):
        try:
            if data is not None:
                # Data should be dictionary
                insert_result = self.database.animals.insert_one(data) 
                # Logging for debugging purposes in production application
                logging.info(f"Insert successful, ID: {insert_result.inserted_id}")
                return {'success': True, 'id': insert_result.inserted_id}
            else:
                # Specific error handling to catch exceptions
                raise ValueError("Nothing to save, data is empty")
        except ValueError as ve:
            logging.error(f"Validation error: {ve}")
            return {'success': False, 'error': str(ve)}
        except Exception as e:
            logging.error(f"Unexpected error: {e}")
            return {'success': False, 'error': 'Unexpected error occurred'}
```


### Lessons Learned

Implementing a test configuration and test instance in the CrudModule, Dashboard, and test script class files was important in learning additional concepts in database-driven applications. For example, one concept learned is designing software in modular components to allow swapping between production and test instances. Additionally, keeping in mind additional enhancements, using a method to toggle between instances allows the enhancements to be tested in a development environment before it’s deployed. The main challenge faced in incorporating the enhancement was consistency between the files, but code reviews and documentation helped detect inconsistency in the enhancement. 


### Skills and Abilities Showcased

1.	Database management by creating database schemas for different environments and designing test data that reflects production data structures without using real data.
2.	Database system design by creating a modular design that allows switching between different configurations, in this case, a test configuration and instance.
3.	Database collaboration by documenting code files in a way to allows for cross-functional team collaboration for development, security, and operations.


### Course Outcomes Demonstrated

### Employment strategies for building collaborative environments that enable diverse audiences to support organizational decision-making in the field of computer science by:

1.	Using a test instance for privacy and data protection in strategic development, collaborative privacy design, and access controls.
3.	Using a test instance to simulate cyber attacks in cross-functional cybersecurity testing, feedback, and incident response, and cybersecurity awareness.
4.	Using a test instance for learning and innovation in learning opportunities, prototype testing, and collaborative workflows.

### The development of a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources by:

1.	Promoting secure development lifecycle practices in continuous security training, automated security scanning, and risk assessment and management.
2.	Enforcing the principle of least privilege in minimal access rights, regular access reviews, and zero trust architecture.
3.	Facilitating test environments for security audits and penetration testing in dedicated testing environments, regular penetration testing, and security audits.

Original and enhanced technical files can be found in the course repository [CS320 Software Automation and Quality Assurance]([https://github.com/dpoloniajr/CS-320-Software-Testing-Automation-and-QA]).
