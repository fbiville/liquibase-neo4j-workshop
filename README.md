# Liquibase Neo4j workshop

## Exercises

### Exercise 1

#### Step 1

Create a node key constraint on nodes with the Movie label and the imdbId property.

#### Step 2

Before creating an existence constraint on movie plots, let's make sure all nodes have a defined plot property.
For that, create a new change set with a Cypher query that sets the plot property to the movie title, for movies without
plots.
Then, create another change set that creates the existence constraint on nodes with the Movie label and the plot
property.

### Exercise 2

Load data from `countries.csv`.
Use the `tableName` attribute as the label name, it must be `Country`.
The CSV header column is named `name`, make sure the column name is called `country` instead.

### Exercise 3

#### Step 1

Extract country nodes with label `Country` and property `names`, from `Movie` nodes that have a defined `countries`
property.
There should be a relationship created with type `IN_COUNTRY` going from `Movie` to `Country`.

Hint: there is a refactoring for this!

#### Step 2

The second half of this step is provided. It links the `Country` nodes with a `name` property to their `Movie` nodes.

Your job here is to create these new `Country` nodes with a single, distinct and trimmed country code from the `Country`
nodes that were extracted in step 1.

### Exercise 4

Time to rollback!

#### Step 1

Let's start with the easiest bit: the rollback for exercise 3/step 1.
The goal is to provide the reverse operation of the property extraction.
In other words, set the `names` property of the `Country` nodes back the `Movie` where they belong. Remember the `Movie`
property is named `countries` though!
A short Cypher query should do the trick here.

### Step 2

Let's reverse exercise 3/step 2 now.
It's probably easier to split the work into two Cypher queries:

1. recreate `Country` nodes with `names` collected from all the country names involved in each movie, link them to their
   movie as well
2. remove all `Country` nodes that include the `name` property, as well as their relationship
