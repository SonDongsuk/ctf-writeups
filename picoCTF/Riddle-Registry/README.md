# picoCTF - Riddle Registry

## Metadata
Metadata is descriptive information about a file.

Examples include:
- File title
- Author
- Program used to create the file
- Creation date
- Modification date
- Comments or hidden text

Metadata is **not visible on the screen** and must be viewed separately using **file properties or specialized tools**.

---

## Base64

Base64 is an encoding method that represents binary data as text.  
It is **not encryption**, but simply a change in representation.

- **Input:** Arbitrary binary data (files, executable code, images, etc.)
- **Output:** Human-readable ASCII characters
- **Purpose:** To include binary data in environments where only text can be safely transmitted (email, PDF metadata, JSON, HTTP)

### Working Principle

1. **Split the bits**

Original data is stored in **8-bit (1 byte)** units.  
Base64 divides the data into **6-bit units**.

2^6 = 64

This allows each 6-bit value to map exactly to one of **64 characters**.

2. **Conversion Structure**

3 bytes (24 bits) → 4 × (6 bits) → 4 characters

Therefore, the resulting encoded string is always a **multiple of 4**.

### Padding (=)

If the input length is not a multiple of **3 bytes**, the final block becomes incomplete.

Padding (`=`) is added to ensure the output length is a **multiple of 4**.

Rules:
- The padding character `=` only appears **at the end** of the encoded string.
- If `=` appears in the **middle**, it is usually not valid Base64.

Exceptions:
- Line breaks or formatting issues
- Certain URL-safe variants where the string may be truncated

---

# Problem

Not all information inside a file is visible on the screen.  
Some information is hidden in **metadata**.

The goal is to find the **hidden flag inside `Confidential.pdf`**.

---

# Solution

## Method 1: GUI Approach

Open the **Document Properties** of the PDF file.  
In that section, the author's name appeared encoded in **Base64 format**.

### Advantages

1. Intuitive and easy to access  
2. Easy to open and inspect unfamiliar files  
3. Beginners can approach it quickly  

### Disadvantages

1. Hidden fields or non-standard tags may not appear  
2. Cannot be automated and inefficient for repetitive tasks  

---

## Method 2: CLI Approach

Install **exiftool** in the terminal.

Move to the directory where `confidential.pdf` is located and run:

```bash
sudo apt install exiftool
exiftool confidential.pdf
