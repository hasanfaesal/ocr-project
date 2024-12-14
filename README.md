# OCR Project

This is a beginner level Optical Character Recognition (OCR) project. The goal of this project is to extract text from images using Python.

I'm building this for my courses of Data Structres and Algorithms and Programming for AI semester projects.

## Features

- Extract text from images
- Support for multiple image formats (JPEG, PNG, etc.)
- Simple and easy-to-understand code

## Requirements

- Python 3.x
- Tesseract-OCR
- Pillow
- pytesseract

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/ocr-project.git
    cd ocr-project
    ```

2. Install the required Python packages/dependencies:
    ```bash
    pip install pillow pytesseract
    ```
    '''pip install -r requirements.txt'''

3. Install Tesseract-OCR:
    - **Windows**: Download the installer from [here](https://github.com/UB-Mannheim/tesseract/wiki).
    - **macOS**: Install using Homebrew:
        ```bash
        brew install tesseract
        ```
    - **Linux**: Install using the package manager:
        ```bash
        sudo apt-get install tesseract-ocr
        ```

## Usage

1. Place the images you want to process in the `images` directory.
2. Run the OCR script:
    ```bash
    python ocr.py
    ```
3. The extracted text will be saved in the `output` directory.

## Example

```python
from PIL import Image
import pytesseract

# Load an image from file
image = Image.open('images/sample.jpg')

# Use Tesseract to do OCR on the image
text = pytesseract.image_to_string(image)

# Print the extracted text
print(text)
```

## GUI Based OCR System (PyQt5 library)

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QVBoxLayout, QPushButton, QLabel, QFileDialog, QHBoxLayout, QFrame
from PyQt5.QtGui import QPixmap, QColor, QPalette, QClipboard  # Updated import for QClipboard
from PyQt5.QtCore import Qt
import pytesseract
from PIL import Image

# Update the path to Tesseract OCR executable
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'

class OCRApp(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("OCR GUI with PyQt5")
        self.setGeometry(100, 100, 750, 550)
        self.setStyleSheet("background-color: #f4f4f9;")  # Set background color of the window

        # Layouts
        self.main_layout = QVBoxLayout()
        self.top_layout = QHBoxLayout()

        # Button to select an image
        self.select_button = QPushButton("Select Image")
        self.select_button.setStyleSheet("""
            background-color: #A8D0E6;
            color: white;
            font-size: 16px;
            border-radius: 5px;
            padding: 10px;
        """)
        self.select_button.clicked.connect(self.select_image)
        self.top_layout.addWidget(self.select_button)

        # Label to display the image
        self.image_label = QLabel("Selected image will appear here")
        self.image_label.setStyleSheet("""
            border: 2px solid #A8D0E6;
            border-radius: 10px;
            padding: 10px;
            background-color: white;
        """)
        self.image_label.setAlignment(Qt.AlignCenter)
        self.image_label.setScaledContents(True)
        self.image_label.setFixedHeight(200)
        self.main_layout.addLayout(self.top_layout)
        self.main_layout.addWidget(self.image_label)

        # Label to display extracted text
        self.text_label = QLabel("Extracted text will appear here")
        self.text_label.setStyleSheet("""
            border: 2px solid #A8D0E6;
            border-radius: 10px;
            padding: 10px;
            background-color: white;
            font-size: 14px;
            word-wrap: break-word;
        """)
        self.text_label.setAlignment(Qt.AlignTop)
        self.main_layout.addWidget(self.text_label)

        # Copy to Clipboard Button
        self.copy_button = QPushButton("Copy Text")
        self.copy_button.setStyleSheet("""
            background-color: #A8D0E6;
            color: white;
            font-size: 16px;
            border-radius: 5px;
            padding: 10px;
        """)
        self.copy_button.clicked.connect(self.copy_text)
        self.main_layout.addWidget(self.copy_button)

        # Set layout
        self.setLayout(self.main_layout)

    def select_image(self):
        # Open file dialog to select an image
        file_path, _ = QFileDialog.getOpenFileName(self, "Select an Image", "", "Image Files (*.png *.jpg *.jpeg *.bmp)")

        if file_path:
            # Display the selected image
            pixmap = QPixmap(file_path)
            self.image_label.setPixmap(pixmap)

            # Perform OCR on the selected image
            extracted_text = self.perform_ocr(file_path)
            self.text_label.setText(f"Extracted Text:\n{extracted_text}")

    def perform_ocr(self, image_path):
        try:
            # Open the image using PIL
            img = Image.open(image_path)

            # Use Tesseract OCR to extract text
            text = pytesseract.image_to_string(img)

            return text.strip()  # Return the extracted text
        except Exception as e:
            return f"Error: {e}"

    def copy_text(self):
        # Get the extracted text from the label
        extracted_text = self.text_label.text()

        # If text is available, copy it to clipboard
        if extracted_text != "Extracted text will appear here" and extracted_text != "Error: No text extracted":
            clipboard = QApplication.clipboard()
            clipboard.setText(extracted_text)
            self.text_label.setText("Text copied to clipboard!")

# Run the application
if __name__ == "__main__":
    app = QApplication(sys.argv)
    ocr_app = OCRApp()
    ocr_app.show()
    import sys
    from PyQt5.QtWidgets import QApplication, QWidget, QVBoxLayout, QPushButton, QLabel, QFileDialog, QHBoxLayout, \
        QFrame
    from PyQt5.QtGui import QPixmap, QColor, QPalette, QClipboard  # Updated import for QClipboard
    from PyQt5.QtCore import Qt
    import pytesseract
    from PIL import Image

    # Update the path to Tesseract OCR executable
    pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'


    class OCRApp(QWidget):
        def __init__(self):
            super().__init__()
            self.setWindowTitle("OCR GUI with PyQt5")
            self.setGeometry(100, 100, 750, 550)
            self.setStyleSheet("background-color: #f4f4f9;")  # Set background color of the window

            # Layouts
            self.main_layout = QVBoxLayout()
            self.top_layout = QHBoxLayout()

            # Button to select an image
            self.select_button = QPushButton("Select Image")
            self.select_button.setStyleSheet("""
                background-color: #A8D0E6;
                color: white;
                font-size: 16px;
                border-radius: 5px;
                padding: 10px;
            """)
            self.select_button.clicked.connect(self.select_image)
            self.top_layout.addWidget(self.select_button)

            # Label to display the image
            self.image_label = QLabel("Selected image will appear here")
            self.image_label.setStyleSheet("""
                border: 2px solid #A8D0E6;
                border-radius: 10px;
                padding: 10px;
                background-color: white;
            """)
            self.image_label.setAlignment(Qt.AlignCenter)
            self.image_label.setScaledContents(True)
            self.image_label.setFixedHeight(200)
            self.main_layout.addLayout(self.top_layout)
            self.main_layout.addWidget(self.image_label)

            # Label to display extracted text
            self.text_label = QLabel("Extracted text will appear here")
            self.text_label.setStyleSheet("""
                border: 2px solid #A8D0E6;
                border-radius: 10px;
                padding: 10px;
                background-color: white;
                font-size: 14px;
                word-wrap: break-word;
            """)
            self.text_label.setAlignment(Qt.AlignTop)
            self.main_layout.addWidget(self.text_label)

            # Copy to Clipboard Button
            self.copy_button = QPushButton("Copy Text")
            self.copy_button.setStyleSheet("""
                background-color: #A8D0E6;
                color: white;
                font-size: 16px;
                border-radius: 5px;
                padding: 10px;
            """)
            self.copy_button.clicked.connect(self.copy_text)
            self.main_layout.addWidget(self.copy_button)

            # Set layout
            self.setLayout(self.main_layout)

        def select_image(self):
            # Open file dialog to select an image
            file_path, _ = QFileDialog.getOpenFileName(self, "Select an Image", "",
                                                       "Image Files (*.png *.jpg *.jpeg *.bmp)")

            if file_path:
                # Display the selected image
                pixmap = QPixmap(file_path)
                self.image_label.setPixmap(pixmap)

                # Perform OCR on the selected image
                extracted_text = self.perform_ocr(file_path)
                self.text_label.setText(f"Extracted Text:\n{extracted_text}")

        def perform_ocr(self, image_path):
            try:
                # Open the image using PIL
                img = Image.open(image_path)

                # Use Tesseract OCR to extract text
                text = pytesseract.image_to_string(img)

                return text.strip()  # Return the extracted text
            except Exception as e:
                return f"Error: {e}"

        def copy_text(self):
            # Get the extracted text from the label
            extracted_text = self.text_label.text()

```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.
I'd be more than glad for any help.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
