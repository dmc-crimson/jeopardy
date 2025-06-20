# jeopardy
# Jeopardy Project

[jeopardy_starter_code.zip](https://prod-files-secure.s3.us-west-2.amazonaws.com/163f1722-85e9-4a3c-adba-457a91094f00/fff684c2-ab51-4c9e-8921-a5af961043f8/jeopardy_(2).zip)

## Welcome to Jeopardy!

Hey there! This is the time for your final project. Finally we go over the concepts
and the skills you have learned so far and apply them. We will build Jeopardy or
specifically your own version of the game which runs in the browser. We will be using
an external API to retrieve the data and then manipulating the DOM to build an
interactive game board.

### The API

In order to fetch the correct data you will be using an external API. The "endpoint"
is https://rithm-jeopardy.herokuapp.com/api. Now... if you just go ahead and click on
it as is, the response will be 404 Not Found. Why? Well because we send in the request
to retrieve the data in a specific format which the API expects. Let's give it a
SPECIFIC request so that we can get a SPECIFIC response.

### Retrieving Category Data

First we will need to retrieve Category data for our questions. The format for the URL
is the following:

GET "[https://rithm-jeopardy.herokuapp.com/api/categories?count=[**integer**]](https://rithm-jeopardy.herokuapp.com/api/categories?count=%5B**integer**%5D)"

What does this mean? Well let's review the structure of the URL. The API is telling us
that we can plug in a number in the count=[integer] part of the URL and the API will
fetch us the data which we need.
What is the HTTP Request that we need to make? Fetching data? Seems like a GET request
is the appropriate one.

```jsx
let res = await axios.get(`https://rithm-jeopardy.herokuapp.com/api/categories?
count=100`)
// NOTICE WE HAVE PROVIDED THE VALUE 100 FOR THE <count> query
// what is in our res variable?
// checking out res.data will produce the following result //
[
{
"id": 2,
"title": "baseball",
"clues_count": 5
},
{
"id": 3,
"title": "odd jobs",
"clues_count": 5
},
{
"id": 4,
"title": "movies",
"clues_count": 5
},
{
"id": 6,

"title": "\"cat\" egory",
"clues_count": 5
},
// and so on until 100 objects in an array
]
```

### Retrieving Questions in a Specific Category

Now that you know how to retrieve all available categories, let's explore how you can
retrieve the questions from this API.
The format for the URL is the following:

GET "[https://rithm-jeopardy.herokuapp.com/api/category?id=[**integer**]](https://rithm-jeopardy.herokuapp.com/api/category?id=%5B**integer**%5D)"

Just like in the previous example the API is telling us that if we plug in a number in
the id=integer part of the URL we will receive an appropriate response.
For example:

```jsx
let res = await axios.get(`https://rithm-jeopardy.herokuapp.com/api/category?
id=2`)
// NOTICE: Our URL is different and we have the value 2 for id= part of the URL
// what is in our res variable?
// checking out res.data will produce the following result //
{
"id": 2,
"title": "baseball",
"clues": [
{
"id": 2,
"answer": "the Western division",
"question": "The Atlanta Braves are in this division of the National
League",
"value": 100,
"airdate": "1985-02-08T12:00:00.000Z",
"created_at": "2014-02-11T22:47:18.829Z",
"updated_at": "2014-02-11T22:47:18.829Z",
"category_id": 2,
"game_id": null,
"invalid_count": null,
"category": {
"id": 2,
"title": "baseball",
"created_at": "2014-02-11T22:47:18.706Z",
"updated_at": "2014-02-11T22:47:18.706Z",
"clues_count": 45
}
},
{
"id": 1183,
"answer": "no-hitters",
"question": "Johnny Vander Meer is the only man to have ever pitched 2 of

them consecutively",
"value": 200,
"airdate": "1984-10-04T19:00:00.000Z",
"created_at": "2014-02-11T22:47:18.829Z",
"updated_at": "2014-02-11T22:47:18.829Z",
"category_id": 2,
"game_id": null,
"invalid_count": null,
"category": {
"id": 2,
"title": "baseball",
"created_at": "2014-02-11T22:47:18.706Z",
"updated_at": "2014-02-11T22:47:18.706Z",
"clues_count": 45
}
},
// and so on... there will be MANY clues in this array
]
};
```

### Working Further with the API

Before you begin the project, explore the API. What happens when you limit the
responses in the first URL? (i.e 'count=5') or if you try to GET a Category which does
NOT exist (i.e "id=0").
