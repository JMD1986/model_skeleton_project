This project is an exercise in using existing frameworks and using ActiveRecord.

The first part of the project involved establishing models so thatwe could use ActiveRecord to go over a dataset we had used previously. The next part of the project was determing which ActiveRecord queries to use to solve a set of problems.

Once we got out layout working we could run our console file and ask it questions.

The following are questions and how I answered them in Ruby.

How many users are there?

 User.last.id
=> 50

What are the 5 most expensive items?

'[43] pry(main)> Item.order('price DESC').limit(5)
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
  price: 9341>]'

What’s the cheapest book?

'Item.where(category: 'Books').order("price ASC").first
=> #<Item:0x007fae38e33698 id: 76, title: "Ergonomic Granite Chair", category: "Books", description: "De-engineered bi-directional portal", price: 1496>'

Who lives at “6439 Zetta Hills, Willmouth, WY”? Do they have another address?

`Address.find_by street: '6439 Zetta Hills'` give's us a user_id of 40
If she has another address I can't figure out how to get it :-/

edit: at some point my user id's changed :-/

Correct Virginie Mitchell’s address to “New York, NY, 10108”.

First I found her ID then I changed her Address the following way

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
[43] pry(main)>
`

How much would it cost to buy one of each tool?

`[23] pry(main)> Item.where(category: 'Tools')
=> [#<Item:0x007fae39137268
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

How many total items did we sell?

`pry(main)> Order.last.id
=> 377`

How much was spent on books?
`
I don't even know how to start on this.
`
Simulate buying an item by inserting a User for yourself and an Order for that User.

```
.
├── Gemfile             # Details which gems are required by the project
├── README.md           # This file
├── Rakefile            # Defines `rake generate:migration` and `db:migrate`
├── config
│   └── database.yml    # Defines the database config (e.g. name of file)
├── console.rb          # `ruby console.rb` starts `pry` with models loaded
├── db
│   ├── dev.sqlite3     # Default location of the database file
│   ├── migrate         # Folder containing generated migrations
│   └── setup.rb        # `require`ing this file sets up the db connection
└── lib                 # Your ruby code (models, etc.) should go here
    └── all.rb          # Require this file to auto-require _all_ `.rb` files in `lib`
```

