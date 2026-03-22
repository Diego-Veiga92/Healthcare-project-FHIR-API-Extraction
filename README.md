# Healthcare-project-FHIR-API-Extraction

## 📌 Project Overview
This project focuses on the extraction, transformation, and analysis of electronic health records (EHR) using the **HL7 FHIR (Fast Healthcare Interoperability Resources)** standard. Using the public **HAPI FHIR R4** server, I developed a robust data pipeline to retrieve patient resources and prepare them for clinical data science applications.

## 🚀 Key Features
- **API Data Ingestion:** Automated extraction of 3,000+ patient records using Python.
- **Pagination Handling:** Implementation of recursive loops to navigate FHIR search bundles via `next` links.
- **Data Profiling:** Identification and mitigation of class imbalances (Gender/Demographics) found in synthetic datasets.
- **Bronze Layer Storage:** Persistence of raw JSON payloads for reproducibility.

## 🛠️ Technologies Used
- **Language:** Python
- **Libraries:** `requests`, `pandas`, `tqdm` (progress tracking), `json`
- **Standard:** HL7 FHIR R4
- **Source:** [HAPI FHIR Public Server](https://hapi.fhir.org/baseR4/swagger-ui/)

## 📊 The Extraction Pipeline
The extraction process follows a "Bronze Layer" approach in a Medallion Architecture:
1. **Request:** Querying the `/Patient` endpoint with a `_count=500` parameter.
2. **Sort:** Utilizing `_sort=_id` to ensure linear database crawling.
3. **Loop:** Following the `relation: next` URL provided in the FHIR Bundle until the target record count is reached.
4. **Validation:** Sanity checks on gender distribution and resource keys.

## 📉 Initial Data Insights
During the initial pull, a significant **selection bias** was observed in the public sandbox:
- **Total Records:** 8,362
- **Gender Distribution:**  female - 4,067 / male - 2,708 / unknown - 1184 / other - 403
