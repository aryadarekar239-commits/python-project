# python-project

# Student Record and Academic Management System
# Using String, List, Tuple, Set and Dictionary

students = {}

# Set stores unique subject names
subjects = {"Python", "Mathematics", "Physics"}


def calculate_grade(percentage):    #def means(define any function)
    if percentage >= 90:
        return "A+"
    elif percentage >= 80:
        return "A"
    elif percentage >= 70:
        return "B"
    elif percentage >= 60:
        return "C"
    elif percentage >= 40:
        return "D"
    else:
        return "F"


def add_student():
    print("\n--- Add Student Record ---")

    roll = input("Enter roll number: ").strip()

    if not roll:
        print("Roll number cannot be empty.")
        return

    if roll in students:
        print("This roll number already exists.")
        return

    name = input("Enter student name: ").strip().title()

    if not name:
        print("Student name cannot be empty.")
        return

    course = input("Enter course name: ").strip().upper()

    if not course:
        print("Course name cannot be empty.")
        return

    marks_list = []

    for subject in sorted(subjects):
        while True:
            try:
                mark = float(input(f"Enter marks in {subject} (0-100): "))

                if 0 <= mark <= 100:
                    marks_list.append(mark)
                    break
                else:
                    print("Marks must be between 0 and 100.")

            except ValueError:
                print("Please enter a valid number.")

    # Tuple stores marks after entry
    marks_tuple = tuple(marks_list)

    total = sum(marks_tuple)
    percentage = total / len(marks_tuple)
    grade = calculate_grade(percentage)

    # Dictionary stores each student's details
    students[roll] = {
        "name": name,
        "course": course,
        "marks": marks_tuple,
        "total": total,
        "percentage": percentage,
        "grade": grade
    }

    print("Student record added successfully!")


def display_student(roll, student):
    print("\n------------------------------")
    print("Roll Number :", roll)
    print("Name        :", student["name"])
    print("Course      :", student["course"])

    print("Subject-wise Marks:")
    for subject, mark in zip(sorted(subjects), student["marks"]):
        print(f"{subject}: {mark:g}")

    print("Total Marks :", f"{student['total']:g} / 300")
    print("Percentage  :", f"{student['percentage']:.2f}%")
    print("Grade       :", student["grade"])
    print("------------------------------")


def display_all_students():
    print("\n--- All Student Records ---")

    if not students:
        print("No student records found.")
        return

    for roll, student in students.items():
        display_student(roll, student)


def search_student():
    print("\n--- Search Student ---")
    roll = input("Enter roll number to search: ").strip()

    if roll in students:
        display_student(roll, students[roll])
    else:
        print("Student record not found.")


def update_marks():
    print("\n--- Update Student Marks ---")
    roll = input("Enter roll number: ").strip()

    if roll not in students:
        print("Student record not found.")
        return

    student = students[roll]
    marks_list = list(student["marks"])

    print("Subjects:", ", ".join(sorted(subjects)))

    for index, subject in enumerate(sorted(subjects)):
        while True:
            try:
                mark = float(
                    input(f"Enter new marks for {subject} (0-100): ")
                )

                if 0 <= mark <= 100:
                    marks_list[index] = mark
                    break
                else:
                    print("Marks must be between 0 and 100.")

            except ValueError:
                print("Please enter a valid number.")

    # Convert the updated list back into a tuple
    marks_tuple = tuple(marks_list)

    total = sum(marks_tuple)
    percentage = total / len(marks_tuple)
    grade = calculate_grade(percentage)

    student["marks"] = marks_tuple
    student["total"] = total
    student["percentage"] = percentage
    student["grade"] = grade

    print("Marks updated successfully!")


def delete_student():
    print("\n--- Delete Student Record ---")
    roll = input("Enter roll number to delete: ").strip()

    if roll in students:
        del students[roll]
        print("Student record deleted successfully!")
    else:
        print("Student record not found.")


def display_subjects():
    print("\n--- Available Subjects ---")

    for subject in sorted(subjects):
        print("-", subject)

    print("Total unique subjects:", len(subjects))


def main():
    while True:
        print("\n===== STUDENT MANAGEMENT SYSTEM =====")
        print("1. Add Student")
        print("2. Display All Students")
        print("3. Search Student")
        print("4. Update Student Marks")
        print("5. Delete Student")
        print("6. Display Subjects")
        print("7. Exit")

        choice = input("Enter your choice (1-7): ").strip()

        if choice == "1":
            add_student()
        elif choice == "2":
            display_all_students()
        elif choice == "3":
            search_student()
        elif choice == "4":
            update_marks()
        elif choice == "5":
            delete_student()
        elif choice == "6":
            display_subjects()
        elif choice == "7":
            print("Thank you for using the Student Management System!")
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 7.")


