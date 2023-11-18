```python
# main.py
import tkinter as tk
from tkinter import messagebox
from game_logic import GuessTheNumberGame

class GuessTheNumberApp:
    def __init__(self, master):
        self.master = master
        self.master.title("Гра 'Вгадай число'")
        
        self.game = GuessTheNumberGame()

        self.label = tk.Label(master, text="Вгадайте число від 1 до 100:")
        self.label.pack(pady=10)
        
        self.entry = tk.Entry(master)
        self.entry.pack(pady=10)
        
        self.button = tk.Button(master, text="Перевірити", command=self.check_guess)
        self.button.pack(pady=10)
        
        self.reset_button = tk.Button(master, text="Нова гра", command=self.reset_game)
        self.reset_button.pack(pady=10)

    def check_guess(self):
        user_guess = self.entry.get()
        
        try:
            guess = int(user_guess)
        except ValueError:
            messagebox.showerror("Помилка", "Будь ласка, введіть ціле число.")
            return
        
        result = self.game.check_guess(guess)
        messagebox.showinfo("Результат", result)

    def reset_game(self):
        self.game.start_game()
        self.label.config(text="Вгадайте число від 1 до 100:")
        self.entry.delete(0, 'end')

if __name__ == "__main__":
    root = tk.Tk()
    app = GuessTheNumberApp(root)
    root.mainloop()

