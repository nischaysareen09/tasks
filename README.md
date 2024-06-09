import os

# Function to list existing tasks
def list_tasks():
  """
  Prints existing tasks stored in a file.
  """
  if not os.path.exists("tasks.txt"):
    print("No tasks found.")
    return
  with open("tasks.txt", "r") as f:
    tasks = f.readlines()
    if tasks:
      print("Your Tasks:")
      for i, task in enumerate(tasks):
        print(f"{i+1}. {task.strip()}")
    else:
      print("No tasks found in the list.")

# Function to add a new task
def add_task(task):
  """
  Adds a new task to the task list file.
  """
  with open("tasks.txt", "a") as f:
    f.write(f"{task}\n")
  print(f"Task '{task}' added successfully!")

# Function to remove a task
def remove_task(task_index):
  """
  Removes a task from the task list file based on its index.
  """
  if not os.path.exists("tasks.txt"):
    print("No tasks found to remove.")
    return
  tasks = []
  with open("tasks.txt", "r") as f:
    tasks = f.readlines()
  if task_index < 1 or task_index > len(tasks):
    print(f"Invalid task index: {task_index}")
    return
  tasks.pop(task_index - 1)
  with open("tasks.txt", "w") as f:
    f.writelines(tasks)
  print(f"Task #{task_index} removed successfully!")

# Main program flow
if __name__ == "__main__":
  import argparse

  # Define command-line arguments
  parser = argparse.ArgumentParser(description="Simple Task Manager")
  parser.add_argument("command", choices=["list", "add", "remove"], help="Command to execute (list, add, or remove)")
  parser.add_argument("-t", "--task", help="Task description (for add command)")
  parser.add_argument("-i", "--index", type=int, help="Task index (for remove command)")
  args = parser.parse_args()

  # Execute commands based on user input
  if args.command == "list":
    list_tasks()
  elif args.command == "add":
    if not args.task:
      print("Please provide a task description with the -t argument.")
    else:
      add_task(args.task)
  elif args.command == "remove":
    if not args.index:
      print("Please provide a task index with the -i argument.")
    else:
      remove_task(args.task_index)
  else:
    print("Invalid command. Use 'list', 'add', or 'remove'.")
