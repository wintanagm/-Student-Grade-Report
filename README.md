# -Student-Grade-Report\
"""
Project 1 Final Draft
Title : Student Grade Report
Group Members: Wintana Medhanie,Sofiya Sherif ,and Brook Alemu
4 / 14 / 2024
"""
import csv
from class_file import Student


def read_students_from_file(student_grades_file):
	scores_list = []# a list that stores student exam scores
	students_dict={} # a dict that stores student instances 
	with open(student_grades_file, 'r') as file:
		reader = csv.reader(file)
		first_row = True
		for row in reader:
			#Skip the first row with column names
			if first_row:
				first_row = False
				continue
			name = row[0]
			# Convert score strings into floats
			scores = [float(cell) for cell in row[1:]]
			scores_list.append(scores)
			exam1_weighted = scores[0]* 0.20
			exam2_weighted = scores[1]* 0.20
			exam3_weighted = scores[2]* 0.20
			fin_weighted = scores[3]* 0.40
			score = (exam1_weighted + exam2_weighted + exam3_weighted + fin_weighted) 
			# Create Student instance and add it to the dictionary
			student = Student(name, score)
			student.add_grade()
			students_dict[name] = student
		return students_dict
def display_students_info(students_dict):
    for student_name, student in students_dict.items():
        print(student.display_info())
welcome_message = "Welcome to Student Grade Report!"
smiley_face = r"""
     *********
   *************
  ***   ***    ***
 ***  0  *  0   ***
***             ***
***   \_____/   ***
 ***           ***
  ***         ***
    ************
      ********
"""
print(welcome_message)
print(smiley_face)
user_name = input("Enter your name: ")
print(f"Hello, {user_name}.")
student_grades_file = input("Enter student_grades.csv to see the average grade of students in CIS 121 class: \n")
students_dict = read_students_from_file(student_grades_file)
print("\n")
display_students_info(students_dict)
print("\n")
