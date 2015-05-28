#This project is an exercise in using existing frameworks and using ActiveRecord.

##The first part of the project involved establishing models so that we could use ActiveRecord to go overa dataset we had used previously.
##The next part of the project was determing which ActiveRecord queries to use to solve a set of problems.

Once we got out layout working we could run our console.rb file and ask it questions.

The following are questions and how I answered them in Ruby.

####1) How many users are there?

we call the last method on the ID numbers in the user class.
`
 User.last.id
=> 50
`

A user ID is given to each person in the user class. 50 ids for 50 folks.


####2) What are the 5 most expensive items?

By arranging for the order of the items to be decending we get the most expensive first. By limiting it to 5 we just get the top five.


`[43] pry(main)> Item.order('price DESC').limit(5)
=> [#<Item:0x007fae38cd15e8
  id: 25,
  title: "Small Cotton Gloves",
  category: "Automotive, Shoes & Beauty",
  description: "Multi-layered modular service-desk",
  price: 9984>,
 #<Item:0x007fae38cd1430
  id: 83,
  title: "Small Wooden Computer",
  category: "Health",
  description: "Re-engineered fault-tolerant adapter",
  price: 9859>,
 #<Item:0x007fae38cd1160 id: 100, title: "Awesome Granite Pants", category: "Toys & Books", description: "Upgradable 24/7 access", price: 9790>,
 #<Item:0x007fae38cd0f08
  id: 40,
  title: "Sleek Wooden Hat",
  category: "Music & Baby",
  description: "Quality-focused heuristic info-mediaries",
  price: 9390>,
 #<Item:0x007fae38cd0cd8
  id: 60,
  title: "Ergonomic Steel Car",
  category: "Books & Outdoors",
  description: "Enterprise-wide secondary firmware",
  price: 9341>]`

We get a collection of five somewhat peculiar items. These seem to have been created by a some kind of random-useless-shit generator. But then again I have been waiting my entire life for a wooden hat.

####3) What’s the cheapest book?

lets use the where method to make sure we only get books and then arrange them with their prices ascending. lastly we will just get the first to make sure we arent wasting time.

`Item.where(category: 'Books').order("price ASC").first
=> #<Item:0x007fae38e33698 id: 76, title: "Ergonomic Granite Chair", category: "Books", description: "De-engineered bi-directional portal", price: 1496>`

And orgonomic granite chair! Also, its a book! Also its 1476 which I take to me $14.76. Thats a killer deal. Gimme a dozen!

####4) Who lives at “6439 Zetta Hills, Willmouth, WY”? Do they have another address?

We will use the find_by method to locate the user id by searching for the street.

`Address.find_by street: '6439 Zetta Hills'` gives us a user_id of 40. If we enter

`User.find_by id: 40`

This returns

`<User:0x007f9cc205a710 id: 40, first_name: "Corrine", last_name: "Little", email: "rubie_kovacek@grimes.net">
[6] pry(main)> `

We now know miss Corrine Littles email, full name, and address! Lets hope software engineers are employing property safety protocals and not just leaving this stuff out in public. With a little legwork anyone could find out she our dear Corrine has an Awesome Concrete Chair.


####5) Correct Virginie Mitchell’s address to “New York, NY, 10108”.

First lets use the find_by method to look through our list of users for this totally not made up name.

`
User.find_by first_name: 'Virginie'
`

this returns

`#<User:0x007f9cc15af220 id: 39, first_name: "Virginie", last_name: "Mitchell", email: "daisy.crist@altenwerthmonahan.biz">
[9] pry(main)>
`

Now we know her user id number. With that info we can change the specifics of her address.

`[36] pry(main)> address = Address.find_by(id: 39)
=> #<Address:0x007fae38e33080 id: 39, user_id: 37, street: "7503 Cale Grove", city: "Robertoshire", state: "PA", zip: 49744>
[38] pry(main)> address.state = 'NY'
=> "NY"
[39] pry(main)> address.city = 'New York'
=> "New York"
[40] pry(main)> address.zip = 10108
=> 10108
[41] pry(main)> address.save
=> true
[42] pry(main)> Address.find_by(id: 39)
=> #<Address:0x007fae38d91f00 id: 39, user_id: 37, street: "7503 Cale Grove", city: "New York", state: "NY", zip: 10108>
[43] pry(main)>`

This is not the prettiest way to change amounts but it makes what we are doing the easiest to read.

####6) How much would it cost to buy one of each tool?

If we call where on the item class for the category like so:

`[23] pry(main)> Item.where(category: 'Tools')`

we get a list of the items that are tools. Tremendous! a practical rubbert shirt and incredible plastic gloves.

`=> [#<Item:0x007fae39137268
  id: 32,
  title: "Practical Rubber Shirt",
  category: "Tools",
  description: "De-engineered multimedia info-mediaries",
  price: 1107>,
 #<Item:0x007fae39137100
  id: 80,
  title: "Incredible Plastic Gloves",
  category: "Tools",
  description: "Operative mission-critical emulation",
  price: 5437>,`

  This however only gives us the two results and not the sum of them.
  If we wish to add the results together we can use the sum method.

####7) How many total items did we sell?

`pry(main)> Order.last.id
=> 377`

This is the easiest way I know how to do things.

####8) How much was spent on books?

`
I don't even know how to start on this.
`
####9) Simulate buying an item by inserting a User for yourself and an Order for that User.

