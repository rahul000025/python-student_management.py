# python-student_management.py
The Student Management System provides the following functionalities:1. Add Student  Allows user to add new student record including:  Roll Number  Name  Course 2. View Students  Displays all student records stored in the file. 3. Search Student  Searches a student record using roll number. 4. Delete Student  Deletes a student record from the file.

code

def add_student():
    roll = input("Enter Roll No: ")
    name = input("Enter Name: ")
    course = input("Enter Course: ")

    with open("students.txt", "a") as f:
        f.write(f"{roll},{name},{course}\n")

    print("Student Added Successfully!")


def view_students():
    try:
        with open("students.txt", "r") as f:
            data = f.readlines()
            if not data:
                print("No students found!")
            else:
                print("\n--- Student List ---")
                for line in data:
                    roll, name, course = line.strip().split(",")
                    print(f"Roll: {roll} | Name: {name} | Course: {course}")
    except FileNotFoundError:
        print("No record file found!")


def search_student():
    roll = input("Enter Roll No to search: ")
    found = False

    try:
        with open("students.txt", "r") as f:
            for line in f:
                r, name, course = line.strip().split(",")
                if r == roll:
                    print("\nStudent Found!")
                    print(f"Roll: {r}")
                    print(f"Name: {name}")
                    print(f"Course: {course}")
                    found = True
                    break
        if not found:
            print("Student not found!")
    except FileNotFoundError:
        print("No record file found!")


def delete_student():
    roll = input("Enter Roll No to delete: ")
    found = False
    new_data = []

    try:
        with open("students.txt", "r") as f:
            for line in f:
                r, name, course = line.strip().split(",")
                if r != roll:
                    new_data.append(line)
                else:
                    found = True

        with open("students.txt", "w") as f:
            for line in new_data:
                f.write(line)

        if found:
            print("Student deleted successfully!")
        else:
            print("Student not found!")

    except FileNotFoundError:
        print("No record file found!")


while True:
    print("\n==== Student Management System ====")
    print("1. Add Student")
    print("2. View Students")
    print("3. Search Student")
    print("4. Delete Student")
    print("5. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        add_student()
    elif choice == "2":
        view_students()
    elif choice == "3":
        search_student()
    elif choice == "4":
        delete_student()
    elif choice == "5":
        print("Thank you! Exiting...")
        break
    else:
        print("Invalid choice! Try again.")
