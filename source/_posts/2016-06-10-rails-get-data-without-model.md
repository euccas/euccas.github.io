---
layout: post
title: "Rails: Get data from PostgreSQL database without the Model"
date: 2016-06-10 18:32:01 -0700
comments: true
categories: Ruby PostgreSQL
---

In Ruby on Rails, Active Record is the M in MVC - the model. Model is the layer of the system which represents business data and logic. Active Record facilitates the creation and the use of business objects whose data requires persistent storage to a database. In some cases, however, you may want to use databases in Rails applications without the Model. What you can do is using the ```pg``` gem to directly manipulate the data you need.

# Create a database connection

If the database is not declared in Rails app's ```config/database.yml``` file, you won't be able to use the ```establish_connection``` method in ActiveRecord. But you can still use the ```pg``` gem to directly connect to the database.

<!--more--> 

```ruby
# page_controller.rb

conn = PGconn.connect('<server>', <port>, "", "", '<database>', "<user>", "<password>")
render :plain => "Oops, database currently not accessible" unless conn

```

# Query data with RAW SQL

```ruby
# page_controller.rb

@page_records = []
result = conn.exec('SELECT * FROM <table> ORDER BY id DESC')

@page_records = result

```

The result is an array of Hash. For example:

```ruby
[
  { "title" => "my page 1", "author" => "Tom", "created_at" => "2016-06-08" }
  { "title" => "my page 2", "author" => "Nancy", "created_at" => "2016-06-09" }
]
```

# Use the data in View

When using the queried data in Rails View, need to note you need use ```record['title']``` instead of ```record.title```, which is different from using the data generated from a Rails Model.

```ruby
# page.erb

<div>
    <% @page_records.each do |record| %>
        <p> <%= record['title'] %> </p>
        <p> <%= record['author'] %> </p>
    <% end %>
</div>
```

# As a note in the end

Although the above approach works in Rails, I'd say a more decent way to handle the need of getting data from multiple databases, is creating a crafted Model. The process will need:

- Add the configurations of all your external databases in Rails app
- Create a Model file

```ruby
class Pages < ActiveRecord::Base

end
```

- Use ```establish_connection``` in the Model
- When your table name doesn't match Rails convention, set the table name with ```self.table_name = '<your table name>'```
- Create methods in the Model to fetch the data you need

