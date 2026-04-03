from datetime import date
import json as js

date = str(date.today())


# Data List
categories = ["Junk Food", "healthy food", "Cloths", "Furnitures", "t.Products"]
My_expense = {date:{"category":[], "expense":[]}}

# Option or Functions

def availabe_categories():
    availabe_cat = []
    
    for count, cat in zip(range(1, (len(categories)+1)), categories):
        availabe_cat.append(f"{count}. {cat}")
    
    return availabe_cat
        

def add_expense(category, expense):
    
        location = My_expense[date]
        location["category"].append(category)
        location["expense"].append(expense)
        
def show_all_expense():
    all_expense = []
    
    for dt in My_expense.keys():
        category = My_expense[dt]["category"]
        expense = My_expense[dt]["expense"]
        
        """
        zip() function make the pair of multiple list and reduce
        """
        

        for cat, exp in zip(category, expense):
            all_expense.append(f"{dt:^12}{cat:^11}{exp:^12}")
    return all_expense
        
        
def total_expense():
    
    total_exp = 0
    days = len(My_expense.keys())
    
    for dt in My_expense.keys():
        for exp in My_expense[dt]["expense"]:
            total_exp += exp
            result = f"{"-" * 32}\nTotal Expense of {days} days: {total_exp}\n{"-" * 32}"
            
    return result

def monthly_expense(month):

    monthly_exp =[]
    avialabe_month = []
    
    for dt in My_expense.keys():
        
        category = My_expense[dt]["category"]
        expense = My_expense[dt]["expense"]

        for cat, exp in zip(category, expense):
            if dt[6] == month:
                monthly_exp.append(f"{dt:^12}{cat:^11}{exp:^12}")
                avialabe_month.append(dt[6])        
                
    return monthly_exp, avialabe_month
        
            
def specific_category_expense(category):
    
    for dt in My_expense.keys():
        
        specific_category = [f"\n{"-" *36}\n{category:^12} \n{"-" *36}\n{"Date":^12}{"Category":^11}{"Expense":^12}\n{"_" *36}"]
        
        categories = My_expense[dt]["category"]
        expenses = My_expense[dt]["expense"]
                
        for cat, exp in zip(categories, expenses):
            if cat == category:
                specific_category.append(f"{dt:^12}{cat:^11}{exp:^12}")
                
    return specific_category
         

def delete_expense(date, category):
    
    categories = My_expense[date]["category"]
    expenses = My_expense[date]["expense"]
    
    for cat, exp in zip(categories, expenses):
        if cat == category:
            del(categories[categories.index(cat)], expenses[expenses.index(exp)])
            message = "Expenses deleted successfully."
        else:
            message = "Expense not exist!"
            
    return message

def load_expenses(file):
    with open(file, "r") as fl:
        My_expense.update(js.load(fl))

def save_expenses(file):
    with open(file, "w") as fl:
        js.dump(My_expense, fl, indent= 4)



def main():
    with open("expense.json", "r+") as file:
        file.seek(0,2)
        if file.tell() != 0:
            load_expenses("expense.json")
            
    try: 
        while True:
            print(f"\n{"_" * 32}\n {"Personal Expense Tracker":<22}\n{"-" * 32}\n1. Add Expense \n2. Show all Expenses \n3. Total Expense \n4. Monthly Expense \n5. Specific Category Expense \n6. Delete Expense \n7. Exit\n{"-" * 32}")
            user_input = int(input("What you want to do: "))
            stop = False
            
            if user_input == 1:
                while True:
                    print(f"\n{"_" *36}\n Availabe Categories\n{"-" *36}")
                    for availabe_cat in availabe_categories():
                        print(availabe_cat)
                    print(f"{"-" * 32}\n")
                    
                    user_category = int(input("Choose Category: "))
                    for count, cat in zip(range(1, (len(categories)+1)), categories):
                        
                        if user_category == count:
                            user_category_exp = int(input("Enter Expense: "))
                            add_expense(category=cat, expense=user_category_exp)
                            save_expenses("expense.json")

                            add_more = input("Want to Add more Expense y/n: ").lower()
                            if add_more == "n":
                                stop = True
                                break
                            
                        elif (user_category > len(categories)) or (user_category == 0):
                            print("\rCategory not Available!", end="" )
                            
                    if stop: # Agar stop = True hai 
                        break
            elif user_input == 2:
                print(f"\n{"-" *36}\n{"All Expenses":^12}\n{"-" *36}\n{"Date":^12}{"Category":^11}{"Expense":^12}\n{"_" *36}")
                all_expense = show_all_expense()
                for i in all_expense:
                    print(i)
                print(f"{"-" *36}\n")
                
            elif user_input == 3:
                total_exp = total_expense()
                print(total_exp)
            
            elif user_input == 4:
                user_month = input("\nEnter Month in digits: ")
                monthly_exp, availabe_month = monthly_expense(month= user_month)
                
                if user_month in availabe_month:
                    
                    print(f"\n{"-" *36}\n{"Montly Expenses":^12}\n{"-" *36}\n{"Date":^12}{"Category":^11}{"Expense":^12}\n{"_" *36}")
                    for i in monthly_exp:
                        print(i)
                    print(f"{"-" *36}\n")
                    
                else:
                    print("Monthly data not availabe!")
            
            elif user_input == 5:
                print(f"{"_" *36}\n Availabe Categories\n{"-" *36}")
                for available_cat in availabe_categories():
                    print(available_cat)
                print(f"{"-" *36}\n")
            
                filter_cat = int(input("Choose Category: "))
                
                for dt in My_expense.keys():
                
                    for count, cat in zip(range(1, (len(categories)+1)), categories):
                        if filter_cat == count and cat in My_expense[dt]["category"]:
                            for i in specific_category_expense(cat):
                                print(i)
                            print("-" *36, "\n")
                        elif (filter_cat > len(categories)) or (filter_cat == 0):
                            print("\rCategory not Available!", end="" )
                            
                        elif cat not in My_expense[dt]["category"]:
                            print(f"\rExpense not added yet, in this category.", end="")
                
                        
            elif user_input == 6:
                for available_cat in availabe_categories():
                    print(available_cat)
            
                del_cat = int(input("Choose Category: "))
                
                for count, cat in zip(range(1, (len(categories)+1)), categories):
                    if del_cat == count:
                        delete_expense(date=date, category=cat)
                        save_expenses("expense.json")
                        print(f"{cat} deleted successfully.")
                        
            else:
                break
    except ValueError:
        print("!Invalid Choice!: (Choose by Numbering.)")

if __name__ == "__main__":           
    main()
