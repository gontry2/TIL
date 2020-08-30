# Web Scraper in Python(indeed)

[beutifulsoup site](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

```python
# temp_indeed.py #
import requests
from bs4 import BeautifulSoup

indeed_result = requests.get("https://www.indeed.com/job?q=pythons&limit=50")

# soup: 데이터를 추출하고 탐색할 수 있음.
indeed_soup = BeautifulSoup(indeed_result.text, "html.parse")


## Extracting Indeed Pages ##
pagination = indeed_soup.find("div, {"class": "pagination"}")

links = pagination.find_all("a")
pages = []
# 페이지 마지막 << Next >> 제외
for link in links[:-1]:
    pages.append(int(link.string))
max_page = pages[-1]

## Requesting Each Page ##
for n in range(max_page):
    print(f"{n*50}")

```



```python
#indeed.py
import requests
from bs4 import BeautifulSoup

LIMIT = 50
URL = f"https://www.indeed.com/job?q=pythons&limit={LIMIT}"

def extract_indeed_pages():
    result = requests.get(URL)
    soup = BeautifulSoup(result.text, "html.parse")
    pagination = soup.find("div, {"class": "pagination"}")

    links = pagination.find_all("a")
    pages = []
    for link in links[:-1]:
        pages.append(int(link.string))
        
    max_page = pages[-1]
    return max_page

```



```python
# main.py
from indeed import extract_indeed_pages, extract_indeed_jobs

last_indeed_page = extract_indeed_pages()
```



```python
# indeed.py
...

def extract_job(html):
    ## Extracting titles ##
    # anchor의 속성이 title.
    title = html.find("div", {"class":"title"}).find("a")
    ["title"]
    ## Extracting Companies ##
    company = html.find("div", {"class": "company"})
    company_anchor = company.find("a")
    if company_anchor is not None:
       company = str(company_anchor.string)
    else:
       company = str(company.string)
    company = company.strip()
    location = html.find("div", {"class": "recjobLoc"})["data-rc-loc"]
    job_id = html["data-jk"]
    return { "title": title, "company": company, "location": location, "link", f"https://www.indeed.com/viewjob?jk={job_id}" }


def extract_indeed_jobs(last_page):
    jobs = []
    for page in range(last_page):
        print(f"Scrapping page {page}")
        result = requests.get(f"{URL}&start={page*LIMIT}")
        soup = BeautifulSoup(result.text, "html.parser")
        results = soup.find_all("div", {"class": "jobsearch-SerpJobCard"})
        for result in results:
            job = extract_job(result)
            jobs.append(job)
    return jobs


```



```python
# main.py
...

indeed_jobs = extract_indeed_jobs(last_indeed_page)
```



```python
# indeed.py
...

def get_jobs():
    last_page = extract_indeed_pages()
    jobs = extract_indeed_jobs(last_page)
    return jobs


# main.py
from indeed import get_jobs as get_indeed_jobs
indeed_jobs = get_indeed_jobs()
print(indeed_jobs)
```



출처: [노마드 아카데미(Python으로 웹 스크래퍼 만들기)](https://nomadcoders.co/python-for-beginners/lobby)