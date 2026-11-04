# BabyRev – CTF Write-up

## 1. Challenge Information

|Field|Details|
|---|---|
|Challenge Name|BabyRev|
|Platform|Crackmes.one|
|Category|Reverse Engineering|
|Difficulty|1.3|
|Programming Language|C/C++|
|Architecture|x86-64|
|Analysis Tool|Ghidra|
|Operating System|Linux|

**Challenge URL:** [https://crackmes.one/crackme/6784f8a84d850ac5f7dc5173](https://crackmes.one/crackme/6784f8a84d850ac5f7dc5173)

---
## 2. Introduction

In this challenge, the objective is to reverse engineer a Linux executable named `babyrev` to discover the password and secret code required by the application.

The challenge provides an executable that requests two inputs from the user. Instead of guessing these values, I used static analysis with Ghidra to examine the program's internal logic and identify the required credentials.

---
## 3. Step-by-Step Analysis

### Step 1: Download the Challenge

First, I visited the Crackmes.one platform and downloaded the BabyRev challenge.

**Challenge link:** [https://crackmes.one/crackme/6784f8a84d850ac5f7dc5173](https://crackmes.one/crackme/6784f8a84d850ac5f7dc5173)

---
### Step 2: Extract the Downloaded Archive

After downloading the challenge, I extracted the ZIP archive.

The archive was password-protected. I used the website's domain name as the extraction password:

text

```
crackmes.one
```

After successfully extracting the archive, I obtained the `babyrev` executable.

---
### Step 3: Execute the Binary

Next, I opened a terminal and executed the `babyrev` binary to understand its initial behavior.

Upon execution, the application displayed the following output:

text

```
Welcome to baby rev challenge
Input the password:
Input the secret code now:
```

From this output, I identified two input requirements:

- Password: The application requires a password before proceeding.
- Secret Code: The application requests an additional secret code.

This indicated that the binary contains validation logic for both inputs.

---
### Step 4: Open the Binary in Ghidra

To investigate the program's internal implementation, I opened the `babyrev` executable in **Ghidra**.

I created a new project, imported the binary, and allowed Ghidra to perform its initial analysis.

Ghidra helped me inspect the executable's functions, strings, and decompiled code.

---
### Step 5: Analyze the Main Function and Discover the Password

After the analysis was complete, I navigated to the `main()` function.

I examined the decompiled code and focused on the password validation logic.

By inspecting the comparison operations and relevant string references, I identified the password used by the application.

**Discovered Password:**

text

```
Sup3rS3cr3tP455W0rd
```

This revealed the first required input for the challenge.

![[{15947967-F664-441E-8A95-99D18C783884}.png]]

---
### Step 6: Analyze the Secret Code Validation Function

After discovering the password, I continued analyzing the program's control flow.

I examined the code responsible for validating the second input, focusing on the relevant function and its comparison logic.

This allowed me to understand how the application checks the secret code and identify the value required for the next stage.

![[{15947967-F664-441E-8A95-99D18C783884}.png]]

---
### Step 7: Discover the Secret Code

By analyzing the secret code validation logic and examining the relevant comparison values, I identified the decimal secret code.

**Discovered Secret Code:**

text

```
1337
```

This completed the identification of the two required values through static reverse engineering.

![[{718360CD-A534-4AD3-A439-F21F6C151589}.png]]

---
## 4. Final Findings

The following credentials were identified during the analysis:

|Input|Discovered Value|
|---|---|
|Password|`Sup3rS3cr3tP455W0rd`|
|Secret Code|`1337`|

![[{1314A27A-8AE4-4A70-BA9B-5CE51436FD3A}.png]]

---
## 5. Conclusion

In this challenge, I practiced basic static reverse engineering using Ghidra.

I started by downloading and extracting the challenge binary, then executed it to understand its input requirements. After that, I imported the executable into Ghidra and analyzed the `main()` function and the secret code validation logic.

Through static analysis, I identified the password and decimal secret code without relying on random guessing.

This challenge helped me improve my understanding of:

- Linux executable analysis.
- Static reverse engineering.
- Ghidra navigation and decompilation.
- Main function analysis.
- String references and input validation.
- Understanding conditional branches and comparison operations.

Overall, BabyRev was a useful beginner-level reverse engineering exercise that strengthened my understanding of how to analyze executable files and locate hidden validation values.