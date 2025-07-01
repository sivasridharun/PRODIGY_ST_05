import requests
from bs4 import BeautifulSoup
import csv

def get_rating(text):
    return {"One": 1, "Two": 2, "Three": 3, "Four": 4, "Five": 5}.get(text, 0)

def scrape_books(pages=1):
    data = []
    for page in range(1, pages+1):
        url = f"https://books.toscrape.com/catalogue/page-{page}.html"
        soup = BeautifulSoup(requests.get(url).text, "html.parser")
        for book in soup.select("article.product_pod"):
            title = book.h3.a["title"]
            price = book.select_one(".price_color").text[1:]
            rating = get_rating(book.p["class"][1])
            data.append([title, price, rating])
    return data

def save_csv(data, filename="books.csv"):
    with open(filename, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerow(["Title", "Price", "Rating"])
        writer.writerows(data)

books = scrape_books(3)
save_csv(books)
print("Scraping complete. Data saved to books.csv.")
