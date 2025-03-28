# bloco-de-notas-

import tkinter as tk
from tkinter import filedialog

def new_file():
    text.delete("1.0", tk.END)

def open_file():
    file_path = filedialog.askopenfilename(defaultextension=".txt", filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
    if file_path:
        with open(file_path, "r") as file:
            text.delete("1.0", tk.END)
            text.insert(tk.END, file.read())

def save_file():
    file_path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")])
    if file_path:
        with open(file_path, "w") as file:
            file.write(text.get("1.0", tk.END).strip())

# Configuração da interface gráfica
app = tk.Tk()
app.title("Bloco de Notas")

text = tk.Text(app, wrap="word")
text.pack(expand=True, fill="both")

menu_bar = tk.Menu(app)
file_menu = tk.Menu(menu_bar, tearoff=0)
file_menu.add_command(label="Novo", command=new_file)
file_menu.add_command(label="Abrir", command=open_file)
file_menu.add_command(label="Salvar", command=save_file)
menu_bar.add_cascade(label="Arquivo", menu=file_menu)

app.config(menu=menu_bar)
app.mainloop()
