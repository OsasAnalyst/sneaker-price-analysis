# Sneaker Price Analysis System

![Sneaker Price Analysis Banner](https://github.com/user-attachments/assets/54392658-910b-4997-92ab-3efa274c1ef0)

## Executive Summary

This project presents an automated **Sneaker Price Analysis System** that collects and compares prices from major retail platforms — primarily **Nike** and **Zappos**. It uncovers pricing trends, platform-specific differences, and market behavior for popular sneaker models through web scraping, data processing, and visualization.

From the results, **Nike sneakers average $138.63**, while **Zappos averages $102.50**, showing a **34% higher pricing gap** on Nike’s end. Visualizations confirm that Nike focuses heavily on **premium and limited editions**, while Zappos offers a **broader, budget-friendly range**.  
Premium colorways like *“Cave Stone and Black”* and *“Baroque Brown and Sail”* command the highest prices, while models with *unknown colorways* or *standard editions* tend to sell for less. These findings give a clear picture of how each platform positions itself in the sneaker market.

The full pipeline automates data scraping, cleaning, transformation, and storage, producing a ready-to-analyze dataset for Power BI or other analytics tools. By automating the collection process, the system reduces manual effort by over **90%**, ensuring reliable and up-to-date insights for **retailers, analysts, and sneaker enthusiasts** who want to track pricing, spot opportunities, or benchmark competitiveness.

---

## Project Objective

The goal of this project is to build a **scalable sneaker price intelligence system** that automates the collection, comparison, and analysis of sneaker prices from multiple online retail platforms.

### Key Objectives:
- **Quantify price variation** across platforms, models, and editions  
- **Detect pricing patterns** driven by brand, model, or colorway  
- **Identify resale potential** by highlighting undervalued models  
- **Provide structured data** for visualization and trend tracking  
- **Automate data updates** to replace manual, repetitive price checks  

This project demonstrates how automation and data analytics can reveal valuable pricing insights in the sneaker market. In the future, the system can be extended to include **resale platforms like StockX**, enabling full **retail-to-resale market intelligence**.

---


## Data Collection

The data collection stage is where we build the foundation of this sneaker price analysis project.  
Our goal was to automatically gather up-to-date sneaker listings from **[Nike](https://www.nike.com/)** and **[Zappos](https://www.zappos.com/)**, focusing on consistent product attributes that allow us to compare prices and trends across both retail platforms.

To achieve this, we used a combination of **Requests** and **BeautifulSoup** to scrape data directly from product listing pages. Since both Nike and Zappos expose most of their product information in static HTML, this approach was efficient and reliable without needing Selenium or JavaScript rendering.

Across both platforms, we collected the following key fields:
- **Brand**  
- **Model / Product Name**  
- **Colorway**  
- **Release Date** (where available)  
- **Retail Price**  
- **Product URL**  
- **Image URL**  
- **Platform** (Nike or Zappos)

After collecting data from both sources, we combined them into a single structured dataset — ready for cleaning, transformation, and visualization.

---

### Nike Scraping ([Visit Nike](https://www.nike.com/))

In the Nike scraping phase, we targeted a curated list of popular sneaker models such as *Air Jordan 1 Retro High*, *Air Force 1*, and *Nike Dunk Low*. The scraper uses a standardized search approach and extracts structured product details including model names, prices, images, and URLs.

We also built a **model normalization function** to map inconsistent product titles (like “Air Jordan 1 Retro OG” or “AJ1 High”) to a clean set of standardized model names. This ensures consistency when comparing across multiple platforms.

After running the scraper, each Nike product entry included:
- Brand (Nike)
- Standardized model name
- Colorway (if detected)
- Retail price (cleaned and converted)
- Product URL
- Image link
- Platform (Nike)

The output was saved as a CSV file:
```python
nike_df.to_csv("nike_products.csv", index=False)
````

---

### Zappos Scraping ([Visit Zappos](https://www.zappos.com/))

For Zappos, the approach was similar but slightly adjusted to match the site’s HTML structure.
Each product card on Zappos includes brand, title, and price information, so our scraper extracts these values and applies another **normalization layer** to align product names with our Nike dataset.

We also introduced a **colorway extraction function** that intelligently removes generic descriptors like “shoes”, “sneakers”, or “running” to isolate the actual colorway name — e.g., “Baroque Brown and Sail”.

Each Zappos listing included:

* Brand (filtered for Nike)
* Model (standardized)
* Colorway
* Retail price
* Product and image URLs
* Platform label (“Zappos”)

Results were saved as:

```python
zappos_df.to_csv("zappos_products.csv", index=False)
```

---

### Combined Dataset

After completing both scrapers, we merged the Nike and Zappos datasets into a single DataFrame for analysis.
This combined dataset became the backbone of the project — allowing us to compare retail prices across platforms, evaluate how model and colorway affect pricing, and visualize patterns in Power BI.

Each record in the final dataset represents a unique sneaker entry with consistent fields across both sources, ensuring it’s ready for downstream analysis like pricing gaps, brand positioning, and colorway-based price segmentation.

---


## Exploratory Data Analysis (EDA)

This section dives into the insights uncovered after cleaning and merging the data from **Nike** and **Zappos**. The goal of the EDA was to understand pricing trends, platform-specific differences, and edition-level pricing behavior across sneaker models.


### Price Distribution Across Platforms

This visualization compares how Nike and Zappos distribute their sneaker prices.  

- Nike’s prices are tightly clustered toward the higher end, showing the brand’s focus on premium pricing.  
- Zappos displays a much wider price range, from affordable to high-end sneakers, appealing to a more diverse audience.  
- Overall, Nike positions itself in the premium segment, while Zappos serves a broader retail market.

![Price_Distribution_Across_Platform](https://github.com/user-attachments/assets/3972ec8a-bb7c-4bee-a4ae-cc4d56ba229f)


---


### Price Distribution by Platform

![price_distribution_by_platform](https://github.com/user-attachments/assets/bc9ce586-1a88-431e-85a7-7b4dd5ad699d)

---

## Recommendations  

From the analysis, it’s clear that Nike and Zappos occupy different ends of the sneaker retail spectrum.  
Nike maintains a **premium-focused pricing strategy**, targeting customers who value exclusivity and brand appeal. Zappos, on the other hand, caters to a **broader audience**, offering a mix of budget and high-end options.  

For **buyers**, Zappos is often the better choice for affordable deals. For **resellers or analysts**, Nike’s consistent premium pricing provides a benchmark for identifying sneakers that hold or increase in value.  
Premium models like the **Air Max 97**, **Air Jordan 4 Retro**, and exclusive colorways such as **“Cave Stone and Black”** should be prioritized when assessing resale potential.  
Differences in average prices across platforms also present clear **arbitrage opportunities** — buying from one platform at a lower rate and selling on another where prices trend higher.  

---

## Conclusion  

This project confirms that sneaker prices differ sharply across platforms, models, and editions.  
Nike’s strong brand positioning allows it to charge premium prices consistently, while Zappos competes through price diversity and accessibility.  
These findings give **practical insight** into how pricing strategies affect market segmentation and how consumers, retailers, and resellers can respond.  
In short, the analysis gives a clear picture of how value is created, distributed, and perceived in the sneaker market.  

---

## Limitations  

While the results are meaningful, there are some boundaries to note.  
The dataset only covers **Nike and Zappos** within the **U.S. market**, meaning the findings might differ in other regions.  
The analysis captures prices at one point in time — without tracking **seasonal shifts**, **discounts**, or **promotions** that could alter market dynamics.  
Additionally, missing or incomplete data for some colorways and editions may introduce slight bias in average prices.  
These limitations highlight why continuous data collection is key for more accurate, long-term insights.  

---

## Future Work  

There are several ways to expand this project.  
Future iterations could include **additional resale platforms** such as **StockX** or **GOAT** to deepen comparison and calculate real-time resale premiums.
Incorporating **time-series tracking** could reveal how sneaker prices fluctuate after release dates or during sales cycles.  
Finally, automating **scheduled data refreshes** would allow the system to track price movements continuously and provide live insights for decision-making.  

---

## 🏁 Closing Remark  

This project shows how data can uncover clear market insights and bridge the gap between retail strategy and consumer value.  

📌 **Author:** [Osaretin Idiagbonmwen](https://www.linkedin.com/in/osaretin-idiagbonmwen-33ab85339)  
📩 **Email:** oidiagbonmwen@gmail.com  


