# To-do-list
import tkinter as tk
from tkinter import messagebox, simpledialog

# Function to add a task to the listbox
def add_task():
    task = task_entry.get()
    if task:
        listbox.insert(tk.END, task)
        task_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Input Error", "Please enter a task.")

# Function to delete a selected task from the listbox
def delete_task():
    try:
        selected_task_index = listbox.curselection()[0]
        listbox.delete(selected_task_index)
    except IndexError:
        messagebox.showwarning("Selection Error", "Please select a task to delete.")

# Function to edit a selected task
def edit_task():
    try:
        selected_task_index = listbox.curselection()[0]
        current_task = listbox.get(selected_task_index)
        new_task = simpledialog.askstring("Edit Task", f"Edit task (current: {current_task}):")
        if new_task:
            listbox.delete(selected_task_index)
            listbox.insert(selected_task_index, new_task)
    except IndexError:
        messagebox.showwarning("Selection Error", "Please select a task to edit.")

# Function to clear all tasks from the listbox
def clear_tasks():
    if messagebox.askyesno("Confirm Clear", "Are you sure you want to clear all tasks?"):
        listbox.delete(0, tk.END)

# GUI setup
root = tk.Tk()
root.title("To-Do List with Tkinter")

frame = tk.Frame(root)
frame.pack(pady=10)

task_label = tk.Label(frame, text="Task:")
task_label.pack(side=tk.LEFT)
task_entry = tk.Entry(frame, width=40)
task_entry.pack(side=tk.LEFT)

add_button = tk.Button(root, text="Add Task", command=add_task)
add_button.pack(pady=10)

listbox = tk.Listbox(root, width=50, height=15)
listbox.pack(pady=10)

delete_button = tk.Button(root, text="Delete Task", command=delete_task)
delete_button.pack(pady=5)

edit_button = tk.Button(root, text="Edit Task", command=edit_task)
edit_button.pack(pady=5)

clear_button = tk.Button(root, text="Clear All Tasks", command=clear_tasks)
clear_button.pack(pady=5)

root.mainloop()
