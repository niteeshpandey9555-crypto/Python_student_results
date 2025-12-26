import os

DATA_FILE = os.path.join(os.path.dirname(__file__), "..", "data", "students.txt")

def show_menu():
    print("
===== Student Result Management =====")
    print("1. Add student")
    print("2. View all students")
    print("3. Search by roll number")
    print("4. Exit")

def add_student():
    roll = input("Enter roll number: ")
    name = input("Enter name: ")
    marks = input("Enter marks: ")

    with open(DATA_FILE, "a", encoding="utf-8") as f:
        f.write(f"{roll},{name},{marks}
")

    print("Student record added successfully!")

def view_students():
    if not os.path.exists(DATA_FILE):
        print("No records found.")
        return

    with open(DATA_FILE, "r", encoding="utf-8") as f:
        lines = f.readlines()

    if len(lines) == 0:
        print("No records found.")
        return

    print("
Roll\tName\tMarks")
    for line in lines:
        roll, name, marks = line.strip().split(",")
        print(f"{roll}\t{name}\t{marks}")

def search_student():
    roll_search = input("Enter roll number to search: ")

    if not os.path.exists(DATA_FILE):
        print("No records found.")
        return

    with open(DATA_FILE, "r", encoding="utf-8") as f:
        for line in f:
            roll, name, marks = line.strip().split(",")
            if roll == roll_search:
                print(f"Found: Roll={roll}, Name={name}, Marks={marks}")
                return

    print("Student not found.")

def main():
    while True:
        show_menu()
        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            add_student()
        elif choice == "2":
            view_students()
        elif choice == "3":
            search_student()
        elif choice == "4":
            print("Exiting...")
            break
        else:
            print("Invalid choice! Please try again.")

if __name__ == "__main__":
    main()
