# SchoolSystemDatabase
A complete database design in SSMS for managing school operations, including student records, faculty schedules, courses, grades, and multi-school support. Built with scalability, efficiency, and accuracy in mind.
### Key Use Cases:
- Student Management:
Store and manage student personal details, academic records, and GPA calculations.
- Course and Enrollment Management:
Schedule courses and assign them to specific departments, faculty, and semesters.
Handle student enrollment and registration processes.
- Faculty and Staff Management:
Manage faculty data, including contact information, schedules, and assigned courses.
- Academic Reporting:
Generate transcripts, GPA reports, and department performance summaries.
### Key Functionalities
- Database Design Principles: Third Normal Form (3NF), data integrity, and relationship management
- Automated GPA Calculation: Calculate and update student GPAs after each semester.
- Course Management: Register, drop, and schedule courses.
- Faculty Schedules: Track which courses faculty teach and when.
### ER Diagram Overview
![image](https://github.com/user-attachments/assets/0c4b4957-e667-4895-af11-a736399f2d76)
### Queries run and results
``` 
SELECT
	TitleName, CONCAT(FirstName,' ', LastName) AS 'Faculty Name', Office, CourseName, RoomNumber,
	CASE 
        WHEN s.Fall = 1 THEN 'x'
        ELSE ''
    END AS Fall,
	CASE 
        WHEN s.[Winter/Spring] = 1 THEN 'x'
        ELSE ''
    END AS 'Winter/Spring',
	CASE 
        WHEN s.FullSummer = 1 THEN 'x'
        ELSE ''
    END AS 'Full Summer'
FROM	
	FacultyList fl
INNER JOIN
	FacultyCourses fc on fl.FacultyID = fc.FacultyID
INNER JOIN
	CourseCatalogue cc on fc.CourseID = cc.CourseID
INNER JOIN
	Semesters s on s.CourseID = cc.CourseID
INNER JOIN
	CourseSchedule cs on cc.CourseID = cs.CourseID
INNER JOIN
	CourseRegistration cr on cc.CourseID = cr.CourseID
WHERE
	fl.ClientID = 3;
```
![image](https://github.com/user-attachments/assets/d3dd3d21-2963-4099-9aa9-780bc266939c)
```
SELECT
	CourseName, DepartmentName, RoomNumber, CreditHours, NumberOfStudents,
	CASE 
        WHEN s.Fall = 1 THEN 'x'
        ELSE ''
    END AS Fall,
	CASE 
        WHEN s.[Winter/Spring] = 1 THEN 'x'
        ELSE ''
    END AS 'Winter/Spring',
	CASE 
        WHEN s.FullSummer = 1 THEN 'x'
        ELSE ''
    END AS 'Full Summer',
	CONCAT(fl.FirstName,' ',fl.LastName) AS 'Teacher Name'
FROM
	CourseCatalogue cc
INNER JOIN
	CourseRegistration cr on cc.CourseID = cr.CourseID
INNER JOIN
	Semesters s on s.CourseID = cr.CourseID
INNER JOIN
	CourseSchedule cs on cc.CourseID = cs.CourseID
INNER JOIN
	FacultyCourses fc on cc.CourseID = fc.CourseID
INNER JOIN
	FacultyList fl on fc.FacultyID = fl.FacultyID
WHERE
	cc.ClientID = 3 AND cs.[Current] = 1;
```
![image](https://github.com/user-attachments/assets/88707178-3de6-449b-8438-ae58a8a934c4)




