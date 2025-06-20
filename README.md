# ai-agent
File: todo_manager.py

Simple to-do list manager

todo_list = []

def add_task(task): todo_list.append(task) return f"Task added: {task}"

def view_tasks(): if not todo_list: return "Your to-do list is empty." return "\n".join([f"{i+1}. {task}" for i, task in enumerate(todo_list)])

def remove_task(index): try: removed = todo_list.pop(index - 1) return f"Removed task: {removed}" except IndexError: return "Invalid task number."

File: assistant.py

import datetime import wikipedia from todo_manager import add_task, view_tasks, remove_task

def get_time(): now = datetime.datetime.now() return f"The current time is {now.strftime('%I:%M %p')}"

def get_date(): today = datetime.date.today() return f"Today's date is {today.strftime('%B %d, %Y')}"

def search_wikipedia(query): try: result = wikipedia.summary(query, sentences=2) return result except: return "Sorry, I couldn't find anything on Wikipedia."

def handle_input(user_input): user_input = user_input.lower()

if "time" in user_input:
    return get_time()
elif "date" in user_input:
    return get_date()
elif "add" in user_input and "to-do" in user_input:
    task = user_input.replace("add", "").replace("to-do", "").strip()
    return add_task(task)
elif "show to-do" in user_input:
    return view_tasks()
elif "remove" in user_input and "to-do" in user_input:
    try:
        num = int(user_input.split()[-1])
        return remove_task(num)
    except:
        return "Please specify a valid task number."
elif "search" in user_input:
    topic = user_input.replace("search", "").strip()
    return search_wikipedia(topic)
else:
    return "Sorry, I didn't understand that."

File: main.py

from assistant import handle_input

print("Welcome to the Smart Personal Assistant Agent!") print("Type 'exit' to quit.\n")

while True: user_input = input("You: ") if user_input.lower() in ["exit", "quit"]: print("Assistant: Goodbye!") break response = handle_input(user_input) print("Assistant:", response)
