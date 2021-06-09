# Designing a URL Shortening service like TinyURL

## 1. Why and the Purpose - why is this service useful or necessary?

In essence, shorter URL links are more sharable and easy on the eyes compared to long URLs with a lot of random letters and numbers put together. It can also reduce errors and time when someone types in a short URL.

## 2. Requirements and Goals of the System

_It's important to begin with defining the requirements at the beginning of the interview and try to understand the scope of the requirements that the interviewer has in mind_

- Functional Requirements

1. Given a URL, the user will be receive a shortened version of the URL.
2. The shortened URL will redirect to the original URL.
3. Users have the option to customize the short link.
4. There's an expiration that the user can dictate.

- Non-functional requirements

1. A highly available system. If the service is down, all URL redirections would be down.
2. Minimal latency.
3. The shortened link should be predictable.
4. Contain analytics - how many times the redirection happened.

## 3. Capacity Estimation and Constraints

- This service is going to be read heavy, so we can assume a ratio that says for every one write, there are 100 reads (100:1 ratio).
- We can start with assuming 500 million URL shortenings a month.

### 3.1 Traffic Estimates

1. How many redirections would occur each month?

```
500 million shortenings x 100 reads = 50 billion redirections per month
```

2. How many URL shortenings per second?

```
  500 million / (30 days * 24 hours * 60 mins * 60 sec) = ~200 URLs/second
```

3. How many URL redirections per second, given 100:1 ratio?

```
200 URLs/s * 100 = 20,000 redirections per second
```

### 3.2 Storage Estimates

- Each URL has to be stored in the database.
- Let's assume that each object of the URL stored takes up 500 bytes.
- Let's also assume that we'll hold each object for a total of 5 years.

1. How many objects total would be stored in 5 years?

```
500 million requests/month * 12 months * 5 years = 30 billion objects stored
```

2. How much total storage do we need?

```
30 billion * 500 bytes = 15 TB
```
