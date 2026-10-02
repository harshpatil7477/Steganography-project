# LSB Image Steganography in C

## 📌 Project Overview

**LSB Image Steganography** is a C-based project that hides a secret file inside a **BMP image** using the **Least Significant Bit (LSB)** technique.

The main idea is to embed the binary data of a secret file into the least significant bits of the image's pixel data. Since only the least significant bits are modified, the visual appearance of the image remains almost unchanged to the human eye.

The project supports both **encoding** and **decoding** operations:

* **Encoding** – Hide a secret file inside a BMP image.
* **Decoding** – Extract the hidden file from the stego image and reconstruct the original data.

---

## 🎯 Objectives

* Implement LSB-based image steganography using C.
* Hide secret files inside BMP images.
* Extract and reconstruct the hidden file without data corruption.
* Understand binary file handling and bit-level data manipulation.
* Implement command-line based encoding and decoding.
* Preserve the visual appearance of the original BMP image.
* Work with metadata such as magic string, file extension and file size.

---

## 🔐 What is Steganography?

Steganography is the technique of hiding information inside another medium in such a way that the existence of the hidden information is not obvious.

Unlike encryption, which changes readable data into an unreadable form, steganography focuses on hiding the **existence** of the data.

In this project, a BMP image is used as the cover medium and the secret file is embedded into its pixel data.

---

## 💡 What is LSB?

**LSB stands for Least Significant Bit.**

Every byte contains 8 bits:

```text
Bit position:
7 6 5 4 3 2 1 0
```

The rightmost bit is the Least Significant Bit.

For example:

```text
Original pixel byte:
11001001

Secret bit:
0

After embedding:
11001000
```

Only the last bit is changed.

Because the change is very small, the difference between the original image and the stego image is generally not noticeable to the human eye.

---

## 🖼️ Why BMP?

BMP is suitable for this project because its pixel data can be accessed directly without the complexity of lossy image compression.

Advantages of using BMP:

* Direct access to pixel bytes
* Suitable for bit-level manipulation
* No lossy compression during normal BMP storage
* Predictable data layout for this type of implementation

---

## ⚙️ How the Project Works

### 1. Encoding

The encoding process takes:

```text
Cover Image + Secret File
          ↓
      LSB Encoding
          ↓
      Stego Image
```

The main steps are:

1. Open the source BMP image.
2. Open the secret file.
3. Copy the BMP header to the output image.
4. Check whether the image has enough capacity.
5. Encode the magic string.
6. Encode the secret file extension.
7. Encode the secret file size.
8. Read the secret file byte by byte.
9. Convert each byte into individual bits.
10. Store those bits in the LSBs of the image data.
11. Copy the remaining image data.
12. Generate the final stego image.

---

### 2. Decoding

The decoding process takes:

```text
Stego Image
     ↓
Extract Metadata
     ↓
Extract Hidden Bits
     ↓
Reconstruct Secret File
```

The main steps are:

1. Open the stego BMP image.
2. Read and extract the embedded magic string.
3. Verify that the image contains the expected hidden data.
4. Decode the secret file extension.
5. Decode the secret file size.
6. Extract the embedded bits from the image.
7. Reconstruct the original bytes.
8. Write the recovered bytes into the output file.

---

## 🔄 Encoding Flow

```text
                 ENCODING
                     |
                     v
              Cover BMP Image
                     |
                     v
              Check Capacity
                     |
                     v
              Copy BMP Header
                     |
                     v
              Encode Magic String
                     |
                     v
            Encode File Extension
                     |
                     v
              Encode File Size
                     |
                     v
             Encode Secret Data
                     |
                     v
                Stego Image
```

---

## 🔓 Decoding Flow

```text
                 DECODING
                     |
                     v
                Stego Image
                     |
                     v
             Decode Magic String
                     |
                     v
            Decode File Extension
                     |
                     v
              Decode File Size
                     |
                     v
            Decode Secret Data
                     |
                     v
             Reconstructed File
```

---

## 🧩 Important Functions

### `check_operation_type()`

Determines whether the user selected encoding or decoding.

### `open_files()`

Opens the required source, secret and destination files.

### `check_capacity()`

Checks whether the BMP image has enough space to store the secret data.

### `encode_magic_string()`

Stores a predefined magic string in the image so the decoder can verify that valid hidden data exists.

### `encode_secret_file_extn()`

Encodes the extension of the secret file.

For example:

```text
.txt
.pdf
.mp3
```

### `encode_secret_file_data()`

Reads the secret file and embeds its data bit by bit into the image pixel bytes.

### `decode_magic_string()`

Extracts and verifies the embedded magic string.

### `decode_secret_file_data()`

Extracts the hidden bits and reconstructs the original secret file byte by byte.

---

## 📂 Project Structure

A typical project structure is:

```text
LSB-Image-Steganography/
│
├── main.c
├── encode.c
├── encode.h
├── decode.c
├── decode.h
├── types.h
├── common.h
├── README.md
│
├── sample.bmp
├── secret.txt
└── output.bmp
```

> File
