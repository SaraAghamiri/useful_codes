🧠 What problem does this code solve?
Imagine you have a giant digital cabinet (a folder) full of other folders and files — kind of like a filing cabinet full of drawers, each with papers and more folders inside.
📂 Problem:
It’s hard to see everything inside — all the folders, subfolders, and files — especially if it’s really big. You’d have to open each folder one by one to figure out what’s inside.
#✅ What this code does:
# This code is like a robot helper that walks through the entire cabinet and writes down everything it sees — folders, files, what’s inside each one — and makes a nice, clean list in a Word document.
#📝 At the end, you get a document (like a report) that shows all the folders and files in a bullet-point list, showing what’s inside what. You don’t have to explore it yourself — the robot did it for you!
#💡 Why it's useful:
# This helps you:
# Understand how your folders are organized
#  Share that structure with someone else
#  Keep a backup of how things were arranged



# cd to your directory
#---------
#bash:
#nano file.py


#Python:

import os
from docx import Document

# === CONFIGURATION ===
# Set this to the folder you want to analyze
base_path = '/yor directory'  # or '.' if already in folder
output_docx = 'folder_structure.docx'

# === STEP 1: Create Word Document ===
doc = Document()
doc.add_heading('Folder and File Structure', level=1)

# === STEP 2: Walk Through Folder ===
def add_folder_contents(doc, path, indent=0):
    prefix = '    ' * indent + '• '
    items = sorted(os.listdir(path))
    for item in items:
        item_path = os.path.join(path, item)
        doc.add_paragraph(f"{prefix}{item}")
        if os.path.isdir(item_path):
            add_folder_contents(doc, item_path, indent + 1)

add_folder_contents(doc, base_path)

# === STEP 3: Save Word File ===
doc.save(output_docx)
print(f"Saved as {output_docx}")




#bash:
#Python file.py 
#--------

#bash
#>> python -m venv venv_docx
#>> source venv_docx/bin/activate
#>> pip install python-docx
#>> python make_doc.py
