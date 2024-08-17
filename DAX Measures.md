# [DAX] Elevating Retail Operations through Data

#### Total Transactions 

         = COUNT(Transaction_Data[quantity])
         
#### Total Revenue
       
         = SUMX(
            Transaction_Data,
            Transaction_Data[quantity] *
            RELATED(
              Products[product_retail_price]))
         
#### Total Cost 

        = SUMX(
            Transaction_Data,
            Transaction_Data[quantity] *
            RELATED(
              Products[product_cost]))

#### Total Profit

         = [Total Revenue] - [Total Cost]

#### Total Returns

         = COUNT(Return_Data[quantity])

#### Last Month Returns

        = CALCULATE(
            [Total Returns],
            DATEADD(
              'Calendar'[date],
              -1,
              MONTH))
     
#### Last Month Transactions

        = CALCULATE(
            [Total Transactions],
            DATEADD(
              'Calendar'[date],
              -1,
              MONTH))

#### Transaction Target

        = [Last Month Transactions] * 1.05

#### Transaction Target Gap

        = [Total Transactions] - [Transaction Target]

#### Last Month Revenue

        = CALCULATE(
            [Total Revenue],
            DATEADD(
              'Calendar'[date],
              -1,
              MONTH))

#### Revenue Target

        = [Last Month Revenue] * 1.05

#### Revenue Target Gap

        = [Total Revenue] - [Revenue Target]

#### Last Month Profit

        = CALCULATE(
            [Total Profit],
            DATEADD(
              'Calendar'[date],
              -1,
              MONTH))

#### Profit Target

        = [Last Month Profit] * 1.05

#### Profit Target Gap

        = [Total Profit] - [Profit Target]

#### Profit Margin

        = DIVIDE(
            [Total Profit],
            [Total Revenue])

#### Quantity Sold 

        = SUM(Transaction_Data[quantity])
        
#### Quantity Returned 

        = SUM(Return_Data[quantity])

#### Return Rate

        = DIVIDE(
            [Quantity Returned],
            [Quantity Sold])

#### Unique Products

        = DISTINCTCOUNT(Products[product_name])

#### Total Customers

        = DISTINCTCOUNT(Transaction_Data[customer_id])

#### All Transactions 

        = CALCULATE(
            [Total Transactions],
            ALL(
              Transaction_Data))
#### All Returns

        = CALCULATE(
            [Total Returns],
            ALL(
              Return_Data))
              
#### Average Revenue Per Customer

        = DIVIDE(
            [Total Revenue],
            [Total Customers])

#### Average Profit Per Customer

        = DIVIDE(
            [Total Profit],
            [Total Customers])

#### Average Orders Per Customer

        = DIVIDE(
            [Total Transactions],
            [Total Customers])

#### Average Retail Price

        = AVERAGE(Products[product_retail_price])

#### Adjusted Revenue

        = SUMX(
            'Sales Data',
            'Sales Data'[OrderQuantity] * 
            [Adjusted Price])
            
#### Adjusted Profit

        = [Adjusted Revenue] - [Total Cost]

#### Adjusted Price

        = [Average Retail Price] * 
          (1 + 'Price Adjustment (%)'[Price Adjustment (%) Value])

#### Quantity Sold 

        = SUM('Sales Data'[OrderQuantity])

#### 60-Day Revenue
        
        = CALCULATE(
            [Total Revenue],
            DATESINPERIOD(
              'Calendar'[date],
              MAX(
                'Calendar'[date]),
                -60,
                DAY))

#### Weekend Transactions
        
        = CALCULATE(
            [Total Transactions],
            'Calendar'[Weekend] = "Y")

#### % Weekend Transactions
        
        = DIVIDE(
            [Weekend Transactions],
            [Total Transactions])

#### YTD Revenue

        = CALCULATE(
            [Total Revenue],
            DATESYTD(
              'Calendar'[date]))
