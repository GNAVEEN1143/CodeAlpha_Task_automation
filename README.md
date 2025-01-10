# CodeAlpha_Task_automation

import os
import shutil
from datetime import datetime

# Define the source directory containing the files to organize
source_directory = r'C:\\Users\\navee\\OneDrive\\Documents\\\Newfolder'  # Use the correct source folder path
destination_directory = r'C:\\Users\\\navee\\OneDrive\\Documents\\New'

# Function to check if the source directory exists
def check_directory(directory):
    if not os.path.exists(directory):
        print(f"Error: The directory '{directory}' does not exist.")
        return False
    elif not os.path.isdir(directory):
        print(f"Error: The path '{directory}' is not a valid directory.")
        return False
    return True

# Function to create folder structure based on file extension or modification date
def create_folders(file_path, criteria):
    if criteria == 'extension':
        file_extension = os.path.splitext(file_path)[1].lower()[1:]  # Get file extension (without dot)
        folder_name = file_extension if file_extension else 'others'
    elif criteria == 'modification_date':
        mod_time = os.path.getmtime(file_path)
        mod_date = datetime.fromtimestamp(mod_time).strftime('%Y-%m-%d')
        folder_name = mod_date
    else:
        raise ValueError("Invalid criteria. Use 'extension' or 'modification_date'.")

    target_folder = os.path.join(destination_directory, folder_name)

    if not os.path.exists(target_folder):
        os.makedirs(target_folder)

    return target_folder

def move_file(file_path, target_folder):
    try:
        shutil.move(file_path, target_folder)
        print(f"Moved: {file_path} -> {target_folder}")
    except Exception as e:
        print(f"Error moving file {file_path}: {e}")

def organize_files(criteria='extension'):
    if not check_directory(source_directory):
        return
    
    for file_name in os.listdir(source_directory):
        file_path = os.path.join(source_directory, file_name)

        if os.path.isdir(file_path):
            continue

        target_folder = create_folders(file_path, criteria)
        move_file(file_path, target_folder)

if __name__ == "__main__":
    organize_files(criteria='extension')

OUYPUT:

![Screenshot 2025-01-10 183420](https://github.com/user-attachments/assets/aa06c938-3678-4e90-a736-80d8670b2ed2)
