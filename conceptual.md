### Conceptual Exercise

Answer the following questions below:

- What is a JWT?
JWT is a compact, URL-safe means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is digitally signed using JSON Web Signature (JWS).

- What is the signature portion of the JWT?  What does it do?
The signature portion of a JWT ensures the data integrity of the token and verifies the sender's identity. It's created by encoding the header and payload using a secret key, which makes it computationally infeasible to alter without detection.

- If a JWT is intercepted, can the attacker see what's inside the payload?
 If a JWT is intercepted, the attacker can see what's inside the payload because it's only base64 encoded, not encrypted. However, they cannot alter the payload without invalidating the signature.

- How can you implement authentication with a JWT?  Describe how it works at a high level.
A user logs in with credentials.
The server validates the credentials and generates a JWT.
The JWT is sent back to the user.
The user stores the JWT and includes it in the header of subsequent requests.
The server verifies the JWT and grants access based on its validity.

- Compare and contrast unit, integration and end-to-end tests.
Unit Tests: Test individual components or functions in isolation.
Integration Tests: Test the interaction between integrated units/modules.
End-to-End Tests: Test the entire application's workflow as it would be used by an end user.

- What is a mock? What are some things you would mock?
A mock is a simulated object that mimics the behavior of real objects in controlled ways. Commonly used to test interactions with external services, databases, or complex system integrations.

- What is continuous integration?
CI is a software development practice where developers regularly merge their code changes into a central repository, after which automated builds and tests are run.

- What is an environment variable and what are they used for?
These are dynamic-named values that can affect the way running processes behave on a computer. They're used for configuring applications, storing sensitive information like API keys, database URLs, etc., outside the codebase.

- What is TDD? What are some benefits and drawbacks?
Benefits: Ensures thorough test coverage, promotes simpler design, and catches bugs early.
Drawbacks: Can be more time-consuming initially, requires a change in mindset, and can be challenging for complex scenarios.

- What is the value of using JSONSchema for validation?
It ensures the structure and format of JSON data is correct, enhances API reliability, and reduces the likelihood of invalid or malformed data being processed.

- What are some ways to decide which code to test?
Focus on parts of the application that are most prone to errors, critical to the functionality of the application, or have had recent changes.

- What does `RETURNING` do in SQL? When would you use it?
This clause is used to return data from inserted, updated, or deleted rows. It's particularly useful in scenarios where you need immediate feedback about the operations performed, like getting the ID of a newly inserted row.

- What are some differences between Web Sockets and HTTP?
Web Sockets: Allow for full-duplex, bidirectional communication. They keep a persistent connection open for real-time data transfer.
HTTP: A stateless, request-response protocol typically used for retrieving web pages and API calls.

- Did you prefer using Flask over Express? Why or why not (there is no right
  answer here --- we want to see how you think about technology)?
  I prefer Express since it's the technology primarily used for full stack web development, while flask focuses more on simplicity, small and medium size projects.
