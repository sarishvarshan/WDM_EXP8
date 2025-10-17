### EX NO:8 Web Scraping On E-commerce platform using BeautifulSoup
### DATE: 17/10/25
### NAME: SARISH VARSHAN V
### REG NO: 212223230196
### AIM: To perform Web Scraping on Amazon using (beautifulsoup) Python.
### Description: 
<div align = "justify">
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique 
to extract unstructured data and store that data either in a local file or in a database. 
There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. 
One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
<p>The basic steps involved in web scraping are:
<p>1) Loading the document (HTML content)
<p>2) Parsing the document
<p>3) Extraction
<p>4) Transformation

### Procedure:

1) Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
2) Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
3) Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
4) Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
5) Return sorted product data as a list of dictionaries.
6) Call get_amazon_products(search_query) to get product data based on the user's search query.
7) Check if products are found; if not, display "No products found."
8) Visualize Product Data using a Bar Chart

### Program:
```PYTHON

import requests
from bs4 import BeautifulSoup
import matplotlib.pyplot as plt
import re

def get_snapdeal_products(search_query):
    url = f'https://www.snapdeal.com/search?keyword={search_query.replace(" ", "%20")}'
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36'
    }

    response = requests.get(url, headers=headers)
    products_data = []

    if response.status_code == 200:
        soup = BeautifulSoup(response.content, 'html.parser')
        products = soup.find_all('div', {'class': 'product-tuple-listing'})

        for product in products:
            title = product.find('p', {'class': 'product-title'})
            price = product.find('span', {'class': 'product-price'})
            discount = product.find('div', {'class': 'product-discount'}) or product.find('span', {'class': 'product-discount'})
            rating = product.find('div', {'class': 'filled-stars'})  # rating via style width

            if title and price:
                product_name = title.text.strip()
                product_price = float(price.get('data-price', '0'))
                product_discount = discount.text.strip() if discount else "No discount"
                product_rating = rating['style'].split(':')[-1].split('%')[0].strip() + "%" if rating else "No rating"

                products_data.append({
                    'Product': product_name,
                    'Price': product_price,
                    'Rating': product_rating,
                    'Discount': product_discount
                })

                # Print each product details
                print(f'Product: {product_name}')
                print(f'Price: ₹{product_price}')
                print(f'Rating: {product_rating}')
                print(f'Discount: {product_discount}')
                print('---')
    else:
        print('Failed to retrieve content')

    return products_data

# Main execution
if __name__ == "__main__":
    search_query = input('Enter product to search on Snapdeal: ')
    products = get_snapdeal_products(search_query)


```

### Output:
<img width="1241" height="633" alt="image" src="https://github.com/user-attachments/assets/345bc532-ecd0-4549-bf96-ab6dcc539ebd" />


### Result:
Thus,To perform Web Scraping on Amazon using (beautifulsoup) Python is executed successfully.
