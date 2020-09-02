# Web Scrapper in Python(StackOverflow)

```python
# stackoverflow.py

import requests
from bs4 import BeautifulSoup

# step 1. get the pages
# step 2. make the requests
# step 3. extract the jobs
URL = f"https://stackoverflow.com/jobs?q=python&sort=i"

def get_last_page():
    result = requests.get(URL)
    soup = BeautifulSoup(result.text, "html.parser")
    pages = soup.find("div", {"class":"pagination"}).find_all("a")
    last_page = pages[-2].get_text(strip=True)
    return int(last_page)

def extract_job(html):
    title = html.find("div", {"class":"-title"}).find("h2").find("a")["title"]
    # recursive=False > span안의 span까지 가져오는 것을 방지
    company, location = html.find("div", {"class":"-company"}).find_all("span", recursive=False)
    company = company.get_text(strip=True)
    location = location.get_text(strip=True).strip("-").strip("\r").strip("\n")
    job-id = html["data-jobid"]
    
	return {"title": title, "company": company, "location": location, "apply_link" : f"https://stackoverflow.com/jobs/{job_id}"}


def extract_jobs(last_page):
    jobs = []
    for page in range(last_page):
        print(f"Scrapping SO: Page {page}")
        result = requests.get(f"{URL}&pg={page+1}")
        soup = BeautifulSoup(result.text, "html.parse")
        results = soup.find_all("div", {"class":"-job"})
		for result in results:
            job = extract_job(result)
            jobs.append(job)
     return jobs
    
def get_jobs():
    last_page = get_last_page()
    jobs = extract_jobs(last_page)
    return []
```

```python
# main.py
from indeed import get_jobs as get_indeed_jobs
from so import get_jobs as get_so_jobs
from save import save_to_file

so_jobs = get_so_jobs()
indeed_jobs = get_indeed_jobs()
jobs = so_jobs + indeed_jobs
save_to_file(jobs)

# Comma Separeted Values


```

```python
# save.py
import csv

def save_to_file(jobs):
    file = open("jobs.csv", mode="w")
    writer = csv.writer(file)
    writer.writerow("title", "company", "location", "link")
    for job in jobs:
        writer.writerow(list(job.values()))
    return
    
```



출처: [노마드 아카데미(Python으로 웹 스크래퍼 만들기)](https://nomadcoders.co/python-for-beginners/lobby)