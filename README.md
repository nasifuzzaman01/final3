Image Manipulation Software

Student Name: Md Nasifuzzaman
Roll: 1820

A C-based desktop image manipulation application built using the IUP GUI toolkit and IM image-processing library. The application provides a simple graphical interface for opening BMP images, applying common pixel-level transformations, undoing the last operation, and saving the result.

Features

Open BMP images through a file dialog

Save the edited image as a BMP file

Grayscale conversion

Color inversion

Horizontal flip

Vertical flip

90-degree rotation

Blur using a neighborhood averaging operation

Brightness adjustment from -255 to 255

Crop using X, Y, Width, and Height

Undo the most recent image operation

Basic validation and warning dialogs for invalid operations

Screenshots

Application Interface

The following screenshot shows the application's GUI and its available image-editing controls.



Example: Inversion

The project includes lena.bmp and its inverted result invertedLena.bmp.



Technologies Used

Technology

Purpose

C

Application and image-processing logic

IUP

Graphical user interface

IM

Image loading, conversion, manipulation support, and BMP saving

GTK 3

GUI backend/dependencies on Linux

GCC

Compilation

Make

Build automation

Project Structure

image_manipulation/
├── Makefile
├── app
├── include/
│   └── custom.h
├── src/
│   ├── main.c
│   ├── gui.c
│   ├── menu.c
│   ├── controls.c
│   ├── ui.c
│   └── utils.c
├── images/
│   ├── lena.bmp
│   ├── invertedLena.bmp
│   └── a.bmp
├── iup/
└── im/

Source-file responsibilities

src/main.c — initializes the application state, starts IUP, launches the GUI, and performs cleanup.

src/gui.c — creates the main window, menus, buttons, text inputs, and image display widget.

src/menu.c — handles Open, Save As, and Exit.

src/controls.c — implements grayscale, inversion, flips, rotation, blur, crop, brightness, and undo.

src/ui.c — converts the current IM image into an IUP image and refreshes the GUI.

src/utils.c — application-state validation, cleanup, and debugging helpers.

include/custom.h — shared declarations, callback prototypes, and the AppState structure.

Makefile — compiles and links the complete application.

How the Application Works

The program maintains an application state containing:

typedef struct
{
    char *currentImageFile;
    imImage *currentImage;
    imImage *undoImage;
    Ihandle *imageWidget;
} AppState;

When an image is opened, it is loaded using the IM library. Each editing operation changes currentImage and stores a duplicate in undoImage before modification. The GUI is then refreshed so the updated image is displayed.

The processing operations work directly with the RGB pixel planes of the imImage.

Build and Run Process

The project can be built and executed from an Ubuntu/Linux terminal or from Ubuntu running through WSL on Windows.

Step 1: Open the Project Directory

Open the terminal and move into the project folder:

cd ~/image_manipulation

If the project is stored somewhere else, replace the path with the actual project location.

Step 2: Install Required Build Dependencies

Update the package list:

sudo apt update

Install GCC, Make, GTK 3 development files, X11 development files, and pkg-config:

sudo apt install build-essential libgtk-3-dev libx11-dev pkg-config

The project also contains the required IUP and IM libraries in the iup/ and im/ directories.

Step 3: Build the Application

Run the Makefile:

make app

The Makefile compiles the C source files and links them with the IUP, IM, GTK, and X11 libraries.

If the build is successful, an executable named app is created in the project directory.

Step 4: Run the Application

Start the program with:

./app

This opens the Image Manipulation Software GUI.

Step 5: Open an Image

Inside the application:

Click File → Open.

Select a .bmp image.

The selected image appears in the application window.

Use the available buttons to perform image-processing operations.

Step 6: Apply Image Operations

The application supports:

Grayscale

Inversion

Horizontal Flip

Vertical Flip

Rotate 90°

Blur

Brightness adjustment

Crop

Undo

Step 7: Save the Result

After editing the image:

Click File → Save as.

Choose the destination and filename.

Save the processed image as a BMP file.

Step 8: Clean the Build

To remove the generated executable and build files:

make clean

After cleaning, the application can be rebuilt at any time with:

make app

Complete Build and Run Commands

For a quick setup, the main commands are:

sudo apt update
sudo apt install build-essential libgtk-3-dev libx11-dev pkg-config

cd ~/image_manipulation

make app

./app

Build flow:

Source Code (.c/.h)
        ↓
      make app
        ↓
   GCC Compilation
        ↓
 IUP + IM + GTK + X11
        ↓
    app executable
        ↓
       ./app
        ↓
 Image Manipulation GUI

Using the Program

Run ./app.

Select File → Open.

Choose a .bmp image.

Use the operation buttons to manipulate the image:

Grayscale

Inversion

Horizontal Flip

Vertical Flip

Rotate 90deg

Blur

Undo

For brightness, enter a value from -255 to 255 and press Apply.

For cropping, enter:

X coordinate

Y coordinate

Width

Height

Click Crop Image.

Use File → Save as to save the processed image.

Image Processing Details

Grayscale

The RGB values are converted using the standard weighted luminance formula:

Gray = 0.299R + 0.587G + 0.114B

The resulting gray value is assigned to all three RGB channels.

Inversion

Each channel is replaced by its complement:

R' = 255 - R
G' = 255 - G
B' = 255 - B

Brightness

A user-specified value is added to every RGB channel. Values are clamped to the valid byte range:

0 <= channel <= 255

Horizontal and Vertical Flip

Pixel positions are exchanged across the corresponding horizontal or vertical axis.

90-Degree Rotation

A new image is allocated with swapped width and height, and pixels are copied into their rotated positions.

Blur

A neighborhood averaging approach is used. The surrounding pixels are averaged to produce a smoother image.

Crop

A new image is created from the requested rectangular region. Invalid starting coordinates or non-positive dimensions are rejected.

Undo

Before an editing operation changes the current image, a duplicate is stored as the undo image. The Undo button restores that previous state.

Notes

The current Open/Save dialogs are configured specifically for BMP images.

The program is designed for a Linux/GTK environment because the Makefile links against GTK 3 and X11.

The bundled iup/ and im/ directories contain the project's local IUP and IM libraries, headers, and related files.

Author

Md Nasifuzzaman
Roll: 1820
