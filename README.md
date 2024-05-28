# PressW's Public Docker Images

Welcome to PressW's Public Docker Images repository! This repository hosts Docker images that are publicly available for use. The current image available is `pressw/python-ai`, an extension of the official Python image with additional system dependencies for enhanced AI capabilities.

## Available Docker Images

### `pressw/python-ai`

#### Description

The `pressw/python-ai` image is an enhanced version of the official Python Docker image. It includes Tesseract and several other system dependencies to support AI and machine learning applications more efficiently.

#### Features

-   Based on the official Python image
-   Includes Tesseract OCR for text recognition tasks
-   Pre-installed system dependencies for AI applications
-   Optimized for running AI and machine learning workloads

#### Usage

To use the `pressw/python-ai` image, you can pull it from Docker Hub using the following command:

```bash
docker pull pressw/python-ai:latest
```

You can then use this image as a base for your Dockerfile or run it directly. Here's an example of how to use it in a Dockerfile:

```Dockerfile
FROM pressw/python-ai:latest

# Add your application code here
COPY . /app
WORKDIR /app

# Install any additional Python dependencies
RUN pip install -r requirements.txt

# Command to run your application
CMD ["python", "your_application.py"]
```

Alternatively, you can run a container directly using this image:

```bash
docker run -it --name my-python-ai-container pressw/python-ai:latest
```

#### System Dependencies Included

-   Python
-   ffmpeg
-   libsm6
-   libxext6
-   poppler-utils
-   tesseract-ocr
-   tesseract-ocr-eng

#### Example

Below is an example of how you might use the `pressw/python-ai` image in a FastAPI application:

```python
# app/main.py
from fastapi import FastAPI
from pytesseract import image_to_string
from PIL import Image

app = FastAPI()

@app.post("/ocr/")
async def perform_ocr(image: UploadFile):
    img = Image.open(image.file)
    text = image_to_string(img)
    return {"text": text}

# Dockerfile
FROM pressw/python-ai:latest

COPY . /app
WORKDIR /app
RUN pip install fastapi uvicorn pillow pytesseract

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## Contribution

We welcome contributions to improve and extend the functionality of these Docker images. Please follow the steps below to contribute:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and commit them with clear and descriptive commit messages.
4. Push your changes to your forked repository.
5. Open a pull request to the main repository.

## License

This repository is licensed under the MIT License.

## Contact

If you have any questions, issues, or suggestions, please open an issue in this repository, or contact us at `help@pressw.ai`.

Thank you for using PressW's Public Docker Images!
