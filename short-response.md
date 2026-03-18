# Short Response Questions

Answer each of these questions completely but concisely. Use the proper technical terminology. You may refer to the [Marcy Lab School Docs](https://marcylabschool.gitbook.io/marcy-lab-school-docs) or Google but do NOT copy and paste definitions or explanations verbatim.

You can earn up to 6 points for each response (3 points for writing quality, 3 points for technical content).

Before submitting your responses, use a spell checker / AI to ensure that you have no grammar or spelling mistakes.

## Question 1: Servers and HTTP

What is a server? Describe the HTTP request-response cycle including the key components of a request (method, endpoint, headers, body) and a response (status code, headers, body). Use an analogy to support your explanation.

**Your Answer:**

A server is either a computer or program that can receive requests and send back a response. HTTP request-response cycle is how a client sends a request to a server, and the server will send back a response with the information or change requested by the client. The request includes the method, like `GET`, `POST`, `PATCH`, and `DELETE` which tell the server what the request wants, to read, create, update, or delete data. The endpoint of the API it wants to make a request to (which data to modify or read). The header is where we tell the server what method the request has and the content type. The request body is where information that is required to complete the response is stored when sent to the server. A response has a status code like `200`, `400`, and `500` to indicate whether the request was a success or error. 200 status codes indicate success, 400 status codes indicate a client error, and 500 status codes indicate a server error. The header has the content type of the response and the body is what we're sending back to the client. An analogy is ordering food online, we are the client, making a request to the restaurant, the server, with information like our address so they can complete the request and send us our response, in this context our food. Depending on if the delivery was successful or not, the app we used will tell us if we got our food or if it was canceled for a specific reason.

## Question 2: Middleware

What is middleware in Express? How does it differ from a regular controller? Explain the role of `next()` and provide an example of when middleware is useful.

**Your Answer:**

Middleware in Express is a function that we can use before our other controllers, which will always run no matter which endpoint or controller we hit. It differs from regular controllers because it's not endpoint specific but rather every endpoint will go through the middleware first. The `next()` is important as it tells the middleware to continue onto the next middleware or controller when it's done running, ensuring that the correct controller for which endpoint was hit will run, as well as other middleware.

## Question 3: API Key Security

Why is it dangerous to use API keys in client-side (frontend) code? Explain how a backend server solves this problem (the "proxy" pattern). Include what role environment variables (`.env`) play in this approach.

**Your Answer:**

It's dangerous to expose our API keys in our client-side because if the repo is public, anyone examining the code will be able to use our API key. The same is true if anyone checks our web app's source code through a browser. A backend server solves this problem using the proxy pattern and environment variables. We use a `.env` file to store our API key in a variable, and a `.gitignore` file to tell git to ignore `.env` files to prevent it from being pushed to our repo. Next, we import our variable into our server by requiring `dotenv` and calling `dotenv.config()`, which loads our `.env` file. We can now access our sensitive information in our server without third-party individuals accessing this information using `process.env.VARIABLE_NAME`. The proxy pattern is important as we're fetching information from a third-party API in our backend, then creating our own endpoints to display that information on our frontend. This means the frontend has no access to the original API and API key we're fetching from/using to fetch, but is still able to read that information from our endpoints.

## Question 4: Debugging a Server

A fellow student is building an Express server. They send a `PATCH` request to `/api/bookmarks/1` using Postman, but they receive a `404` status code. List at least three things you would check to debug this issue and explain why each one could be the cause of the problem.

**Your Answer:**

1. I would first check if a bookmark with the id 1 exists, `404` means data was not found, so it's possible that there was nothing with the id 1.

2. I would check if `app.patch('/api/bookmarks/:id', controller)` exists, if the endpoint doesn't exist, the catch-all 404 error will run for any endpoints that aren't defined.

3. I would check if our catch-all 404 controller is before or after our endpoints, if it's before any of our endpoints it will lead to a 404 because it uses `app.use` and JS is executed line by line.
