---
permalink: /enhancementone/
title: "Enhancement One: Software Engineering and Design"
modified: 2024-02-23
---

## Task Service Application Enhancement

The artifacts selected for enhancement in the software engineering and design category are Task and Task Service class, part of the Grand Strand Application Project in the Software Testing, Automation, and Quality Assurance course (CS320). The artifacts were originally created in December 2021, and the two Java class files were developed to use in-memory data structures to support storing tasks. The Task class required a name string field between 1 and 20 characters, therefore not null, and a description field of no more than 50 characters. The Task Service Class required a unique ID with the ability to delete and update tasks per task ID. Only the name and description fields can be updated. 



### Weaknesses and Limitations

1. 
2. 
3. 


### Original Task Class File

```java
package task;

public class Task {

	/*
	 * We initialize our variables to be used in the constructor and 
	 * mutator/accessor methods
	 */
	private String taskId;
	private String name;
	private String description;

	/*
	 * Our constructor with its parameters and conditionals set to the 
	 * specifications in the requirements doc. Then assigning the values 
	 * if the conditional statements pass.
	 */
	
	public Task(String id, String name, String desc) {

		if (id == null || id.length() > 10) {
			throw new IllegalArgumentException("Invalid Id");
		}

		if (name == null || name.length() > 20) {
			throw new IllegalArgumentException("Invalid Task Name");
		}

		if (desc == null || desc.length() > 50) {
			throw new IllegalArgumentException("Invalid Description");
		}
		
		this.taskId = id;
		this.name = name;
		this.description = desc;

	}
```


### Enhancements Made

1.	Created a helper class file, which contains the logic for generating default task names
2.	Modified the Task class file to call ‘DefaultTaskHelper.generateDefaulTaskName’ when a contact is selected.
3.	Updated the Task and TaskService class files to use ‘DefaultTaskHelper’ to set the default name when a new task is created without a specific name.
4.	Created a new test class, ‘DefaultTaskHelperTest’, and wrote unit tests that pass contact names to ‘generateDefaultTaskName’ and return the correct default task name.
5.	Updated the TaskServiceTest class file to test that when a new task is created with a selected contact, the default name is set correctly.
6.	Added a header to the code files, followed by updating code comments throughout the class files.

While the course assignment did not have a visual component requirement, the enhancements proposed in Module One were successful in aligning with communications that adapted to the audience, in this case customers, or contacts, and their context, setting an appointment using their default service preference. This enhancement also demonstrated the use of innovative techniques with the purpose of creating solutions that deliver value and accomplish industry-specific goals, such as operational efficiency and the ability to establish individual preferences. 
 

### Default Task Helper

```java
/*
 * File: Default Task Helper
 * Programmer Name: Domingo Polonia Jr
 * Created For: Copmuter Science Capstone CS499
 * Creation Date: February 2024
 * Date: 02-25-2024
 * Version: 1.1
 * Description: This Java class will contain the logic for generation the default task names
 */

 // A defaulttaskhelper package is created to separate the code into directories
package defaulttaskhelper;

// Import the associated class file it has a different package
import task.Task; 

public class DefaultTaskHelper {

	// The logic to generate and return the default task name
	public static String generateDefaultTaskName(String contactName) {
		return "Default Task for " + contactName; // Placeholder logic
		}

		// Method to create a Task object with smart defaults
		public static Task createTaskWithDefaults(String id, String contactName, String desc) {
			String defaultName = generateDefaultTaskName(contactName);
			return new Task(id, defaultName, desc); // Using the Task constructor
		}
}
```


### Enhanced Task Class File

```java
/*
 * File: Task Class
 * Programmer Name: Domingo Polonia Jr
 * Created For: Software Testing Automation and Quality Assurance CS320
 * Creation Date: December 2021
 * Course: CS499 Capstone
 * Date: 02-25-2024
 * Version: 2.2
 * Description: This Java class uses in-memory data structures to support storing tasks (no database required).
 * The Task Class requirements are: 
 * 1. The task object shall have a required unique task ID String that cannot be longer than 10 characters. 
 * 2. The task ID shall not be null and shall not be updatable.
 * 3. The task object shall have a required name String field that cannot be longer than 20 characters. 
 * 4. The name field shall not be null. 
 * 5. The task object shall have a required description String field that cannot be longer than 50 characters. 
 * 6. The description field shall not be null.
 */

package task;

// Import the DefaultTaskHelper class
import defaulttaskhelper.DefaultTaskHelper;

public class Task {

	// Initialize the variables to be used in the constructor and mutator/accessor methods
	private String taskId;
	private String name;
	private String description;

	/*
	 * Our constructor with its parameters and conditionals set to the 
	 * specifications in the requirements doc. Then assigning the values 
	 * if the conditional statements pass.
	 */

	/*
     * Modified constructor to include logic for setting a default name using
     * DefaultTaskHelper when name is not provided.
     * Original parameters and conditionals set to the specification requirements
	 * remain and the values are assigned if the conditional statements pass.
     */
	
	 public Task(String id, String name, String desc, String contactName) { // Added contactName parameter

        if (id == null || id.length() > 10) {
            throw new IllegalArgumentException("Invalid Id");
        }

        // Check if name is provided, else use DefaultTaskHelper to generate it
        if (name == null || name.isEmpty()) {
            this.name = DefaultTaskHelper.generateDefaultTaskName(contactName); // Generate default name based on contact
        } else if (name.length() > 20) {
            throw new IllegalArgumentException("Invalid Task Name");
        } else {
            this.name = name;
        }
// No changes to remaining code
```


### Lessons Learned

TBD


### Skills and Abilities Showcased

1.	
2.	
3.	


### Course Outcomes Demonstrated

### Demonstrating an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals (software engineering/design/database) by:

1.	Using smart default logic to improve the overall user experience.
2.	Creating a helper class to implement the smart default functionality and allow for developer collaboration and configuration management.
3.	Integrating the smart default logic into the task creation form, using the contact name as a parameter for the task input.

Original and enhanced technical files can be found in the course repository [CS320 Software Automation and Quality Assurance]([https://github.com/dpoloniajr/CS-320-Software-Testing-Automation-and-QA]).
