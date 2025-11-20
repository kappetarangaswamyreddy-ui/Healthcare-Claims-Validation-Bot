# 🏥 Healthcare Claims Validation Bot  
### UiPath Document Understanding + Regex Extractor + Business Rules + Action Center

This project automates end-to-end **Healthcare Claim Data Validation** using UiPath’s  
**Document Understanding (DU), Regex Extractor, validation rules, and Action Center**  
for human-in-the-loop review.  

Invalid claims are automatically routed to **Action Center** with a dynamic form, while valid claims are logged to an Excel output file.

---

## 🚀 Features

### 🔹 1. Document Understanding Pipeline
- OCR + Digitize Document
- Taxonomy-based extraction (Taxonomy.json)
- Regex Extractor for structured fields
- Extracts:
  - Claim ID  
  - Member ID  
  - Patient Name  
  - Provider Name & NPI  
  - Service Date Range  
  - CPT/HCPCS  
  - ICD-10  
  - Units  
  - Charge Amount  

---

### 🔹 2. Business Rule Validation
Custom rule engine checks:

- ✔ Required fields  
- ✔ NPI Format (`[0-9]{10}`)  
- ✔ ICD-10 Code Format (`[A-Z][0-9]{2}[A-Z0-9]{0,4}`)  
- ✔ Service Date From <= Date To  
- ✔ Total Charge vs. Line Item Sum  
- ✔ Consistency checks  

Invalid claims → added to `dtError`  
Valid claims → added to `dtValid`

---

### 🔹 3. Action Center Integration
Invalid claims are routed to Orchestrator through a **Create Form Task**:

Form fields include:
- Claim ID (read-only)  
- Error Messages  
- Provider NPI  
- Resolution (Approve / Fix & Resubmit / Reject)  
- Reviewer Comments  

Form is built using **UiPath Form Designer**.

---

### 🔹 4. Excel Output
Two Excel files are generated:

