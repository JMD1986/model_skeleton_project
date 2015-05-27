This project is an exercise in using existing frameworks and using ActiveRecord.

The first part of the project involved establishing models so thatwe could use ActiveRecord to go over a dataset we had used previously. The next part of the project was determing which ActiveRecord queries to use to solve a set of problems.

Once we got out layout working we could run our console file and ask it questions.

The following are questions and how I answered them in Ruby.

How many users are there?

 User.last.id
=> 50

What are the 5 most expensive items?

Item.order('price DESC').limit(5)

What’s the cheapest book?

'Item.where(category: 'Books').order("price ASC").first
=> #<Item:0x007fae38e33698 id: 76, title: "Ergonomic Granite Chair", category: "Books", description: "De-engineered bi-directional portal", price: 1496>'

Who lives at “6439 Zetta Hills, Willmouth, WY”? Do they have another address?

`Address.find_by street: '6439 Zetta Hills'` give's us a user_id or 40
If she has another address I can't figure out how to get it :-/

Correct Virginie Mitchell’s address to “New York, NY, 10108”.

How much would it cost to buy one of each tool?



How many total items did we sell?

pry(main)> Order.last.id
=> 377

How much was spent on books?

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

