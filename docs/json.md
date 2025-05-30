# Understanding JSON



### Navigate to [JSON Path Finder](https://jsonpathfinder.com/){:target="_blank"}
   
### Exercise 1

1. Copy this text into the left pane of the JSON PathFinder
   >  <textarea cols="50" disabled style= "background-color: #ffffff">{"name":"John", "age":30, "car":null} </textarea>
2. Click Beautify
3. Click age
   > What is the JSON path for age? 
   >
4. Delete the contents of the left pane and copy this text into the left pane of the JSON PathFinder
   >
   >   <textarea cols="50" disabled style= "background-color: #ffffff">{"name":"John","age":30,"cars":["Ford","BMW","Fiat"]}</textarea>
5. Click Beautify
   > Click on cars and observe that there is an array.
   >
   > What is the JSON path for BMW?

### Exercise 2

1. Delete the contents of the left pane and copy this text into the left pane of the JSON PathFinder
   >  <textarea cols="70" rows = "8" disabled style= "background-color: #ffffff">{"name":"John Smith","sku":"20223","price":23.95,"shipTo":{"name":"Jane Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"},"billTo":{"name":"John Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"}}</textarea>
   >

2. Click Beautify
   > !!! Note 
      "shipTo" and "billTo" have additional JSON objects in them.
   >
   > What is the JSON path for the ship to state?
   >
3. Delete the contents of the left pane and copy this text into the left pane of the JSON PathFinder
   > <textarea cols="70" rows = "10" disabled style= "background-color: #ffffff">[{"name":"John Smith","sku":"20223","price":23.95,"shipTo":{"name":"Jane Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"},"billTo":{"name":"John Smith","address":"123 Maple Street","city":"Pretendville","state":"NY","zip":"12345"}},{"name":"Alice Brown","sku":"54321","price":199.95,"shipTo":{"name":"Bob Brown","address":"456 Oak Lane","city":"Pretendville","state":"HI","zip":"98999"},"billTo":{"name":"Alice Brown","address":"456 Oak Lane","city":"Pretendville","state":"HI","zip":"98999"}}]</textarea>
   >

4. Click Beautify
   > !!! Note 
      We now have an array of objects (0 and 1)
   >
   > What is the JSON path for Alice Brown's ship to state?

### Navigate to [JSON Path](https://jsonpath.com/){:target="_blank"}

### Exercise 3

1. Copy the raw text from this [Desktop Layout](./assets/Default%20Desktop%20Layout.json){:target="_blank"} into the Document (left pane) of the JSON Path
2. In the top bar, type <copy>$</copy>
      1. What are the results?
3. In the top bar, type <copy>$.agent</copy>
      1. What are the results?
      2. Toggle Output Paths to on.
      3. You should see another way to access the path.
      4. Toggle Output Paths to off.
4. In the top bar, type <copy>$["agent"]</copy>
      1. What is the difference?
5. In the top bar, type <copy>$.agent.area.advancedHeader</copy>
      1. what if you wanted to return a list of the "comp" values?
6. In the top bar, type <copy>$.agent.area.advancedHeader..comp</copy>
      1. This returns an array of anything that matches "comp" inside the $.agent.area.advancedHeader path
      2. In the top bar, type <copy>$.agent.area..comp</copy>
        1. How many items are returned in the array?
      3. Toggle Output Paths to on.
        1.  Note how "greedy" the query is.
    1.  When would you want to use a double dot in a JSON path?
    2.  Why would you not want to use a double dot in a JSON path?
    
---
