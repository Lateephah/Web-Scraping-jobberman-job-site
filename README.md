# Web-Scraping-jobberman-job-site
Scraped  Jobberman job-site , extracted 3360 job postings (16 jobs posting per page * 210  pages). Python web scraping project

# 🌐 Jobberman Web Scraping & Data Collection Project

## 📌 Overview

This project focuses on **web scraping job listings from Jobberman** and transforming the extracted data into a structured dataset for analysis.

**Project Summary:**
Scraped Jobberman job site and extracted **3,360 job postings** *(16 jobs per page × 210 pages)* using Python.

The project implements a **multi-level scraping pipeline** that:

* Extracts job summaries from listing pages
* Visits individual job pages for additional details
* Aggregates data across hundreds of pages
* Outputs a clean dataset ready for analysis

---

## 🎯 Objectives

* Scrape job listings from Jobberman
* Extract structured job data from unstructured HTML
* Collect additional job details from individual job pages
* Handle pagination to gather large datasets (200+ pages)
* Store cleaned data in CSV format for analysis

---

## 📂 Project Structure

```
├── webscraping.ipynb   # Main notebook containing scraping logic
├── job_data.csv        # Output dataset (generated)
├── README.md           # Project documentation
```

---

## 🧪 Data Collected

The scraper extracts the following fields:

* `company_name`
* `job_title`
* `job_function`
* `industry`
* `workType`
* `Location`
* `Posted_Time`
* `Min_Qualification`
* `ExperienceLevel`
* `ExperienceLength`
* `Salary_range`
* `job_urls`

---

## ⚙️ Technologies Used

* Python
* BeautifulSoup (HTML parsing)
* Requests (HTTP requests)
* Pandas (data manipulation)
* Time (rate limiting)

---

## 🔍 Detailed Workflow

### 1. Scraping Job Listings (`scrap_jobs`)

This function handles the main listing page scraping:

* Sends a request to Jobberman
* Parses HTML using BeautifulSoup
* Extracts:

  * Job title
  * Company name
  * Job function
  * Posting time
  * Location, work type, and salary
* Collects job URLs for deeper scraping

It loops through all jobs on a page and builds lists for each feature before converting them into a dictionary.

---

### 2. Scraping Individual Job Details (`scrapeJobDetails`)

This function enhances the dataset by visiting each job's page:

Extracted fields:

* Industry
* Minimum Qualification
* Experience Level
* Experience Length

This creates a **multi-level scraping system (list page → detail page)**.

---

### 3. Pagination Handling (`scrap_pages`)

To scale data collection:

* Iterates through multiple pages using a loop
* Dynamically constructs URLs with page numbers
* Calls `scrap_jobs()` for each page
* Combines results using `pandas.concat()`

Example:

```
scrap = scrap_pages(num_pages=210)
```

---

### 4. Rate Limiting Strategy

To reduce the risk of blocking:

* The script pauses after every 10 pages:

```
if count % 10 == 0:
    time.sleep(2)
```

---

### 5. Data Storage

The final dataset is exported as a CSV file:

```
scrap.to_csv('job_data.csv')
```

---

## 📊 Sample Output

Example of the scraped dataset:

| company_name          | job_title                | Location | ExperienceLevel | Salary_range          |
| --------------------- | ------------------------ | -------- | --------------- | --------------------- |
| Blossom VA Services   | TikTok Poster            | Lagos    | Entry level     | NGN 150,000 - 250,000 |
| Ibat Travels and Tour | Graphics & Brand Manager | Lagos    | Entry level     | NGN 150,000 - 250,000 |
| Odixcity Consulting   | AI Engineer              | Remote   | Mid level       | NGN 400,000 - 600,000 |

---

## ⚠️ Challenges & Considerations

* Website structure may change, breaking selectors
* Some fields may return "N/A" when missing
* Large-scale scraping (200+ pages) increases runtime
* Requests without headers may risk blocking
* Heavy reliance on HTML class names (fragile)

---

## 💡 Future Improvements

* Add robust error handling (`try-except`)
* Include request headers (User-Agent)
* Implement retry logic for failed requests
* Store data in a database (PostgreSQL/MySQL)
* Use proxy rotation for large-scale scraping
* Convert pipeline into a reusable scraper class
* Schedule automated scraping (cron jobs)

---

## 📊 Key Learnings

* Building end-to-end web scraping pipelines
* Multi-page and multi-level scraping techniques
* Extracting structured data from messy HTML
* Handling pagination and scaling data collection
* Using Pandas for dataset construction

---

## 📌 Conclusion

This project demonstrates a **complete and scalable web scraping workflow**—from extracting job listings to building a structured dataset. The resulting dataset of **3,360 job postings** can be used for job market analysis, salary insights, or machine learning applications.

---

## 🤝 Contributing

Contributions are welcome! Feel free to fork this repository and submit a pull request.

---

## 📜 License

This project is open-source and available under the MIT License.

