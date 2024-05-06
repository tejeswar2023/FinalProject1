import tkinter as tk
from tkinter import messagebox

def calculate():
    try:
        expression = entry.get()
        result = eval(expression)
        entry.delete(0, tk.END)
        entry.insert(tk.END, str(result))
    except Exception as e:
        messagebox.showerror("Error", "Invalid input")

def clear():
    entry.delete(0, tk.END)

def exit_app():
    window.destroy()

def add_text(text):
    entry.insert(tk.END, text)

def update_label(label, text):
    label.config(text=text)

window = tk.Tk()
window.title("Calculator")

# Creating entry widget
entry = tk.Entry(window)
entry.grid(row=0, column=0, columnspan=4)

# Creating buttons
buttons = [
    ('7', lambda: add_text('7')), ('8', lambda: add_text('8')), ('9', lambda: add_text('9')), ('/', lambda: add_text('/')),
    ('4', lambda: add_text('4')), ('5', lambda: add_text('5')), ('6', lambda: add_text('6')), ('*', lambda: add_text('*')),
    ('1', lambda: add_text('1')), ('2', lambda: add_text('2')), ('3', lambda: add_text('3')), ('-', lambda: add_text('-')),
    ('0', lambda: add_text('0')), ('.', lambda: add_text('.')), ('=', calculate), ('+', lambda: add_text('+'))
]

row, col = 1, 0
for btn_text, cmd in buttons:
    btn = tk.Button(window, text=btn_text, command=cmd)
    btn.grid(row=row, column=col, sticky="nsew", padx=3, pady=3)
    col += 1
    if col > 3:
        col = 0
        row += 1

# Adding labels
label1 = tk.Label(window, text="Label 1")
label1.grid(row=row, column=0)
label2 = tk.Label(window, text="Label 2")
label2.grid(row=row, column=1)
label3 = tk.Label(window, text="Label 3")
label3.grid(row=row, column=2)

# Adding callback functions to buttons
label1_btn = tk.Button(window, text="Update Label 1", command=lambda: update_label(label1, "Label 1 Updated"))
label1_btn.grid(row=row, column=3)
label2_btn = tk.Button(window, text="Update Label 2", command=lambda: update_label(label2, "Label 2 Updated"))
label2_btn.grid(row=row+1, column=0)
label3_btn = tk.Button(window, text="Update Label 3", command=lambda: update_label(label3, "Label 3 Updated"))
label3_btn.grid(row=row+1, column=1)

# Adding exit button
exit_btn = tk.Button(window, text="Exit", command=exit_app)
exit_btn.grid(row=row+1, column=2)

window.mainloop()
