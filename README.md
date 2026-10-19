
"""
============================================================
OBJECT ORIENTED PROGRAMMING USING PYTHON
B.Sc. (Hons.) Computer Science - Practical File
============================================================

TABLE OF CONTENTS
-----------------
01. Roots of a Quadratic Equation
02. Prime Numbers
    a. Check whether a number is prime
    b. Generate all primes up to n
    c. Generate the first n primes
03. Star Pyramid and Reverse Pyramid
04. Character Classification
05. String Operations
    a. Frequency of a character
    b. Replace a character
    c. Remove first occurrence
    d. Remove all occurrences
06. Swap First n Characters of Two Strings
07. Indices of All Occurrences of a Substring
08. Cubes of Even Integers
    a. Using a for loop
    b. Using list comprehension
09. File Operations
    a. Count characters, words and lines
    b. Character frequency
    c. Print words in reverse order
    d. Separate even and odd lines
10. Dictionary of Numbers and Their Cubes
11. Tuple Operations
12. Employee Class
13. Two-Dimensional Point Class
14. Three-Dimensional Point Class (Inheritance)
15. Name Validation Using Exceptions

HOW TO RUN
----------
1. Save this file as OOP_Python_Practicals.py
2. Open a terminal in the file's directory.
3. Run: python OOP_Python_Practicals.py
4. Enter the practical number you want to execute.
5. Enter 0 to exit.

For Practical 9, create a text file named input.txt in the
same directory, or enter another existing file path.
============================================================
"""

import math
from pathlib import Path


# ============================================================
# PRACTICAL 1: ROOTS OF A QUADRATIC EQUATION
# ============================================================

def practical_01():
    print("\n--- Practical 1: Quadratic Equation ---")

    a = float(input("Enter coefficient a: "))
    b = float(input("Enter coefficient b: "))
    c = float(input("Enter coefficient c: "))

    if a == 0:
        if b == 0:
            print("No unique solution exists.")
        else:
            print("Linear equation root:", -c / b)
        return

    discriminant = b**2 - 4*a*c

    if discriminant > 0:
        root1 = (-b + math.sqrt(discriminant)) / (2*a)
        root2 = (-b - math.sqrt(discriminant)) / (2*a)
        print("Two distinct real roots:", root1, "and", root2)

    elif discriminant == 0:
        root = -b / (2*a)
        print("Two equal real roots:", root)

    else:
        real_part = -b / (2*a)
        imaginary_part = math.sqrt(-discriminant) / abs(2*a)
        print(f"Complex roots: {real_part} + {imaginary_part}i")
        print(f"               {real_part} - {imaginary_part}i")


# ============================================================
# PRACTICAL 2: PRIME NUMBERS
# ============================================================

def is_prime(n):
    """Return True if n is prime, otherwise False."""
    if n < 2:
        return False

    for i in range(2, math.isqrt(n) + 1):
        if n % i == 0:
            return False

    return True


def practical_02():
    print("\n--- Practical 2: Prime Numbers ---")
    print("a. Check whether n is prime")
    print("b. Generate all primes up to n")
    print("c. Generate the first n primes")

    choice = input("Choose a, b or c: ").strip().lower()

    if choice == "a":
        n = int(input("Enter an integer: "))
        print(f"{n} is prime." if is_prime(n)
              else f"{n} is not prime.")

    elif choice == "b":
        n = int(input("Generate primes up to: "))
        primes = [i for i in range(2, n + 1) if is_prime(i)]
        print("Prime numbers:", primes)

    elif choice == "c":
        n = int(input("How many primes do you want? "))

        if n < 0:
            print("Please enter a non-negative integer.")
            return

        primes = []
        candidate = 2

        while len(primes) < n:
            if is_prime(candidate):
                primes.append(candidate)
            candidate += 1

        print(f"First {n} prime numbers:", primes)

    else:
        print("Invalid choice.")


# ============================================================
# PRACTICAL 3: STAR PYRAMID AND REVERSE PYRAMID
# ============================================================

def practical_03():
    print("\n--- Practical 3: Star Patterns ---")

    rows = int(input("Enter the number of rows: "))

    if rows <= 0:
        print("Enter a positive number of rows.")
        return

    print("\nPyramid:")
    for i in range(1, rows + 1):
        print(" " * (rows - i) + "* " * i)

    print("\nReverse Pyramid:")
    for i in range(rows, 0, -1):
        print(" " * (rows - i) + "* " * i)


# ============================================================
# PRACTICAL 4: CHARACTER CLASSIFICATION
# ============================================================

def practical_04():
    print("\n--- Practical 4: Character Classification ---")

    character = input("Enter a single character: ")

    if len(character) != 1:
        print("Please enter exactly one character.")
        return

    if character.isalpha():
        print("The character is a letter.")

        if character.isupper():
            print("It is an uppercase letter.")
        else:
            print("It is a lowercase letter.")

    elif character.isdigit():
        digit_names = [
            "ZERO", "ONE", "TWO", "THREE", "FOUR",
            "FIVE", "SIX", "SEVEN", "EIGHT", "NINE"
        ]

        print("The character is a numeric digit.")
        print("Digit in words:", digit_names[int(character)])

    else:
        print("The character is a special character or symbol.")


# ============================================================
# PRACTICAL 5: STRING OPERATIONS
# ============================================================

def practical_05():
    print("\n--- Practical 5: String Operations ---")

    string = input("Enter a string: ")

    print("a. Find character frequency")
    print("b. Replace a character")
    print("c. Remove first occurrence")
    print("d. Remove all occurrences")

    choice = input("Choose a, b, c or d: ").strip().lower()

    if choice == "a":
        char = input("Enter the character to count: ")
        if len(char) != 1:
            print("Enter exactly one character.")
            return
        print("Frequency:", string.count(char))

    elif choice == "b":
        old = input("Character to replace: ")
        new = input("Replacement character: ")

        if len(old) != 1 or len(new) != 1:
            print("Enter exactly one character for each.")
            return

        print("Result:", string.replace(old, new))

    elif choice == "c":
        char = input("Character to remove: ")

        if len(char) != 1:
            print("Enter exactly one character.")
            return

        print("Result:", string.replace(char, "", 1))

    elif choice == "d":
        char = input("Character to remove: ")

        if len(char) != 1:
            print("Enter exactly one character.")
            return

        print("Result:", string.replace(char, ""))

    else:
        print("Invalid choice.")


# ============================================================
# PRACTICAL 6: SWAP FIRST n CHARACTERS OF TWO STRINGS
# ============================================================

def practical_06():
    print("\n--- Practical 6: Swap String Prefixes ---")

    first = input("Enter the first string: ")
    second = input("Enter the second string: ")
    n = int(input("Enter the number of characters to swap: "))

    if n < 0 or n > min(len(first), len(second)):
        print("n must be between 0 and the length of the shorter string.")
        return

    new_first = second[:n] + first[n:]
    new_second = first[:n] + second[n:]

    print("First string after swapping:", new_first)
    print("Second string after swapping:", new_second)


# ============================================================
# PRACTICAL 7: INDICES OF ALL SUBSTRING OCCURRENCES
# ============================================================

def find_occurrences(string, substring):
    """Return all starting indices, including overlapping matches.
    Return -1 if the substring is not found.
    """
    if substring == "":
        return list(range(len(string) + 1))

    indices = []
    start = 0

    while True:
        index = string.find(substring, start)

        if index == -1:
            break

        indices.append(index)
        start = index + 1

    return indices if indices else -1


def practical_07():
    print("\n--- Practical 7: Substring Indices ---")

    string = input("Enter the main string: ")
    substring = input("Enter the substring to search for: ")

    result = find_occurrences(string, substring)
    print("Result:", result)


# ============================================================
# PRACTICAL 8: CUBES OF EVEN INTEGERS
# ============================================================

def practical_08():
    print("\n--- Practical 8: Cubes of Even Integers ---")

    values = list(map(
        int,
        input("Enter integers separated by spaces: ").split()
    ))

    # Method A: using a for loop
    even_cubes_loop = []

    for number in values:
        if number % 2 == 0:
            even_cubes_loop.append(number**3)

    # Method B: using list comprehension
    even_cubes_comprehension = [
        number**3 for number in values if number % 2 == 0
    ]

    print("Using for loop:", even_cubes_loop)
    print("Using list comprehension:", even_cubes_comprehension)


# ============================================================
# PRACTICAL 9: FILE OPERATIONS
# ============================================================

def practical_09():
    print("\n--- Practical 9: File Operations ---")

    filename = input(
        "Enter input filename [input.txt]: "
    ).strip() or "input.txt"

    path = Path(filename)

    try:
        with path.open("r", encoding="utf-8") as file:
            content = file.read()

    except FileNotFoundError:
        print(f"File '{filename}' was not found.")
        print("Create the file and run this practical again.")
        return

    except OSError as error:
        print("Unable to read the file:", error)
        return

    # a. Count characters, words and lines
    lines = content.splitlines()
    words = content.split()

    print("\na. File statistics")
    print("Total characters:", len(content))
    print("Total words:", len(words))
    print("Total lines:", len(lines))

    # b. Frequency of each character
    print("\nb. Character frequency")
    frequency = {}

    for character in content:
        frequency[character] = frequency.get(character, 0) + 1

    for character, count in frequency.items():
        if character == "\n":
            label = r"\n (newline)"
        elif character == "\t":
            label = r"\t (tab)"
        elif character == " ":
            label = "' ' (space)"
        else:
            label = repr(character)

        print(f"{label}: {count}")

    # c. Print words in reverse order
    print("\nc. Words in reverse order")
    print(" ".join(reversed(words)))

    # d. Write even-numbered lines to File1 and odd-numbered
    #    lines to File2. Line numbering starts at 1.
    try:
        with open("File1", "w", encoding="utf-8") as even_file, \
             open("File2", "w", encoding="utf-8") as odd_file:

            for line_number, line in enumerate(lines, start=1):
                if line_number % 2 == 0:
                    even_file.write(line + "\n")
                else:
                    odd_file.write(line + "\n")

        print("\nd. Lines separated successfully.")
        print("Even-numbered lines saved in File1.")
        print("Odd-numbered lines saved in File2.")

    except OSError as error:
        print("Unable to write output files:", error)


# ============================================================
# PRACTICAL 10: DICTIONARY OF NUMBERS AND THEIR CUBES
# ============================================================

def practical_10():
    print("\n--- Practical 10: Dictionary of Cubes ---")

    cubes = {}

    for number in range(1, 6):
        cubes[number] = number**3

    print("Dictionary:", cubes)


# ============================================================
# PRACTICAL 11: TUPLE OPERATIONS
# ============================================================

def practical_11():
    print("\n--- Practical 11: Tuple Operations ---")

    t1 = (1, 2, 5, 7, 9, 2, 4, 6, 8, 10)

    print("Original tuple:", t1)

    # a. Print half the values on each line
    midpoint = len(t1) // 2
    print("\na. First half:", *t1[:midpoint])
    print("   Second half:", *t1[midpoint:])

    # b. Tuple containing even numbers
    even_tuple = tuple(number for number in t1 if number % 2 == 0)
    print("\nb. Even numbers tuple:", even_tuple)

    # c. Concatenate t2 with t1
    t2 = (11, 13, 15)
    combined = t1 + t2
    print("\nc. t1 + t2:", combined)

    # d. Maximum and minimum of the combined tuple
    print("\nd. Maximum value:", max(combined))
    print("   Minimum value:", min(combined))


# ============================================================
# PRACTICAL 12: EMPLOYEE CLASS
# ============================================================

class Employee:
    """Store employee details and calculate salary."""

    count = 0

    def __init__(self, employee_number, name, department,
                 basic, da, hra):
        if basic < 0 or da < 0 or hra < 0:
            raise ValueError(
                "Basic salary, DA and HRA cannot be negative."
            )

        self.employee_number = employee_number
        self.name = name
        self.department = department
        self.basic = basic
        self.da = da
        self.hra = hra

        Employee.count += 1
        self._counted = True

    def salary(self):
        """Return the sum of Basic, DA and HRA."""
        return self.basic + self.da + self.hra

    def __del__(self):
        # Decrease the live-object count when the object is
        # destroyed. Python controls when __del__ is called.
        if getattr(self, "_counted", False):
            Employee.count -= 1
            self._counted = False

    def __str__(self):
        return (
            f"Employee Number: {self.employee_number}\n"
            f"Name: {self.name}\n"
            f"Department: {self.department}\n"
            f"Basic: {self.basic:.2f}\n"
            f"DA: {self.da:.2f}\n"
            f"HRA: {self.hra:.2f}\n"
            f"Total Salary: {self.salary():.2f}"
        )


def practical_12():
    print("\n--- Practical 12: Employee Class ---")

    try:
        employee_number = input("Enter employee number: ")
        name = input("Enter employee name: ")
        department = input("Enter department: ")
        basic = float(input("Enter basic salary: "))
        da = float(input("Enter DA: "))
        hra = float(input("Enter HRA: "))

        employee = Employee(
            employee_number, name, department, basic, da, hra
        )

        print("\nEmployee details")
        print(employee)
        print("\nNumber of live Employee objects:", Employee.count)

    except ValueError as error:
        print("Invalid input:", error)


# ============================================================
# PRACTICAL 13: TWO-DIMENSIONAL POINT CLASS
# ============================================================

class Point2D:
    """Represent a point in two-dimensional space."""

    def __init__(self, x, y):
        self.x = float(x)
        self.y = float(y)

    def distance(self, other):
        """Calculate Euclidean distance between two 2D points."""
        return math.sqrt(
            (self.x - other.x)**2 + (self.y - other.y)**2
        )

    def __str__(self):
        return f"Point2D(x={self.x}, y={self.y})"


def practical_13():
    print("\n--- Practical 13: Two-Dimensional Points ---")

    x1 = float(input("Enter x1: "))
    y1 = float(input("Enter y1: "))
    x2 = float(input("Enter x2: "))
    y2 = float(input("Enter y2: "))

    point1 = Point2D(x1, y1)
    point2 = Point2D(x2, y2)

    print("First point:", point1)
    print("Second point:", point2)
    print("Distance:", point1.distance(point2))


# ============================================================
# PRACTICAL 14: THREE-DIMENSIONAL POINT CLASS
# ============================================================

class Point3D(Point2D):
    """Extend Point2D by adding a z-coordinate."""

    def __init__(self, x, y, z):
        super().__init__(x, y)
        self.z = float(z)

    def distance(self, other):
        """Override distance to calculate 3D Euclidean distance."""
        if not isinstance(other, Point3D):
            raise TypeError("Both points must be Point3D objects.")

        return math.sqrt(
            (self.x - other.x)**2
            + (self.y - other.y)**2
            + (self.z - other.z)**2
        )

    def __str__(self):
        return f"Point3D(x={self.x}, y={self.y}, z={self.z})"


def practical_14():
    print("\n--- Practical 14: Three-Dimensional Points ---")

    x1 = float(input("Enter x1: "))
    y1 = float(input("Enter y1: "))
    z1 = float(input("Enter z1: "))

    x2 = float(input("Enter x2: "))
    y2 = float(input("Enter y2: "))
    z2 = float(input("Enter z2: "))

    point1 = Point3D(x1, y1, z1)
    point2 = Point3D(x2, y2, z2)

    print("First point:", point1)
    print("Second point:", point2)
    print("3D distance:", point1.distance(point2))


# ============================================================
# PRACTICAL 15: NAME VALIDATION USING EXCEPTIONS
# ============================================================

def practical_15():
    print("\n--- Practical 15: Name Validation ---")

    name = input("Enter your name: ").strip()

    try:
        if not name:
            raise ValueError("Name cannot be empty.")

        if any(character.isdigit() for character in name):
            raise ValueError("Name must not contain digits.")

        if any(not (character.isalpha() or character.isspace())
               for character in name):
            raise ValueError(
                "Name must not contain special characters."
            )

        print("Valid name:", name)

    except ValueError as error:
        print("Invalid input:", error)


# ============================================================
# MAIN MENU
# ============================================================

PRACTICALS = {
    1: practical_01,
    2: practical_02,
    3: practical_03,
    4: practical_04,
    5: practical_05,
    6: practical_06,
    7: practical_07,
    8: practical_08,
    9: practical_09,
    10: practical_10,
    11: practical_11,
    12: practical_12,
    13: practical_13,
    14: practical_14,
    15: practical_15,
}

PRACTICAL_NAMES = [
    "Quadratic equation roots",
    "Prime numbers",
    "Star pyramid and reverse pyramid",
    "Character classification",
    "String operations",
    "Swap first n characters",
    "Substring occurrence indices",
    "Cubes of even integers",
    "File operations",
    "Dictionary of cubes",
    "Tuple operations",
    "Employee class",
    "Two-dimensional point",
    "Three-dimensional point and inheritance",
    "Name validation and exceptions",
]


def main():
    while True:
        print("\n" + "=" * 58)
        print(" OBJECT ORIENTED PROGRAMMING USING PYTHON")
        print("               PRACTICAL MENU")
        print("=" * 58)

        for number, name in enumerate(PRACTICAL_NAMES, start=1):
            print(f"{number:2}. {name}")

        print(" 0. Exit")
        print("=" * 58)

        try:
            choice = int(input("Enter practical number (0-15): "))

            if choice == 0:
                print("Exiting practicals. Goodbye!")
                break

            if choice not in PRACTICALS:
                print("Please select a number between 0 and 15.")
                continue

            PRACTICALS[choice]()

        except ValueError:
            print("Invalid input. Please enter a valid number.")

        except (EOFError, KeyboardInterrupt):
            print("\nProgram terminated.")
            break

        except Exception as error:
            print(f"An unexpected error occurred: {error}")

        input("\nPress Enter to return to the main menu...")


if __name__ == "__main__":
    main()
