# Claimed Pilot

**Automating Prior Authorization (PA) Form Filling Using Multimodal Document Intelligence**

---

## 🧠 Purpose

Claimed Pilot is a proof-of-concept pipeline designed to automate the traditionally manual workflow of filling out Prior Authorization (PA) forms in the healthcare domain. This project addresses the challenge of extracting and aligning structured data (fillable PDFs) with unstructured multimodal inputs (scanned referral packages) to streamline insurance approval processes.

This was built as part of the **Headstarter** program to demonstrate:

- Rapid learning and adaptation to a new domain (healthcare).
- Real-world application of multimodal machine learning techniques.
- Creative problem solving with imperfect and ambiguous data.
- Effective use of open-source tools to automate tedious workflows.

---

## 📂 Input Structure

```
Input_Data/
├── Patient_A/
│   ├── PA.pdf
│   └── referral_package.pdf
├── Patient_B/
│   ├── PA.pdf
│   └── referral_package.pdf
...
```

- **PA.pdf**: Interactive, fillable insurance form with well-structured fields.
- **referral_package.pdf**: A collection of high-resolution scanned images (e.g., doctor's notes, test results, insurance cards), requiring OCR.

---

## ✅ Output

For each patient folder:
- 📝 A **filled PA form PDF** with extracted patient-specific data.
- ❗ A **missing-fields report** (Markdown or TXT), listing any required fields not found in the referral package.

---

## ⚙️ How It Works

### 1. **OCR & Preprocessing**
- The referral package is parsed using high-accuracy OCR (e.g., Tesseract or EasyOCR).
- Documents are split by page, denoised, and processed to extract clean, readable text.

### 2. **Field Matching**
- Form fields from the interactive PDF (AcroForm) are parsed.
- Natural Language Processing (NLP) and rule-based heuristics are used to match required fields (e.g., diagnosis, treatment history, provider ID) with the referral package text.

### 3. **Conditional Logic**
- The pipeline respects branching logic in the forms.
  - E.g., if "New Patient" is selected, "Existing Patient" is left blank.
  - Checkbox groups are handled with care to avoid invalid combinations.

### 4. **PDF Form Filling**
- For widget-based PDFs, fields are filled using `pdfrw`, `PyPDF2`, or similar tools.
- If a required field is missing, it is left blank and logged.

### 5. **Report Generation**
- A plain-text or Markdown report is created listing:
  - Unmatched required fields
  - Fields with low confidence
  - Any assumptions made during population

---

## 🧪 Sample Outputs

```
output_examples/
├── Patient_A/
│   ├── filled_PA_form.pdf
│   └── missing_fields_report.md
...
```

Each example shows the system’s ability to extract and infer structured data from unstructured evidence.

---

## 🚀 Getting Started

### 🔧 Installation

```bash
git clone https://github.com/[your-org]/claimed-pilot.git
cd claimed-pilot
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 📦 Dependencies

- `PyMuPDF` / `pdfplumber` – extract text from PA forms
- `pytesseract` / `EasyOCR` – OCR for scanned documents
- `pdf2image` – convert scanned PDFs to images
- `fpdf` / `reportlab` – generate filled PDFs and reports
- `transformers` – optional: for using LLMs to improve extraction

### 🧲 Run the Pipeline

```bash

```

---

## 🧠 Assumptions & Limitations

- Assumes referral packages are in English and scanned at readable DPI.
- Primarily built for AcroForm-based PDFs (interactive forms).
- Non-widget PDF support is experimental and not guaranteed.
- Some fields may not be extractable without fine-tuning domain-specific OCR/NLP models.
- Currently uses rule-based logic + keyword mapping; LLM-enhanced extraction is a potential v2 feature.

---

## 🗺 Project Structure

```

```

---

## 🔮 Future Improvements

- Integrate LLM-based entity extraction to improve matching accuracy.
- Add support for non-fillable PA forms via intelligent document overlay.
- Confidence scoring and human-in-the-loop correction interface.
- Extend to more insurance formats and healthcare services.

---

## 📣 Author

**Mohamed Al-Alimi**  
[GitHub Profile](https://github.com/your-username)  
Part of the **Headstarter 2025 Cohort**  
Project: **Claimed Pilot**
