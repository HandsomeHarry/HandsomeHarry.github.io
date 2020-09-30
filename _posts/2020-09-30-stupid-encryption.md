---
layout: post
title: Stupid Encryption Method, custom-key and fixed-key
---

## What is it?
It's an easy way for encrypting files, with no imports (just using basic python functions)

## How does it work?

Basically it changes the ASCII number for every character to encrypt it, and change it back to decrypt.

As only the 32nd to 126th of the ASCII number are displayable characters, I only included encryptions to those. For the other characters I left them unchanged.

Here's a picture showing how it works:

![Stupid1](/picture/stu-enc.jpg)

As you can see only three numbers are needed to do this kind of encryption. The `95` numbers between 32 and 126 can be separated into `n+1` parts by `n` numbers, in this case `n=3` and it is separated into `4` parts. The n numbers can be the key to decryption, in this case `63`, `79`, and `100`. If I want to do that I'll have to import random, but that kind of messes up the program's beauty.

After a bit of calculation and testing I came up with this algorithm:

![Stupid2](/picture/stu-enc-cus.jpg)

That's clear enough.

Here's the code for encrypting with fixed three numbers `63` `79` `100`:

```
f = open(input("Enter filename for encryption (.txt file): ")+".txt", "r").read()
outFileName = input("Enter output filename: ")
g = open(outFileName+".encrypted", "w+")

# ASCII Encryption
for i in range(len(f)):
    if ord(f[i])<=63 and ord(f[i])>=32:
        # 32~63: +63, becomes 95~126 (31)
        g.write(chr(ord(f[i]) + 63))
    elif ord(f[i])<=79 and ord(f[i])>=64:
        # 64~79: +15, becomes 79~94 (15)
        g.write(chr(ord(f[i]) + 15))
    elif ord(f[i])<=100 and ord(f[i])>=80:
        # 80~100: -22, becomes 58~78 (20)
        g.write(chr(ord(f[i]) - 22))
    elif ord(f[i])<=126 and ord(f[i])>=101:
        # 101~126: -69, becomes 32~57 (25)
        g.write(chr(ord(f[i]) - 69))
    else:
        # other crap (unchanged)
        g.write(f[i])

g.write("Get out! You shouldn't be here!")
g.close()
print("Encryption completed, file", outFileName + ".encrypted", "has been created!")

```
And here's the code for decrypting:
```
inFileName = input("Enter filename for decryption (.encrypted file): ")
f = open(inFileName+".encrypted", "r").read().replace("Get out! You shouldn't be here!", '')
open(inFileName+".encrypted", "w").write(f)
f = open(inFileName+".encrypted", "r").read()
outFileName = input("Enter output filename: ")
g = open(outFileName+".txt", "w+")

# ASCII Decryption
for i in range(len(f)):
    if ord(f[i])<=126 and ord(f[i])>=95:
        # 32~63: +63, becomes 95~126 (31)
        g.write(chr(ord(f[i]) - 63))
    elif ord(f[i])<=94 and ord(f[i])>=79:
        # 64~79: +15, becomes 79~94 (15)
        g.write(chr(ord(f[i]) - 15))
    elif ord(f[i])<=78 and ord(f[i])>=58:
        # 80~100: -22, becomes 58~78 (20)
        g.write(chr(ord(f[i]) + 22))
    elif ord(f[i])<=57 and ord(f[i])>=32:
        # 101~126: -69, becomes 32~57 (25)
        g.write(chr(ord(f[i]) + 69))
    else:
        # other crap (unchanged)
        g.write(f[i])

g.close()
print("Decryption completed, file", outFileName + ".txt", "has been created!")

```
Also here's the custom-key encryption code:
```
# Initialize
f = open(input("Enter filename for encryption (.txt file): ")+".txt", "r").read()
outFileName = input("Enter output filename: ")
g = open(outFileName+".encrypted", "w+")
arr = []

# Ask for input
print("Now you're going to enter 3 numbers to be the encryption key, between 0 and 66")
arr.append(int(input("Enter the first number: ")) + 33)
arr.append(int(input("Enter the second number: ")) + 33)
arr.append(int(input("Enter the third number: ")) + 33)

# Bubble sort the inputs
for i in range(1, len(arr)):
    for j in range(0, len(arr)-i):
        if arr[j] > arr[j+1]:
            arr[j], arr[j+1] = arr[j+1], arr[j]

# Make variables
a = arr[0]
b = arr[1]
c = arr[2]
print(a,b,c)

# Check input
if a>99 or a<33 or b>99 or b<33 or c>99 or c<33:
    print("Invalid input!")
    exit(0)

# Put code in front of outFileName.encrypted
g.write(str(a))
g.write(str(b))
g.write(str(c))

# ASCII Encryption
for i in range(len(f)):
    if ord(f[i])<=a and ord(f[i])>=32:
        # 32~a: +126-a, becomes 158-a~126 (a-32)
        g.write(chr(ord(f[i]) + 126 - a))
    elif ord(f[i])<=b and ord(f[i])>=a+1:
        # a+1~b: -b-a+157, becomes 158-b~157-a (b-a-1)
        g.write(chr(ord(f[i]) - b - a + 157))
    elif ord(f[i])<=c and ord(f[i])>=b+1:
        # b+1~c: c+b-157, becomes 158-c~157-b (c-b-1)
        g.write(chr(ord(f[i]) + c + b - 157))
    elif ord(f[i])<=126 and ord(f[i])>=c+1:
        # c+1~126: +31-c, becomes 32~157-c (126-c)
        g.write(chr(ord(f[i]) + 31 - c))
    else:
        # other crap (unchanged)
        g.write(f[i])

g.write("Get out! You shouldn't be here!")
g.close()
print("Encryption completed, file", outFileName + ".encrypted", "has been created!")

```

Still working on the decoding part for custom-key enryption.

Thanks for reading!
