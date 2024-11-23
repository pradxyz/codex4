import requests
from bs4 import BeautifulSoup
import csv

# Function to scrape product data from a webpage
def scrape_products(url):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    
    # Send a GET request to the webpage
    response = requests.get(url, headers=headers)
    if response.status_code != 200:
        print("Failed to fetch the webpage. Status code:", response.status_code)
        return []
    
    # Parse the HTML content of the page
    soup = BeautifulSoup(response.text, 'html.parser')

    # Customize the selectors to match the structure of the website
    products = []
    for product in soup.select('.product-class'):  # Replace with actual product container class
        name = product.select_one('.product-name-class').text.strip()  # Replace with actual name class
        price = product.select_one('.product-price-class').text.strip()  # Replace with actual price class
        rating = product.select_one('.product-rating-class').text.strip() if product.select_one('.product-rating-class') else "N/A"  # Replace with actual rating class
        products.append([name, price, rating])
    
    return products

# Function to save product data to a CSV file
def save_to_csv(products, filename):
    with open(filename, mode='w', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow(['Product Name', 'Price', 'Rating'])  # Header row
        writer.writerows(products)

# Main function
def main():
    url = input("Enter the URL of the e-commerce webpage to scrape: ")
    output_file = "products.csv"

    print("Scraping product data...")
    products = scrape_products(url)

    if products:
        print(f"Found {len(products)} products. Saving to {output_file}...")
        save_to_csv(products, output_file)
        print("Data saved successfully!")
    else:
        print("No products found or failed to scrape the webpage.")

if __name__ == "__main__":
    main()
