📷 Automated Numeric Entity Extraction from Images using OCR

This project provides an end-to-end solution to extract numeric values with associated units (like kg, V, W, and cm) from images using Optical Character Recognition (OCR) and regex-based entity extraction. It is useful in domains such as e-commerce, healthcare, and supply chain, where critical product data is often embedded in images.

⸻

🚀 Features
	•	🧠 Automatically detects and extracts numeric values with units from text in images
	•	📸 Uses Tesseract OCR and OpenCV for text extraction and image preprocessing
	•	📐 Identifies context-specific entities like:
	•	Weight (e.g., 5.6 kg)
	•	Voltage (e.g., 230 V)
	•	Wattage (e.g., 1200 W)
	•	Dimensions (e.g., 24 x 12 x 5 cm)
	•	🔎 Regex-based filtering to match meaningful patterns
	•	📊 Displays preprocessed image and extracted results

⸻

🛠 Technologies Used
	•	Python 3
	•	OpenCV – Image preprocessing
	•	Tesseract OCR – Text extraction
	•	Regex (re) – Pattern matching
	•	Matplotlib / PIL – Image display
	•	Jupyter Notebook / Colab – Development environment

---

## ⚙️ How It Works

### Step 1: Load and Display the Image
```python
img = Image.open('sample1.jpeg')
display(img)
```

### Step 2: Preprocess Image
Convert the image to grayscale and apply thresholding to enhance OCR accuracy.

```python
def preprocess_image(image_path):
    image = cv2.imread(image_path)
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    _, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)
    plt.imshow(thresh, cmap='gray')
    plt.title('Preprocessed Image for OCR')
    plt.show()
    return thresh

preprocessed_image = preprocess_image(uploaded_image_path)
```

### Step 3: Extract Text using Tesseract OCR

Use Tesseract to convert the preprocessed image into text.
```python
def extract_text_from_image(preprocessed_image):
    extracted_text = pytesseract.image_to_string(preprocessed_image)
    print("Extracted Text:\n", extracted_text)
    return extracted_text

extracted_text = extract_text_from_image(preprocessed_image)
```
### Step 4: Extract Entities using Regex

Use regular expressions to extract numeric values with context-specific units such as kg, V, W, and dimensions in cm.
```python
def extract_entities(text):
    entities = {}
    weight_match = re.search(r'(\d+\.?\d*)\s?kg', text, re.IGNORECASE)
    if weight_match:
        entities['weight'] = weight_match.group(1) + ' kg'
    
    voltage_match = re.search(r'(\d+\.?\d*)\s?v', text, re.IGNORECASE)
    if voltage_match:
        entities['voltage'] = voltage_match.group(1) + ' V'
    
    wattage_match = re.search(r'(\d+\.?\d*)\s?w', text, re.IGNORECASE)
    if wattage_match:
        entities['wattage'] = wattage_match.group(1) + ' W'
    
    dimensions_match = re.search(r'(\d+\.?\d*)\s?x\s?(\d+\.?\d*)\s?x\s?(\d+\.?\d*)\s?cm', text, re.IGNORECASE)
    if dimensions_match:
        entities['dimensions'] = f"{dimensions_match.group(1)} x {dimensions_match.group(2)} x {dimensions_match.group(3)} cm"

    return entities

entities = extract_entities(extracted_text)
print("Extracted Entities:", entities)
```
### Example Output

Extracted Text from Image:
Power: 1200W | Voltage: 230V | Weight: 5.6kg | Size: 24x12x5cm
Extracted Entities:
{
  "weight": "5.6 kg",
  "voltage": "230 V",
  "wattage": "1200 W",
  "dimensions": "24 x 12 x 5 cm"
}


