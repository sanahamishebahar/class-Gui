# class-Gui

import tkinter as tk

#Parent Class
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

   def show_account(self):
        return f"Owner: {self.owner}\nBalance: {self.balance}"

  def deposit(self, amount):
        self.balance += amount


#Child Class
class SavingsAccount(BankAccount):

   def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
        else:
            print("Insufficient balance!")


#Parent Window
class BaseWindow:
    def __init__(self):
        self.window = tk.Tk()
        self.window.title("Bank App")
        self.window.geometry("350x250")


#Child Window
class BankWindow(BaseWindow):
    def __init__(self):
        super().__init__()

  tk.Label(self.window, text="Owner Name", fg = "pink").pack()

   self.owner_entry = tk.Entry(self.window)
        self.owner_entry.pack()

   tk.Label(self.window, text="Balance", fg = "pink").pack()

   self.balance_entry = tk.Entry(self.window)
        self.balance_entry.pack()

   tk.Button(
            self.window,
            text="Create Account",
            fg = "grey",
            command=self.create_account
        ).pack(pady=10)

   self.result_label = tk.Label(self.window, text="", fg = "pink")
        self.result_label.pack()

   self.window.mainloop()

   def create_account(self):
        owner = self.owner_entry.get()
        balance = float(self.balance_entry.get())

  account = SavingsAccount(owner, balance)

  self.result_label.config(text=account.show_account())


#Run Program
BankWindow()
