# Random Password Generator

A simple command-line Password Generator built with Python.  
This project generates random passwords based on user-defined criteria such as password length and character types like letters, numbers, and symbols. The idea matches a common beginner Python mini-project structure using character sets and random selection. [web:1][web:4]

## Features

- Generate random passwords from the command line. [web:4][web:9]
- User can choose the password length. [web:3][web:4]
- User can include letters, numbers, and symbols. [web:1][web:9]
- Basic input validation for safer and correct usage. [web:2]

## Concepts Used

- **Randomization**: Random characters are selected to form the password. [web:1][web:9]
- **User Input Validation**: The program checks whether the entered length and options are valid. [web:2]
- **Character Set Handling**: The program manages separate character groups like alphabets, digits, and symbols. [web:1][web:2]

## Technologies Used

- Python
- `random` or `secrets`
- `string`

Python’s `secrets` module is specifically documented as suitable for generating strong random values for passwords and similar secrets. [web:7]

## How It Works

1. The user enters the desired password length. [web:3][web:4]
2. The user selects which character types to include:
   - Letters
   - Numbers
   - Symbols [web:1][web:9]
3. The program creates a character pool based on the selected options. [web:1][web:2]
4. A random password is generated and displayed. [web:1][web:4]

## Example Output

```bash
Enter password length: 12
Include letters? yes
Include numbers? yes
Include symbols? yes

Generated Password: A@7kP!2xL9#m
```

## Project Structure

```bash
password-generator/
│── password_generator.py
│── README.md
```

## Learning Outcome

This project helps beginners understand:

- Random generation in Python. [web:1]
- Working with strings and character sets. [web:1][web:2]
- Handling user input in a command-line application. [web:2]
- Writing simple utility-based Python projects. [web:4][web:9]

## Future Improvements

- Add an option to generate multiple passwords at once. [web:14]
- Add password strength checking.
- Build a GUI version using Tkinter.
- Use `secrets` instead of basic random generation for stronger password security, since Python documents `secrets` for password and token generation. [web:7]

## Conclusion

This Random Password Generator is a beginner-friendly Python project that demonstrates randomization, validation, and character set management in a practical way. It is a good mini-project for improving Python basics and command-line programming skills. [web:1][web:4]
