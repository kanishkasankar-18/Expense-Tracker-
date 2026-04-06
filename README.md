# Expense-Tracker-
The Expense Tracker is a simple Command Line Interface (CLI) application built using Python that helps users manage their daily expenses efficiently. This project allows users to record, view, and calculate their spending, making it easier to track financial habits.
import os

FILE_NAME = "expenses.txt"

# Add expense
def add_expense():
    name = input("Enter expense name: ")
    amount = input("Enter amount: ")

    with open(FILE_NAME, "a") as file:
        file.write(f"{name},{amount}\n")

    print("✅ Expense added successfully!\n")


# View all expenses
def view_expenses():
    if not os.path.exists(FILE_NAME):
        print("⚠️ No expenses found.\n")
        return

    with open(FILE_NAME, "r") as file:
        expenses = file.readlines()

    if not expenses:
        print("⚠️ No expenses recorded.\n")
        return

    print("\n📊 Your Expenses:")
    for expense in expenses:
        name, amount = expense.strip().split(",")
        print(f"- {name}: ₹{amount}")
    print()


# Calculate total
def total_expense():
    if not os.path.exists(FILE_NAME):
        print("⚠️ No expenses found.\n")
        return

    total = 0
    with open(FILE_NAME, "r") as file:
        for line in file:
            try:
                name, amount = line.strip().split(",")
                total += float(amount)
            except:
                continue

    print(f"\n💰 Total Expense: ₹{total}\n")


# Main menu
def main():
    while True:
        print("==== Expense Tracker ====")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Total Expense")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            add_expense()
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            total_expense()
        elif choice == "4":
            print("👋 Goodbye!")
            break
        else:
            print("❌ Invalid choice\n")


if __name__ == "__main__":
    main()