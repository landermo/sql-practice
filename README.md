# sql-practice

1. How many users are there?

    50
    
    'select count(*) from users'
    

2. What are the 5 most expensive items?

    "Small Cotton Gloves"
    "Small Wooden Computer"
    "Awesome Granite Pants"
    "Sleek Wooden Hat"
    "Ergonomic Steel Car"

    'select title from items order by price desc limit 5'
    
    
3. What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
    
    Ergonomic Granite Chair
    
    'select * from items where category = 'Books' order by price asc limit 1'
    
    No you still get the same book. The query changes. 
    
    'select * from items where category like '%Books%' order by price asc limit 1'


4. Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?

    Corrine Little

    'select users.first_name, users.last_name, addresses.street, addresses.city, addresses.state, addresses.zip from users
    inner join addresses on addresses.user_id = users.id where addresses.street = '6439 Zetta Hills''
    
    yes - other address: 
    
    "54369 Wolff Forges" "Lake Bryon" "CA" "31587"
    
    'select * from addresses where user_id = 40'

5. Correct Virginie Mitchell's address to "New York, NY, 10108".

    There were 2, I chose the one for NY.
    
    'select users.first_name, users.last_name, addresses.user_id, addresses.street from users
     inner join addresses on users.id = addresses.user_id where users.first_name = 'Virginie'
     and users.last_name = 'Mitchell''
    
    'update addresses set city = 'New York', zip = 10108 where id = 41'


6. How much would it cost to buy one of each tool?
    
    29255.0
    
    'select total(price) from items where category like '%tools''


7. How many total items did we sell?

    2125
    
    'select sum(quantity) from orders'

8. How much was spent on books?

    1081352
     
     'select sum(orders.quantity * items.price) as totals from orders 
     inner join items on items.id = orders.item_id 
     where category like '%Books%''

9. Simulate buying an item by inserting a User for yourself and an Order for that User.

    'insert into users (first_name, last_name, email) values ('Laura', 'Montgomery', 'laura@bbb.com')'
    
    'insert into orders (user_id, item_id, quantity, created_at) values (51, 58, 1,datetime('now'))'
    
10.  What item was ordered most often? Grossed the most money?

      These 3 tied for ordered the most often:
      
       "10", "46", "65"
       
     
       select * from orders GROUP BY item_id
       HAVING COUNT(*) >= 9
       
11. What user spent the most?
12. What were the top 3 highest grossing categories?