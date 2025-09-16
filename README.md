**🧠 Contact Information Extraction with JSON Schema Validation**

**📘 Project Overview**

This project demonstrates how to extract structured contact information from unstructured chat messages using Python. It employs regular expressions (regex) and JSON Schema validation to ensure the extracted data adheres to a predefined structure.

**🔧 Key Features
**

a. Regex-Based Extraction: Utilizes regular expressions to identify and extract key information such as name, email, phone number, location, and age from chat messages.

b. JSON Schema Validation: Ensures the extracted data conforms to a specified JSON schema, validating the presence and format of each field.

c. Fallback Mechanism: In the absence of an API client, the system defaults to the regex-based extraction method.

**🛠 Installation & Setup**

To run this project locally, follow these steps:

Clone the Repository:

  git clone https://github.com/yourusername/contact-extraction.git
  cd contact-extraction


Set Up a Virtual Environment:

  python -m venv venv
  source venv/bin/activate  # On Windows, use `venv\Scripts\activate`


Install Dependencies:

  pip install -r requirements.txt


Run the Notebook:

  Open the notebook in Jupyter or execute it in Google Colab.

**📄 Usage**

The main function to extract and validate contact information is extract_info. Here's how you can use it:

  from your_module import extract_info
  
  chat_message = "Hi, I'm Rajiv Sharma. My email is rajiv.sharma@example.com and I'm 24. I live in Pune. My phone is +91-9876543210."

  extracted_data = extract_info(chat_message)
  print(extracted_data)


This will output a dictionary containing the extracted information, validated against the JSON schema.

**🧪 Example Output**

For the input:

  Hi, I'm Rajiv Sharma. My email is rajiv.sharma@example.com and I'm 24. I live in Pune. My phone is +91-9876543210.


The output will be:

  {
    "name": "Rajiv Sharma",
    "email": "rajiv.sharma@example.com",
    "phone": "+91-9876543210",
    "location": "Pune",
    "age": 24
  }

**🧪 Test Cases**

The project includes several test cases to validate the extraction process:

  Rajiv Sharma: Extracts all fields correctly.
  
  Priya: Missing name and phone number; fallback extraction is used.
  
  Ankit: Missing name and age; fallback extraction is used.

**📄 JSON Schema**

The JSON schema used for validation is as follows:

  {
    "type": "object",
    "properties": {
      "name": { "type": "string" },
      "email": { "type": "string" },
      "phone": { "type": "string" },
      "location": { "type": "string" },
      "age": { "type": "integer", "minimum": 0 }
    },
    "required": ["name", "email", "phone", "location", "age"]
  }
**
🧪 Validation Function
**
The validate_extracted function checks if the extracted data conforms to the JSON schema:

  from jsonschema import validate, ValidationError
  
  def validate_extracted(data, schema):
      try:
          validate(instance=data, schema=schema)
          print("✅ Validation successful")
      except ValidationError as e:
          print(f"❌ Validation failed: {e.message}")

**🧪 Sample Chat Messages**

Here are some sample chat messages and their expected outputs:

  Input:
  Hi, I'm Rajiv Sharma. My email is rajiv.sharma@example.com and I'm 24. I live in Pune. My phone is +91-9876543210.
  
  Output:
  {
    "name": "Rajiv Sharma",
    "email": "rajiv.sharma@example.com",
    "phone": "+91-9876543210",
    "location": "Pune",
    "age": 24
  }
  
  Input:
  Hello, this is Priya. You can reach me at priya_contact@gmail.com. Age: 30. Location: Bengaluru.
  
  Output:
  {
    "name": "Priya",
    "email": "priya_contact@gmail.com",
    "phone": "Unknown",
    "location": "Bengaluru",
    "age": 30
  }
  
  Input:
  Hey, it's Ankit — ankit123@mail.com. Phone 9998887776.
  
  Output:
  {
    "name": "Ankit",
    "email": "ankit123@mail.com",
    "phone": "9998887776",
    "location": "Unknown",
    "age": 0
  }
