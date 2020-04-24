# Getting Your JSON needs met with PostgreSQL

You are dealing with JSON in your application and you decide you want to store it in your database. You let out a heavy sigh and  think "Oh well I guess I am going to have to add something besides my favorite DB (PostgreSQL) to my architecture. I wish I could just keep using PostgreSQL". Well my friend, today is the day your wishes come true. In the blog post we will talk a little about how you can use PostgreSQL for all your JSON needs. We will also point you at some free learning resources so you can dig in more.  

## JSON versus JSONB

Since 9.2, released in September 2012, PostgreSQL has had a JSON type. This original JSON type though was not much more than just a simple storage field that let you dump JSON into your database table. It is just a simple text field that checks to make sure your JSON is well formed. Other than that it doesn't do much for you and I would not recommend using it.

With PostgreSQL release 9.4 in December 2014, a JSOB type was added. Though I joke that the B stands for better it really stands for Binary. When you put JSON data into a JSONB column, in addition to checking for well formed JSON, you now have the ability to indexing and query and retrieve portions of the document. Generally for all your work you should use JSONB unless you have a compelling reason not to. Here are a couple of nice discussions on the [tradeoffs](https://heap.io/blog/engineering/when-to-avoid-jsonb-in-a-postgresql-schema) and [choosing](https://www.citusdata.com/blog/2016/07/14/choosing-nosql-hstore-json-jsonb/) JSON versus JSONB

## What can you do with JSONB in PostgreSQL 

Say you had some JSON like:

```
{
    "person":
        {
            "first_name": "Steve",
            "last_name": "Pousty"
        },
    "score" : 100,
    "status" : "Awesome"
}
```

Once you put it in a JSOB column names *json_content* (and make a GIN Index for faster queries) you can do all sort of fun things. Please note that I will be using the JSONB navigation and function syntax found in PostgreSQL version 11. There was a major improvement to JSON document navigation and querying in version 12 which will be the focus of another blog post.

### In the select part of the query

Let's get the users last name

```
select json_content ##> {person, last_name} from mytable;
```

The #> or #> is the JSON path navigator with the difference being #> returns JSON and the ##> returns the JSON text value.

### In the Where clause

Using that same document navigation syntax we can then combine that with the containment check. Just like the name sounds, we check to see if the stored JSON contains the JSON we are looking for. For example, if we wanted to return only those records that had a status of awesome we would write:

```
select json_contet from mytable where json_content @> '{"status": "Awesome"}':jsonb;
```

This `@> ` operator looks for JSON that contains the JSON on the right side of the operator. 

## The Beauty of All This

The best part of working with JSON in PostgreSQL is you get to leverage all the normal SQL you already love along with these JSON functions. SQL processing can be used to greatly reduce the amount of code you need in your application. For example here is the query to get all the distinct status types in the table:

```
select distinct(json_content ##> {status} as status, count(json_content) from mytable group by json_content ##> {status};
```

## Where to learn more

So if you are intrigued by what you saw here and want to learn more here are some great resources (if I do say so myself)

We have an online tutorial to get your started with JSON in PostgreSQL. It is free and available 24/7

and then I also did a live stream where I walked people through the material above.

Let us know what you think of the material! I would also love to hear about how YOU are using JSON with PostgreSQL.

Thanks and happy coding.