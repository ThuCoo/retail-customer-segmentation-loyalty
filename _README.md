<h1> Customer Shopping Behavior Analysis </h1>

This is a project following Amlan Mohanty's walkthrough

- [Amlan Mohanty's walkthrough](https://youtu.be/5PrZvPeUw60?si=wNMZQK7p8cCpg5iV)

<h2> Project Summary </h2>
This project analyzes customers' shopping behavior using purchase records across various categories to uncover insights on spending patterns, customer patterns, product preference, and subscription behavior.

<h2> Problem Statement </h2>
A leading retail company wants to better understand its customers' shopping behavior in order to improve sales, customer satisfaction, and long-term loyalty.

- The management team has noticed changes in purchasing patterns across demographics, product categories, and sales channels (online vs. offline).
- They are particularly interested in uncovering which factors, such as discounts, reviews, seasons, or payment preferences, drive consumer decisions and repeat purchases.
- Analyze the company's consumer behavior dataset to answer the following overarching business question:
  **"How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?"**

<h2> Tools Used </h2>

- **Python** - Data Preparation and Modeling.
- **MS SQL Server** - Data Analysis.
- **Power BI** - Visualization and insights.
- **VS Code** - Development environment.

<h2> Dataset Summary </h2>

Rows: 3,900 \
Columns: 19 \
Key features:

- Customers' data: Age, Gender, Location, Subscription Status.
- Purchase Details: Item Purchased, Category, Purchased Amount (USD), Size, Color, Season.
- Shopping Behavior: Discount Applied, Promo Code Used, Previous Purchase, Frequency of Purchases, Review Rating, Shipping Type.

<h2> Exploratory Data Analysis using Python </h2>

**Data Loading**: Import dataset using pandas. \
**Initial Exploration**: Checking dataset's summary statistic.

|            | Customer ID | Age       | Gender | Item Purchased | Category | Purchase Amount (USD) | Location | Size | Color | Season | Review Rating | Subscription Status | Shipping Type | Discount Applied | Promo Code Used | Previous Purchases | Payment Method | Frequency of Purchases |
| ---------- | ----------- | --------- | ------ | -------------- | -------- | --------------------- | -------- | ---- | ----- | ------ | ------------- | ------------------- | ------------- | ---------------- | --------------- | ------------------ | -------------- | ---------------------- |
| **count**  | 3900.00     | 3900.00   | 3900   | 3900           | 3900     | 3900.00               | 3900     | 3900 | 3900  | 3900   | 3863.00       | 3900                | 3900          | 3900             | 3900            | 3900.00            | 3900           | 3900                   |
| **unique** | NaN         | NaN       | 2      | 25             | 4        | NaN                   | 50       | 4    | 25    | 4      | NaN           | 2                   | 6             | 2                | 2               | NaN                | 6              | 7                      |
| **top**    | NaN         | NaN       | Male   | Blouse         | Clothing | NaN                   | Montana  | M    | Olive | Spring | NaN           | No                  | Free Shipping | No               | No              | NaN                | PayPal         | Every 3 Months         |
| **freq**   | NaN         | NaN       | 2652   | 171            | 1737     | NaN                   | 96       | 1755 | 177   | 999    | NaN           | 2847                | 675           | 2223             | 2223            | NaN                | 677            | 584                    |
| **mean**   | 1950.50     | 44.068462 | NaN    | NaN            | NaN      | 59.764359             | NaN      | NaN  | NaN   | NaN    | 3.750065      | NaN                 | NaN           | NaN              | NaN             | 25.351538          | NaN            | NaN                    |
| **std**    | 1125.977353 | 15.207589 | NaN    | NaN            | NaN      | 23.685392             | NaN      | NaN  | NaN   | NaN    | 0.716983      | NaN                 | NaN           | NaN              | NaN             | 14.447125          | NaN            | NaN                    |
| **min**    | 1.00        | 18.00     | NaN    | NaN            | NaN      | 20.00                 | NaN      | NaN  | NaN   | NaN    | 2.50          | NaN                 | NaN           | NaN              | NaN             | 1.00               | NaN            | NaN                    |
| **25%**    | 975.75      | 31.00     | NaN    | NaN            | NaN      | 39.00                 | NaN      | NaN  | NaN   | NaN    | 3.10          | NaN                 | NaN           | NaN              | NaN             | 13.00              | NaN            | NaN                    |
| **50%**    | 1950.50     | 44.00     | NaN    | NaN            | NaN      | 60.00                 | NaN      | NaN  | NaN   | NaN    | 3.80          | NaN                 | NaN           | NaN              | NaN             | 25.00              | NaN            | NaN                    |
| **75%**    | 2925.25     | 57.00     | NaN    | NaN            | NaN      | 81.00                 | NaN      | NaN  | NaN   | NaN    | 4.40          | NaN                 | NaN           | NaN              | NaN             | 38.00              | NaN            | NaN                    |
| **max**    | 3900.00     | 70.00     | NaN    | NaN            | NaN      | 100.00                | NaN      | NaN  | NaN   | NaN    | 5.00          | NaN                 | NaN           | NaN              | NaN             | 50.00              | NaN            | NaN                    |

**Missing Data Handling**: Checking Null values and replace Null Review Ratings using median. \
**Column Standardization**: Renamed columns to snake case for better readability and implementation. \
**Feature Engineering**:

- Create age_group column by binning customers' age.
- Create purchase_frequency_days column by mapping frequency_of_purchases

**Data Consistency Check**: Verify if discount_applied and promo_code_used are identical -> Remove promo_code_used. \
**Database Integration** : Connect to MS SQL Server and load cleaned dataset into database.

<h2> Data Analysis using SQL </h2>

1. **Revenue by Gender** - Compare total revenue generated by male vs. female customers.
   |gender|total_revenue|
   |------|-------------|
   |Female|75191 |
   |Male |157890 |

2. **High-Spending Discount Users** - Indentify customers who used a discount but still spent more than the average purchase amount.
   |customer_id|purchase_amount|
   |-----------|---------------|
   |2 |64 |
   |3 |73 |
   |4 |90 |
   |7 |85 |
   |9 |97 |
   |... |... |

3. **Top 5 Products by Rating** - List products with the highest average review rating.
   |item_purchased|avg_review_rating|
   |--------------|-----------------|
   |Gloves |3.86 |
   |Sandals |3.84 |
   |Boots |3.82 |
   |Hat |3.8 |
   |Handbag |3.78 |

4. **Shipping Type Comparison** - Compare the average Purchase Amounts between Standard and Express Shipping.
   |shipping_type|avg_purchase_amount|
   |-------------|-------------------|
   |Express |60 |
   |Standard |58 |

5. **Subscribers vs. Non-subscribers** - Compare average spend and total revenue between subscribers and non-subscribers.
   |subscription_status|avg_spend|total_revenue|
   |-------------------|---------|-------------|
   |No |59 |170436 |
   |Yes |59 |62645 |

6. **Discount-Dependant Products** List products with the highest percentage of purchases with discounts applied.
   |item_purchased|discount_usage_rate|
   |--------------|-------------------|
   |Hat |50.00 |
   |Sneakers |49.66 |
   |Coat |49.07 |
   |Sweater |48.17 |
   |Pants |47.37 |

7. **Customer Segmentation** - Segment customers into New, Returning, and Loyal based on purchase history.
   |customer_segment|number_of_customers|
   |----------------|-------------------|
   |Returning |701 |
   |Loyal |3116 |
   |New |83 |

8. **Top 3 Products by Category** - List most purchased products within each category.
   |category|item_purchased|times_purchased|
   |--------|--------------|---------------|
   |Accessories|Jewelry |171 |
   |Accessories|Belt |161 |
   |Accessories|Sunglasses |161 |
   |Accessories|Scarf |157 |
   |Clothing|Blouse |171 |
   |Clothing|Pants |171 |
   |Clothing|Shirt |169 |
   |Clothing|Dress |166 |
   |Footwear|Sandals |160 |
   |Footwear|Shoes |150 |
   |Footwear|Sneakers |145 |
   |Outerwear|Jacket |163 |
   |Outerwear|Coat |161 |

9. **Repeated Buyers and Subscription** - Check customers who are repeat buyers (more than 5 previous purchases) also likely to subscribe
   |subscription_status|total_customers|
   |-------------------|---------------|
   |No |2583 |
   |Yes |980 |

10. **Revenue by Age Group** - Calculate total revenue of each age group
    |age_group|total_revenue|
    |---------|-------------|
    |Middle-aged|89445 |
    |Adult |65842 |
    |Senior |43164 |
    |Young Adult|34630 |

<h2> Dashboard using Power BI </h2>

![Dashboard](https://github.com/ThuCoo/DAProject_CustomerBehavior/blob/065623b87b36af5a466a74a0570c9bdd4afe9f7d/dashboard.png)

<h2> Business Recommendations </h2>

- **Boost Subscription** - Promote exclusive benefits for customers.
- **Customer Loyalty Program** - Rewards repeating buyers to move them to "Loyal" segment.
- **Review Discount Policy** - Balance sale boosts with margin control.
- **Product Positioning** - Highlight top-rated and best-selling products in campaigns.
- **Targeted Marketing** - Focus effort on high-revenue age groups (Middle-aged and Adult) and express-shipping users.
