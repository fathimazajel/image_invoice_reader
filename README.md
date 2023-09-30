# image_invoice_reader
Invoice-Extraction-ML  A machine learning project aimed at extracting specific fields (Company Name, Amount, Address, Date) from scanned invoice images. This repository contains the entire pipeline, from preprocessing and Optical Character Recognition (OCR) to model training and evaluation.

Data: Contains raw and processed invoice images, with annotations to guide the extraction process.
Notebooks: Jupyter notebooks for exploratory data analysis, prototyping, and visual demonstrations.
Source: All source code, including data preprocessing, model definitions, and utility scripts.
Trained Models: Stored pre-trained models for quick deployment and evaluation.
Results: Logs, visualizations, and performance metrics.
Docs: Comprehensive documentation detailing every step of the project.
Tests: Unit tests to ensure code integrity and data validity.


Folder schema

invoice-extraction/
│
├── data/
│   ├── raw/                  # Raw, unmodified invoice images
│   ├── processed/            # Pre-processed images and extracted text files
│   ├── annotations/          # Annotated data (if you have any, for training purposes)
│   └── splits/               # Training, validation, and test data splits
│
├── notebooks/                # Jupyter notebooks for EDA, prototyping, etc.
│
├── src/
│   ├── preprocessing/        # Scripts/modules for data preprocessing
│   │   ├── __init__.py
│   │   └── ...
│   │
│   ├── models/               # Machine learning models, architecture definitions, etc.
│   │   ├── __init__.py
│   │   └── ...
│   │
│   ├── utils/                # Utility scripts/modules (e.g., for evaluation metrics)
│   │   ├── __init__.py
│   │   └── ...
│   │
│   └── main.py               # Main script to tie everything together, if necessary
│
├── trained_models/           # Saved model weights and parameters
│
├── results/                  # Logs, visualizations, and other results
│
├── docs/                     # Documentation
│
├── tests/                    # Unit tests
│   ├── data/                 # Test data
│   └── test_scripts/         # Test scripts/modules
│
├── .gitignore                # List of files and directories to be ignored by Git
├── README.md                 # Project description and user guide
├── LICENSE                   # Licensing information
└── requirements.txt          # List of python libraries required for your project
