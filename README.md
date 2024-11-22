# Product Recommendation API

## How to run this project

To start the project, execute the following command:

```
docker compose up -d --build
```

To stop the project, use:

```
docker compose down
```

## Routes

- Access the Swagger documentation for available endpoints at: http://localhost:8000/docs
- The primary endpoint available is: `http://localhost:8000/api/v1/recommendations`
  - This endpoint returns the top 5 recommended products based on the weights defined in the `.env` file

## Solution

After analyzing the data, I developed the following formula:

$$ {1 \over price} \times totalSales $$

To allow customization, I incorporated configurable weights. After normalizing the features, the scoring formula becomes:

$$ score = weightSales \times normalizedSales + weightPrice \times inverseNormalizedPrice$$

The calculation occurs only on the first request. Subsequent requests retrieve results from the cache (powered by Redis), ensuring faster response times.
