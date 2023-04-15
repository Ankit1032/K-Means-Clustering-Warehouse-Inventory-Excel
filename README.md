# K-Means-Clustering-Warehouse-Inventory-Excel
K-Means-Clustering-Warehouse-Inventory-Excel

---- Storage Space Optimization in Warehouse

Q) Why we need Storage Space optimized?
Ans>
	We need High Frequency Items stored close to Dispatch area, Si that it will be easier to dispatch as their demand are of High frequency.
	
Managers try to optimize storage of products of different attributes:
1. Order Frequency
2. Cycle Inventory
3. Value
4. Dimensions

These optimizations are needed so that we incur less costs and High serviceability.

PROJECT CASE : Clustering of Product Families of an E-Commerce Warehouse
-> 35,000+ SKUs ---> 73 Product Families 

Now the challenge is to cluter these product families into 5 clusters based on Order Frequency & Product Weight.

Algorithm Used : K-Means Clustering

Data Contains :
1. Product Family
2. Sum of count of orders
3. Avg product weight in Kg

Step 1 : We need to normalize the data
	Here, If you plot a Scatter Plot over columns "Sum of count of orders" and "Avg product weight in Kg", You will see that:
	>The column "Avg product weight in Kg" values ranges from 0 - 14 but the values of column "Sum of count of orders" ranges from 0 to 12,000, which is the huge range compared to "Avg product weight in Kg" column. If we don't normalize the data, The clustering will happen based on the values of only "Sum of count of orders".
	
	To normalize a high range column value between 0 to 1, you can use the following formula in Excel:
	= (x - min) / (max - min)
	Where x is the value you want to normalize, min is the minimum value in the column, and max is the maximum value in the column.
	
	Why does this normalization formula work?
	This formula works because it scales the range of the original data to be between 0 and 1. By subtracting the minimum value from each value in the column, the minimum value becomes 0. By dividing the result by the range (i.e., the difference between the maximum and minimum values), the maximum value becomes 1.
	
	For example a column contains values ranging from min:10 to max:100
	
	-if the current value is 10(which is min) = 10 - 10 / 100 - 10 = 0 (So the min value becomes 0 after being normalized)
	-if the current value is 100(which is max) = 100 - 10 / 100 - 10 = 1 (So the max value becomes 1 after being normalized)
	-Now any value is between will always be between 0 and 1 after being normalized
	
	Normalize the data "Sum of count of orders" and "Avg product weight in Kg" using the formula and name the normalized columns as "Count variable" and "Weight variable"
	
	
Step 2 : Make a column "No. Of Cluster" and assign value 5 as you want 5 clusters

Step 3: Make a column "Cluster" in L column and assign random values from 1 to 5 using formula RANDBETWEEN to the product family

Step 4: Make a seperate table "Cluster" , "Count Average" and "Weight Average"
	- In Cluster : Assign 1 to 5 values
	- In Count Average : Take the average values of "Count Variable" column of that particular cluster assigned using AVERGAEIF formula
	- In Weight Avergae : Similar to what u did above, Take the average values of "Weight Variable" column of that particular cluster assigned using AVERGAEIF formula
	
Step 5 : Make a small table "Cluster(Product Fam)" , "Count Variable" and "Weight Variable"
		then, put any name in "Cluster(Product Fam)" and use VLOOKUP to populate the "Count Variable" and "Weight Variable" of that Product
		
Step 6 : Now we need to find the distance from each cluster
		>Calculate the distance between each observation in the table created just above and each centroid(marked in red table)

Step 7 : Assign each observation to the cluster with the closest centroid using MIN formula in excel
	
Step 8 : Now we will have the find the best cluster(min distance) for each product family.
	> We will have to write a MACRO to
		a. paste each product family name in cell(O4)
		b. and then take the "best cluster" in cell(O9) and paste it in "Cluster" column beside each product family
	>MACRO:
		a. Open Developer tab -> Visual basic -> Insert -> Module
		b. Paste the below MACRO
			Sub clustergroups()

			For Each cell In Range("L2:L74")

			Range("O4").Value = Cells(cell.Row, 1).Value

			cell.Value = Range("O9").Value

			Next cell

			End Sub
			
		Note : Remeber to save the workbook as Macro-Enabled Workbook (.xlsm)
		
Step 9: Create a Scatter plot using 3 variables (Count variable, Weight Variable and Cluster) 
	> Its very hard to do in excel(Easy in Power BI) so use the below youtube vid
	https://www.youtube.com/watch?v=1XwYrg5Wf_g

	
	
