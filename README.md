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
    pip install -r requirements.txt
    ```

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

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.
I'd be more than glad for any help.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
