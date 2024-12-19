# TraceCraft

TraceCraft is a powerful API designed to transform images into sketches using the Stable Diffusion model. Built with FastAPI, it provides a fast and efficient way to generate high-quality sketch representations of images.

---

## Features

- **Image to Sketch Conversion**: Leverages Stable Diffusion to create detailed sketches.
- **Fast and Scalable**: Powered by FastAPI for high performance and easy scalability.
- **Simple Integration**: Easy-to-use endpoints for seamless integration into your applications.
- **Customizable**: Supports additional parameters for fine-tuning sketch outputs.

---

## Installation

### Prerequisites

- Python 3.8 or later
- pip (Python package installer)
- CUDA-enabled GPU (recommended for faster processing)

### Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/tracecraft.git
   cd tracecraft
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Ensure the Stable Diffusion model is downloaded and set up. You can integrate it into the API by placing the model files in the `models/` directory (or as specified in the configuration).

4. Start the API:
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8000
   ```

---

## Usage

### Endpoint

#### `POST /convert`
Converts an uploaded image into a sketch.

**Request:**
- **URL**: `/convert`
- **Method**: POST
- **Headers**: `Content-Type: multipart/form-data`
- **Body**:
  - `file`: The image file to convert (e.g., `.jpg`, `.png`).

**Example Request:**
```bash
curl -X POST "http://localhost:8000/convert" \
     -H "Content-Type: multipart/form-data" \
     -F "file=@example.jpg"
```

**Response:**
- **200 OK**: Returns the sketch as a binary file (e.g., `.png`).
- **Error Codes**:
  - `400 Bad Request`: If the file is not provided or is invalid.
  - `500 Internal Server Error`: If something goes wrong during processing.

### Example Python Client
```python
import requests

url = "http://localhost:8000/convert"
files = {"file": ("example.jpg", open("example.jpg", "rb"))}
response = requests.post(url, files=files)

if response.status_code == 200:
    with open("output_sketch.png", "wb") as f:
        f.write(response.content)
else:
    print("Error:", response.json())
```

---

## Configuration

Edit the `config.py` file to:
- Set paths for the Stable Diffusion model.
- Adjust server settings (e.g., host, port).

---

## Development

1. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install development dependencies:
   ```bash
   pip install -r dev-requirements.txt
   ```

3. Run tests:
   ```bash
   pytest
   ```

---

## Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a new branch (`feature/my-feature`).
3. Commit your changes.
4. Push to your fork.
5. Open a pull request.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## Contact

For questions or feedback, please contact [your_email@example.com](mailto:your_email@example.com).
