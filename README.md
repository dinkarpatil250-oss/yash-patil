Capstone Project: Hybrid Inventory Manager
Goal: Build a small inventory manager where the data layer is in C using structs + binary file storage, and the menu/UI is in C++ using classes + STL. Your data must persist after restart (saved in a file).

What you will build: A console app that stores inventory items in a binary file (example: inventory.dat) and lets the user perform basic CRUD operations.
Core idea: C handles file read/write and record updates, while C++ handles menu, input, sorting, and printing.
Minimum features you must implement:
Add item (store a new item with a unique ID)
View item by ID (find and display one item)
Update item (modify an existing record in the file)
Delete item (soft delete so it does not appear in views)
List all items (show all non-deleted items neatly)
Item data format (C struct):
int id
char name[40]
int quantity
float price
int is_deleted (0 = active, 1 = deleted)
Storage rules (C):
Use binary file storage with fread/fwrite
Update and delete must modify the correct record using fseek
Items marked is_deleted = 1 must not appear in view/list
C backend requirements (must expose only these functions):
int add_item(const Item item)*
int get_item(int id, Item out)*
int update_item(int id, const Item updated)*
int delete_item(int id)
int list_items(Item buffer, int max_items)*
Return 1 for success and 0 for failure for add/get/update/delete.
list_items returns the number of items copied into the buffer.
C++ layer requirements:
Create a class InventoryManager that calls the C functions.
Use at least two STL elements:
std::vector to hold items temporarily for listing
std::sort to sort items by id or name before printing
Menu requirement (C++):
1 Add item
2 View item
3 Update item
4 Delete item
5 List all
6 Exit
Input checks (keep it simple):
ID must be positive
Quantity must be 0 or more
Price must be 0 or more
Name must not be empty
If input is invalid, show a message and re-ask (do not crash).
Multi-file build requirement:
Your code must be split into multiple files and build using Make or CMake.
C files must compile as C, C++ files as C++, and link into one executable.
Suggested file structure:
include/inventory.h
src/inventory.c
src/InventoryManager.cpp
src/main.cpp
Makefile or CMakeLists.txt
README.md
Deliverables (submit one zip):
All source files in the structure above
Makefile or CMakeLists.txt
README.md with:
Build and run steps
5 short test cases you tried (written as bullet points)
Acceptance checks (must work):
Add 3 items, exit, run again, and List all still shows them.
Updating an item remains updated after restart.
Deleted items do not show in list or view.
Duplicate IDs are rejected.
