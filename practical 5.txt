class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None


# 1. Insert
def insert(root, key):
    if root is None:
        return Node(key)

    if key == root.data:
        print("Duplicate entry!")
    elif key < root.data:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)

    return root


# 2. Delete
def delete(root, key):
    if root is None:
        return None

    if key < root.data:
        root.left = delete(root.left, key)

    elif key > root.data:
        root.right = delete(root.right, key)

    else:
        if root.left is None:
            return root.right

        if root.right is None:
            return root.left

        temp = root.right
        while temp.left is not None:
            temp = temp.left

        root.data = temp.data
        root.right = delete(root.right, temp.data)

    return root


# 3. Search
def search(root, key):
    if root is None:
        return False

    if key == root.data:
        return True

    if key < root.data:
        return search(root.left, key)

    return search(root.right, key)


# 4. Display Tree
def display(root, level=0, prefix="Root: "):
    if root is not None:
        print(" " * (level * 4) + prefix + str(root.data))
        display(root.left, level + 1, "L--- ")
        display(root.right, level + 1, "R--- ")


# Main Program
root = None

while True:
    print("\n===== BINARY SEARCH TREE =====")
    print("1. Insert")
    print("2. Delete")
    print("3. Search")
    print("4. Display Tree")
    print("0. Exit")

    choice = int(input("Enter your choice: "))

    if choice == 1:
        n = int(input("How many values to insert? "))

        for i in range(n):
            value = int(input("Enter value: "))
            root = insert(root, value)

    elif choice == 2:
        value = int(input("Enter value to delete: "))

        if search(root, value):
            root = delete(root, value)
            print(value, "deleted successfully.")
        else:
            print(value, "not found in tree.")

    elif choice == 3:
        value = int(input("Enter value to search: "))

        if search(root, value):
            print(value, "is FOUND in the tree.")
        else:
            print(value, "is NOT found in the tree.")

    elif choice == 4:
        if root is None:
            print("Tree is empty.")
        else:
            print("\nBinary Search Tree:")
            display(root)

    elif choice == 0:
        print("Thank you!")
        break

    else:
        print("Invalid choice. Try again.")