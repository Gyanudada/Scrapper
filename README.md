# Scrapper
import requests
from bs4 import BeautifulSoup

def scrape_article_content(url):
    try:
        # Send an HTTP GET request to the URL
        response = requests.get(url)
        response.raise_for_status()

        # Parse the HTML content of the page using BeautifulSoup
        soup = BeautifulSoup(response.text, 'html.parser')

        # Find the article content based on the specific HTML structure of the website
        # You may need to inspect the webpage's HTML to determine the exact structure
        article_content = soup.find('div', class_='article-content')  # Example selector

        if article_content:
            # Extract and clean the text from the article content
            article_text = article_content.get_text()
            return article_text
        else:
            return "Article content not found on this page."

    except requests.exceptions.RequestException as e:
        return f"Error: {e}"

if __name__ == "__main__":
    url = input("Enter the URL of the news article: ")
    article_content = scrape_article_content(url)

    print("\nArticle Content:")
    print(article_content)
