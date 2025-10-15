Perfect 😎🔥 — let’s make this repo look **clean, professional, and ready for GitHub stars**.

Here’s your **tailored version** for your GitHub repo:
Repository name: `himesh-raghuwanshi/amazon-product-scraper`
And I’ll include the final `scraper.py` file structure too.

---

## 🧾 README.md

````markdown
# 🛒 Amazon Product Scraper (Python)

A simple **Amazon web scraper** that extracts **product names, prices, links, and images** from Amazon search pages using `BeautifulSoup` and `Requests`.  
Built by **Himesh Raghuwanshi** as part of a Python automation learning project.

---

## 🚀 Features
- Fetches **product title, price, link, and image**.  
- Exports all results to a CSV file.  
- Uses **headers** to simulate browser requests (prevents Amazon blocking).  
- Lightweight — no Selenium or heavy frameworks needed.  

---

## 🧠 Tech Stack
- 🐍 Python 3.x  
- 🌐 Requests  
- 🧩 BeautifulSoup4  
- 📄 CSV

---

## 🧩 Installation & Setup

### 1️⃣ Clone this repository
```bash
git clone https://github.com/himesh-raghuwanshi/amazon-product-scraper.git
cd amazon-product-scraper
````

### 2️⃣ Install dependencies

```bash
pip install requests beautifulsoup4 lxml
```

### 3️⃣ Run the script

```bash
python scraper.py
```

---

## 📊 Output

Scraped data will be saved in:

```
C:\Users\Himesh\Desktop\out.csv
```

| Product Name   | Price   | Link                                    | Image URL                                                     |
| -------------- | ------- | --------------------------------------- | ------------------------------------------------------------- |
| Redmi 12 5G    | ₹11,999 | [View on Amazon](https://amazon.in/...) | [https://m.media-amazon.com/](https://m.media-amazon.com/)... |
| Samsung M14 5G | ₹13,499 | [View on Amazon](https://amazon.in/...) | [https://m.media-amazon.com/](https://m.media-amazon.com/)... |

---

## ⚠️ Disclaimer

This scraper is made **for educational purposes only**.
Amazon’s data is protected by their [Terms of Service](https://www.amazon.in/gp/help/customer/display.html?nodeId=200270160).
Use responsibly and avoid excessive scraping.

---

## 💡 Future Enhancements

* 🔁 Add pagination scraping
* 🖥️ Create a Tkinter GUI interface
* ☁️ Save data in MongoDB/SQLite
* 📊 Build a Streamlit dashboard

---

## 👨‍💻 Author

**Himesh Raghuwanshi**
🎓 Student | AI & Data Science Enthusiast
🔗 [LinkedIn](https://www.linkedin.com/in/himesh-raghuwanshi)

---

## ⭐ Support

If you find this project useful, give it a **star ⭐** on GitHub — it keeps me motivated to build more open-source tools!

````

---

## 📂 `scraper.py`

```python
from bs4 import BeautifulSoup
import requests
import csv
import os

# ✅ Amazon Electronics Category URL (You can change category or filters)
URL = "https://www.amazon.in/s?i=electronics&rh=n%3A976419031%2Cp_36%3A630000-1500000%2Cp_n_condition-type%3A8609960031"

# ✅ Fake headers to avoid getting blocked
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.140 Safari/537.36",
    "Accept-Language": "en-US,en;q=0.9"
}

# ✅ Save file path
output_path = r"C:\Users\Himesh\Desktop\out.csv"

# Make sure the directory exists
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# ✅ Fetch and parse the webpage
response = requests.get(URL, headers=HEADERS)
soup = BeautifulSoup(response.content, "html.parser")

# ✅ Create and write to CSV
with open(output_path, "w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow(["Product Name", "Price", "Link", "Image"])

    for product in soup.find_all("div", {"data-component-type": "s-search-result"}):
        title = product.find("span", class_="a-size-medium a-color-base a-text-normal")
        if not title:
            title = product.find("span", class_="a-size-base-plus a-color-base a-text-normal")

        price = product.find("span", class_="a-price-whole")
        link = product.find("a", class_="a-link-normal s-no-outline")
        image = product.find("img", class_="s-image")

        writer.writerow([
            title.get_text(strip=True) if title else "N/A",
            price.get_text(strip=True) if price else "N/A",
            "https://www.amazon.in" + link['href'] if link else "N/A",
            image['src'] if image else "N/A"
        ])

print(f"✅ Data successfully saved to: {output_path}")
````

---



