## Programming Model

To really understand a syntax, you have to also understand the semantics of the underlying programming model, so that's where we will start. This discussion will be very high-level, so don't worry about the details for now. First, remember that Eve is not just a language; it is also a database. These are not separate components that interact; they are actually one and the same. However, sometimes we use "Eve DB" to refer to the underlying facts in the database.

At its core, Eve only responds to two commands:

1. What facts do you know about this "record"?
2. Remember a new fact about this "record".

Communication with Eve happens through "records", which are key-value pairs attached to a unique ID. To access facts in the Eve DB, you use a record. To insert/remove facts into/from the Eve DB, you also use a record.

Computation occurs as a result of relationships between records. For example, I might model myself as a record with an `age` and a `birth year`. There might also be a record representing the `current year`. Then I could compute my `age` as my `birth year` subtracted from the `current year`.

A key concept here is that age is a derived fact, supported by two other facts: `birth year` and `current year`. If either of those supporting facts are removed from the Eve DB, then `age` can no longer exist as well. For intuition, think about modeling this calculation in a spreadsheet using three cells, and what would happen to the `age` cell if you deleted one of the other two cells.

Thus the presence or absence of facts can be used to control the flow of a program. To see how this works, consider how a navigation button on a webpage might work. When the button is clicked, a fact is inserted into the Eve DB noting the element that was clicked. This click fact would support a record that defines the page to be rendered. This in turn would support the page renderer, whose job it is to display the page.

One last thing to note about control flow is that we have no concept of a loop in Eve. Recursion is one way to recover looping, but set semantics and aggregates often obviate the need for recursion. In Eve, every value is actually a set. With operators defined over sets (think `map()`) and aggregation (think `reduce()`) we can actually do away with most cases where we would be tempted to use a loop.

#### Set Semantics

One other thing to know about Eve is that records follow [set semantics](https://en.wikipedia.org/wiki/Set_(mathematics)). Sets are collections where every element of the collection is unique. This is in contrast to bag semantics, where elements can be duplicated. We'll see the implications of this later, but it's important to keep in mind.