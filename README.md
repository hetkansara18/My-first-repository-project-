# My-first-repository-project 
#This is a Python project to manage files and folders using OOP and Decorators.

import os

# The Decorator Function (Logger)
def log_action(func):
    "Decorator that logs the start and end of a function call"
    def wrapper(*args, **kwargs):
        print(f"--- [LOG]: Execution Started: {func.__name__} ---")
        result = func(*args, **kwargs)  # Executing the original function
        print(f"--- [LOG]: Execution Finished: {func.__name__} ---\n")
        return result
    return wrapper

# The Main Class using OOP
class ProjectManager:
    def __init__(self, project_name):
        self.project_name = project_name
        print(f"Initializing Project Manager for: {self.project_name}\n")

    @log_action
    def create_directories(self, folder_list):
        "Creates multiple directories based on a provided list"
        for folder in folder_list:
            if not os.path.exists(folder):
                os.makedirs(folder)
                print(f"SUCCESS: Created folder '{folder}'")
            else:
                print(f"SKIPPED: Folder '{folder}' already exists.")

    @log_action
    def list_project_files(self, directory="."):
        """Lists all files and folders in the specified path."""
        try:
            items = os.listdir(directory)
            print(f"Contents of '{directory}': {items}")
            return items
        except FileNotFoundError:
            print(f"ERROR: The path '{directory}' was not found.")

# Running the Code
if __name__ == "__main__":
    # Create an instance of the class
    manager = ProjectManager(project_name="Advanced_Python_Project")
    
    # Define a list of folders to create
    required_folders = ['data', 'src', 'logs', 'output']
    
    # Execute methods
    manager.create_directories(required_folders)
    manager.list_project_files()

