OCR-Based Invoice Classification with DistilBERT

This project aims to classify sections of invoices using Optical Character Recognition (OCR) and the DistilBERT model from Hugging Face's Transformers library.

Table of Contents

1.Introduction
2.Dependencies
3.How it Works
4.Usage
5.Model Training
6.API Endpoints
7.Future Improvements

1.Introduction

The primary goal of this project is to extract text from invoice images and classify the extracted segments into categories: company, date, address, total, and other.

2.Dependencies

Python 3.7+
Flask API
PyTesseract (OCR)
Bert Transformers (DistilBertTokenizerFast, DistilBertForSequenceClassification)
PIL (Pillow)
Pytorch

3.How it Works

Image Upload: The user uploads an invoice image to the Flask API.
Text Extraction: Using PyTesseract, the image undergoes OCR to extract text content.
Text Classification: The extracted text segments are tokenized using DistilBertTokenizerFast and then fed into a pre-trained DistilBERT model for sequence classification.
Response: The API returns the classified segments: company, date, address, total. If some fields are not detected, they are returned as null.

4.Usage

To set up and run the project:

Clone the repository: git clone (https://github.com/fathimazajel/image_invoice_reader_n)
Navigate to the project directory: cd /Users/fathimazajel/Documents/GitHub/image_invoice_reader
Install the required dependencies: pip install -r requirements.txt
Run the Flask app: Flask Run (app.py)

5.Model Training

Refer to  notebooks/my_model/main2.ipynb 
The model was trained using a labeled dataset of invoice texts. The process involved:

Labelling the data: The annotated files with bounding box coordinates was labelled using the labels provided.
Tokenization: The invoice texts were tokenized using DistilBertTokenizerFast.
Dataset Splitting: The dataset was split into training, validation, and test sets.
Model Initialization: DistilBertForSequenceClassification was initialized with the number of labels (classes).
Training: The model was trained using Hugging Face's Trainer utility.
Fine Tuning: The model was fine tuned to better the training loss and validation loss
Evaluation & Saving: The best model was saved for later use in the Flask app.
Test data preprocesiing: Text was extracted and tokenized inforder to run model.
For more details on the model training, refer to the modeling script in the repository.

6.API Endpoints Flask and Postman

Refer to  notebooks/my_model/app.py
/predict (POST):Using Postman api software we can run the Flask API link in the local host.
It will accept an invoice image and returns the classified text segments.

Steps:
1.Once the Flask app is running, it will be accessible at http://127.0.0.1:5000/.

2.Testing with Postman:
To test the API using Postman:

Open Postman.
Create a new request.
Set the HTTP method to POST.
Enter the Flask API endpoint (for instance, http://127.0.0.1:5000/predict).
In the "Body" tab, select "form-data".
Add a key named "image" and upload an invoice image as its value.
Click "Send" to make the request.
The API response will be displayed in Postman's result section.
Note: If you're using the web version of Postman, you may encounter issues connecting to localhost. It's recommended to use the Postman desktop application to avoid such issues.


7.Future Improvements

Improve accuracy by further tuning the DistilBERT model or trying other architectures.
Enhance OCR capabilities for better text extraction from varied invoice formats.
Implement a user-friendly front-end for better interaction.



===============================
Bonus Points

•	How would you enhance this data?
In terms of enhancing the data, there are several strategies one might consider:

a.Data Augmentation: Consider effective approaches to perform data augmentation for image data, like rotation, cropping, and color adjustments can be valuable.
b.Opt better methods of data extraction and labelling the data. Consider using Open Ai.
b.Data Cleaning: It's imperative to make sure the data is pristine. This involves eliminating any discrepancies and getting rid of irrelevant or inaccurate annotations. An important note here: if you're dealing with bounding box coordinates, ensuring a consistent format across the dataset can be a game-changer.
c.Collect More Data: Lastly, if the circumstances allow, gathering more data can be a boon. A more extensive dataset can potentially enhance the model's precision and its ability to generalize."


•	Can you containerize the solution(api) using docker and provide the necessary documentation on how to run it for inference?
    1. Create a Dockerfile
       First, you'll need a Dockerfile to specify how Docker should build the container for your API. Place this file in the root of your project directory:
            
            Code to run on Terminal:
            # Use an official lightweight Python image.
            # https://hub.docker.com/_/python
            FROM python:3.9-slim
            
            # Set the working directory in Docker
            WORKDIR /app
            
            # Copy local code to the container image.
            COPY . /app
            
            # Install any dependencies.
            RUN pip install --no-cache-dir -r requirements.txt
            
            # Service must listen to $PORT environment variable.
            # This default value facilitates local development.
            ENV PORT 5000
            
            # Run the web service on container startup.
            CMD [ "python", "app.py" ]
            
   2. Create a .dockerignore file
       You should also have a .dockerignore file to prevent any unwanted files from being included in the Docker image. This is similar to .gitignore for Git
            
  3. Build and Test the Docker Image
       First, navigate to your project directory, then build your Docker image:
            
            Code to run on Terminal:
            docker build -t my_api_image .
            
   After building the image, run it:
            
            Code to run on Terminal:
            docker run -p 5000:5000 my_api_image

   Now, your API should be up and running inside a Docker container, accessible at http://127.0.0.1:5000/.

  4. Documentation
          Running the Dockerized API for Inference

     Ensure you have Docker installed on your system. If not, download and install it from Docker's official website.
     Navigate to the project directory where the Dockerfile is located.
     Build the Docker image:

           Code to run on Terminal:
           docker build -t my_api_image

  Once the build completes, run the image:

          Code to run on Terminal:
          docker run -p 5000:5000 my_api_image

  Access the API at http://127.0.0.1:5000/. You can test it using tools like Postman or any web browser for GET routes.
  To stop the Docker container, find its container ID with:

            Code to run on Terminal:
            docker ps

  Then, stop it using:

            Code to run on Terminal:
            docker stop [CONTAINER_ID] 
            
Replace [CONTAINER_ID] with the actual ID from the previous command.
  

RESOURCES utilized:

Flask API
Flask Official Documentation: The go-to resource for all Flask-related questions.
[Flask Docs](https://flask.palletsprojects.com/en/2.0.x/)
Building a RESTful API with Flask: A great tutorial on how to structure and build APIs using Flask.
[Miguel Grinberg's Flask Mega-Tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)

Transformers and Hugging Face
Hugging Face's Transformers: The official documentation for Hugging Face's transformers library.
[Transformers Docs](https://huggingface.co/docs/transformers/index)
DistilBERT paper: Read more about the DistilBERT model.
[DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter](https://www.youtube.com/watch?v=cCs8exFrGE8)

Docker
Docker's Official Documentation: Comprehensive details on how to use Docker.
[Docker Docs](https://docs.docker.com)

Postman
Postman Learning Center: Official Postman documentation and tutorials.
[Postman Learning](https://learning.postman.com)
API testing using Postman: A beginner’s guide.
[API Testing using Postman](https://www.guru99.com/postman-tutorial.html)

PyTesseract and OCR
PyTesseract for OCR: Video by Neural Nine
[Python-tesseract (pytesseract)](https://www.youtube.com/watch?v=PY_N1XdFp4w)


