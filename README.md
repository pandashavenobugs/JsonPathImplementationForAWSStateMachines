# JsonPath Implementation for AWS StateMachines

Using state machines mostly is a good way to make the decision process readable for the people. However, sometimes it could be hard to deal with a little more complex situations. In this blog post, we will discuss the problem we faced and how we solved it.

## The Problem

We had data like below,

```json
{
  "personID": "123124",
  "name": "berat",
  "surName": "Dinckan",
  "products": [
    {
      "category": "realty",
      "productType": "house",
      "price": 50000,
      "country": "Turkiye"
    },
    {
      "category": "vahicle",
      "productType": "car",
      "price": 10000,
      "country": "Turkiye",
      "color": "RED",
      "age": 15
    },
    {
      "category": "technology",
      "productType": "laptop",
      "price": 1000
    }
  ]
}
```

At this point, all products are unique so every different category has one data. We need a product whose "category" is the "vehicle". We tried the lambda function and the map to solve this problem. For this case,unfortunately the map didn't work as we expected. The map executed all iterations even an item didn't match the what expected. So we added succes and fail probs end of the map but this state machine was too complicated and hard to grasp. After the map, we put a lambda function to filter the data and we said If we are using lambda functions to filter the data what is the matter of using state machines. It was still complicated and if an error has existed the developers would have to take a look at the lambda function to see what was going on. There must be another way.
