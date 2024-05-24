# Python PDF Processing to Postgresql Tutorial

## Query

Produce a Python function that extracts information from inaccessible and damaged PDFs, inferring metadata and logical tag structures, and performing OCR to extract useful text and table data. All data should be returned in Python dictionaries that are structured to facilitate easy data upload to a Postgresql 16 database. Then, write a tutorial for setting up the Postgresql database and using the Python function to process PDF data and upload it to the database.

## wizardcoder Response

To extract information from damaged or inaccessible PDFs, we can use libraries like PyPDF2, which is a high-level interface to the Portable Document Format (PDF) files. This library provides an abstraction layer that allows us to read and modify PDF files without needing to worry about the internals of the format itself. However, it does not handle images or complex layouts well.

Here's a sample Python function that uses PyPDF2 to extract metadata and text from a given PDF file:

```python
import re
from collections import OrderedDict

import fitz
from pdfminer.high_level import extract_text
from pdfminer.layout import LAParams

def pdf_to_dict(filepath):
    # Load the PDF file using PyPDF2 and extract metadata
    with fitz.open(filepath) as doc:
        metadata = OrderedDict()
        for i in range(len(doc.metadata)):
            k, v = doc.metadata[i]
            if not isinstance(v, str):
                continue  # Skip non-string values like binary data
            metadata[k] = v
    
    # Extract text using PDFMiner
    laparams = LAParams()
    with open(filepath, "rb") as f:
        pdf_text = extract_text(f, laparams=laparams)
    
    return metadata, pdf_text.strip()
```

This function first opens the PDF file using PyPDF2 and iterates through its metadata to create a dictionary of key-value pairs. It then uses PDFMiner 
to extract text from the file and returns both the metadata and the extracted text.

Next, we can use libraries like Tesseract OCR to perform optical character recognition (OCR) on the PDF's images to extract useful text. Here's an 
updated function that does this:

```python
import re
from collections import OrderedDict

import fitz
from pdfminer.high_level import extract_text, LAParams
import pytesseract

def pdf_to_dict(filepath):
    # Load the PDF file using PyPDF2 and extract metadata
    with fitz.open(filepath) as doc:
        metadata = OrderedDict()
        for i in range(len(doc.metadata)):
            k, v = doc.metadata[i]
            if not isinstance(v, str):
                continue  # Skip non-string values like binary data
            metadata[k] = v
    
    # Extract text using PDFMiner and OCR images
    laparams = LAParams()
    with fitz.open(filepath) as doc:
        pdf_text = extract_text(f, laparams=laparams)
    for page in doc:
        image_list = page.get_images()
        for img in image_list:
            text = pytesseract.image_to_string(img[0], lang='eng')  # Use English as the OCR language
            pdf_text += '\n' + text.strip()  # Add extracted text to PDF text
    
    return metadata, pdf_text.strip()
```

This function uses PyTesseract to perform OCR on each page of the PDF and concatenates the extracted text with the PDF text from PDFMiner.

To set up PostgreSQL 16, you'll need to download it and install it on your machine. You can then create a new database using the `CREATE DATABASE` 
command in the terminal or graphical client of your choice. Once you have a database created, we can create tables to store our extracted data:

```sql
CREATE TABLE metadata (
    id SERIAL PRIMARY KEY,
    filename VARCHAR(255) NOT NULL UNIQUE,
    title TEXT,
    author TEXT,
    creator TEXT,
    producer TEXT,
    creation_date DATE,
    modified_date DATE,
    subject TEXT,
    keywords TEXT
);

CREATE TABLE text (
    id SERIAL PRIMARY KEY,
    filename VARCHAR(255),
    page INT NOT NULL,
    text TEXT,
    FOREIGN KEY (filename) REFERENCES metadata(filename)
);
```

We'll need to add a new column for each key-value pair we extract from the PDF, but it's important to note that some keys might not be present in every 
PDF. Therefore, it's best to use `VARCHAR` instead of `TEXT` for columns like `title`, `author`, and `creator`. We also need a table to store the 
extracted text on each page of the PDF, with a foreign key relationship to the metadata table.

Finally, we can modify our Python function to insert data into these tables:

```python
import re
from collections import OrderedDict

import fitz
from pdfminer.high_level import extract_text, LAParams
import pytesseract

def pdf_to_dict(filepath):
    # Load the PDF file using PyPDF2 and extract metadata
    with fitz.open(filepath) as doc:
        metadata = OrderedDict()
        for i in range(len(doc.metadata)):
            k, v = doc.metadata[i]
            if not isinstance(v, str):
                continue  # Skip non-string values like binary data
            metadata[k] = v
    
    # Extract text using PDFMiner and OCR images
    laparams = LAParams()
    with fitz.open(filepath) as doc:
        pdf_text = extract_text(f, laparams=laparams)
    for page in doc:
        image_list = page.get_images()
        for img in image_list:
            text = pytesseract.image_to_string(img[0], lang='eng')  # Use English as the OCR language
            pdf_text += '\n' + text.strip()  # Add extracted text to PDF text
    
    # Insert metadata into the database
    cur = conn.cursor()
    filename = filepath.split("/")[-1]  # Extract filename from path
    try:
        cur.execute("INSERT INTO metadata (filename, title, author, creator, producer, creation_date, modified_date, subject, keywords) VALUES (%s, %s, 
%s, %s, %s, %s, %s, %s)",
                  (filename, metadata['Title'], metadata.get('Author'), metadata.get('Producer'), metadata.get('CreationDate'),
                   metadata.get('ModDate'), metadata.get('Subject'), metadata.get('Keywords')))
    except psycopg2.IntegrityError:  # Ignore duplicates
        pass
    
    # Insert extracted text into the database
    cur.execute("SELECT id FROM metadata WHERE filename = %s", (filename,))
    metadata_id = cur.fetchone()[0]
    for i in range(len(doc)):
        page_text = re.sub(r'\W+', ' ', pdf_text)  # Replace non-word characters with spaces
        cur.execute("INSERT INTO text (filename, page, text) VALUES (%s, %s, %s)", (filename, i+1, page_text))
    
    conn.commit()
```

In this example, we're using psycopg2 to interact with PostgreSQL and inserting the metadata and extracted text into their respective tables. Note that 
we're using `try-except` to catch any integrity errors caused by duplicate filenames in the metadata table.

To use this function on a batch of PDFs, you can simply loop through them:

```python
import os
from pathlib import Path

for filepath in Path('/path/to/pdfs').glob('*.pdf'):
    pdf_to_dict(str(filepath))
```

This will insert metadata and extracted text for each PDF into the database, with foreign keys linking them together. To extract tables from the 
extracted text, you can use libraries like `tabula-py` or `pdfplumber`, which can detect and extract tables from a PDF. You may need to adjust the OCR 
settings or other preprocessing techniques to improve the quality of the extracted table data. 
