---
title:  "Scrap Job Site Using Scrapy"
---

In this blog I am going to scrap www.seek.com.au using beautiful soup and scrapy.

To do that I need to create a scrapy project first. First I need to select the directory where I want to create the project.

```
scrapy startproject scrapjobs
```

This will create a scrapjobs directory with the following contents:

![](/img/Annotation194706.jpg)

Spiders are classes. It needs to be defined which Scrapy uses to scrape information from a website (or a group of websites). They must subclass scrapy.Spider and define the initial requests to make, optionally how to follow links in the pages, and how to parse the downloaded page content to extract data.

Here goes my first Spider dsspider.py. This needs to saved under scrapjobs/spiders directory.


```python
import scrapy
import requests
from bs4 import BeautifulSoup

class JobSpider(scrapy.Spider):
    name = 'datasciencespider'

    start_urls = ['https://www.seek.com.au/Data-Science-jobs/in-All-Australia']

    def parse(self, response):
        # follow links to job pages
        for href in response.css('a._2iNL7wI::attr(href)'):
            yield response.follow(href, self.parse_job)

        yield {
            'job_url': response.url
        }
```

Spider defines some attributes and methods:

**name**: identifies the Spider. It must be unique within a project.

**start_urls**: This list will used by the default implementation of start_requests() to create the initial requests of spider.

**parse()**: a method that will be called to handle the response downloaded for each of the requests made. The response parameter is an instance of TextResponse that holds the page content and has further helpful methods to handle it.

The parse() method usually parses the response, extracting the scraped data as dicts and also finding new URLs to follow and creating new requests (Request) from them.

From the given URL we get the list of jobs. If I right click one of the job we see following html tags.

![](/img/SeekUrl200148.jpg)

From there we can follow the classes defined **a._2iNL7wI::attr(href)** and fetch the href location which will open the job.

After opening the job I need to fetch job title, description, company, location, salary, work type, and the job listing date.

Let's try to get job title first. If we inspect what html tags we have to deal with we get following:

![](/img/SeekJobTitle.jpg)

It has span and data-automation tag init. Nice!

Using beutiful soup we can easily get the info we need.

```
soup.findAll(tagName, {attrName: attrValue})
```

- tagName = 'Span'
- attrName = 'data-automation'
- attrValue = 'job-detail-title'

Let's check other info. Looks like description, company, work type, and the job listing date all follows the same rule. Easy then.

How about Salary? Location?

![image.png](/img/SeekSalaryLocation.jpg)

They does not have any class or tag with them. It might be tricky. One thing I can do. There is jobInfoHeader tag where all the info are encapsulated. Let's grab that first. Interesting! I have all information now. If I iterate through I can have all of them. Great!

I have create a dictionary and going through one by one and store information in dictionary. Done!

It does not look like a pretty solution. But I get the idea. Will come back to this if I need more elegant solution.


```python
import scrapy
import requests
from bs4 import BeautifulSoup

class JobSpider(scrapy.Spider):
    name = 'datasciencespider'

    start_urls = ['https://www.seek.com.au/Data-Science-jobs/in-All-Australia']

    def parse(self, response):
        # follow links to author pages
        for href in response.css('a._2iNL7wI::attr(href)'):
            yield response.follow(href, self.parse_job)

        # bHpQ-bp
        # follow pagination links
        for href in response.css('a.bHpQ-bp::attr(href)'):
            yield response.follow(href, self.parse)

    def parse_job(self, response):

        def extract_job_title(query):

            resultStr = ""

            try:
                # response = requests.get(query)
                soup = BeautifulSoup(response.body, 'lxml')
                element = soup.findAll("span", {"data-automation": "job-detail-title"})
                resultStr = element[0].text
            except:
                resultStr = ""

            return resultStr

        def extract_job_info(tagName, attrName, attrValue):

            resultStr = ""

            try:
                # response = requests.get(query)
                soup = BeautifulSoup(response.body, 'lxml')
                element = soup.findAll(tagName, {attrName: attrValue})
                resultStr = element[0].text
            except:
                resultStr = ""

            return resultStr

        def get_job_info(spanName, attrName, attrValue):
            '''
            Check tag name and return value where attrname and attvalue matches with attribute name and attribute value

            Example:
            <span data-automation="job-detail-title" class="_3FrNV7v _12_uzrS E6m4BZb"><span class=""><h1>Data Scientist</h1></span></span>

            If user sends span, data-automation, job-detail-title, it'll return Data Scientist
            '''

            job_soup = BeautifulSoup(response.body, 'lxml')

            element = job_soup.findAll(spanName, {attrName: attrValue})

            elementText = 'N/A'

            if len(element) > 0:
                elementText = element[0].text

            return elementText

        def get_job_information(whattofind):
            '''
            This method is specifcally for location and salary. For salary info there are no tags.
            It'll search every tag and if found sends location and salary back to user.a_tag
            '''

            job_soup = BeautifulSoup(response.body, 'lxml')

            thisdict = {
              "Job Listing Date": "N/A",
              "Location": "N/A",
              "Work Type": "N/A",
              "Salary": "N/A",
              "Classification": "N/A"
            }

            seekingJobListingDate = False
            seekingLocation = False
            seekingWorkType = False

            element = job_soup.find("section", {'aria-labelledby': 'jobInfoHeader'})

            for i in element:
                i_all = i.findAll('div')
                for j in i:
                    if 'Salary' in j.text:
                        thisdict["Salary"] = j.text.replace('Salary', '')
                    elif 'Classification' in j.text:
                        thisdict["Classification"] = j.text.replace('Classification', '')
                    else:
                        if j.text not in ['Job Information']:
                            if j.text == 'Job Listing Date':
                                seekingJobListingDate = True
                            elif j.text == 'Location':
                                seekingLocation = True
                            elif j.text == 'Work Type':
                                seekingWorkType = True
                            elif seekingJobListingDate == True:
                                seekingJobListingDate = False
                                seekingLocation = False
                                seekingWorkType = False
                                thisdict["Job Listing Date"] = j.text
                            elif seekingLocation == True:
                                seekingJobListingDate = False
                                seekingLocation = False
                                seekingWorkType = False
                                thisdict["Location"] = j.text
                            elif seekingWorkType == True:
                                seekingJobListingDate = False
                                seekingLocation = False
                                seekingWorkType = False
                                thisdict["Work Type"] = j.text

            return thisdict[whattofind]

        yield {
            'job_url': response.url
            , 'job_title': get_job_info('span', 'data-automation', 'job-detail-title')
            , 'job_desc': get_job_info('div', 'data-automation', 'mobileTemplate')
            , 'job_company': get_job_info('span', 'data-automation', 'advertiser-name')
            , 'job_detail_date': get_job_info('dd', 'data-automation', 'job-detail-date')
            , 'job_detail_work_type': get_job_info('dd', 'data-automation', 'job-detail-work-type')
            , 'job_right_to_work': get_job_info('span', 'data-automation', 'rightToWorkRequired')
            , 'job_salary': get_job_information('Salary')
            , 'job_classification': get_job_information('Classification')
            , 'job_location': get_job_information('Location')
        }

```

It looks like my spider is ready to scrap some data.

The simplest way to store the scraped data is by using Feed exports, with the following command:

```
scrapy crawl datasciencespider -o datasciencejobs.json
```

I have to go to the folder where scrapy.cfg file is available and execute above command. Yeah, it's scrapping jobs.

I got more than 2000 jobs in whole Australia. That was not too bad for first attempt of scrapping. Will come back later if I can improve performance.
