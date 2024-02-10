# Project to Demo API Tests for Proxima AI
### Task 1:
1. All the tests are in the postman folder in the Proxima_AI_Quiz.postman_collection.json file.
2. There is a circleci config yml in the .circleci folder that runs the tests on a new commit/merge.
3. We can also add a rate limiting test using the newman --iteration-count parameter set to 20000 which is the request limit per day for anapioficeandfire but I have no way of unblocking myself after so it is just mentioned here.

To run the collection via newman locally and or generate a report run the following commands from a terminal:
> npm i  
> npm run test  
> npm run report

![Postman Test Cases](./assets/postman_test_cases.png "CircleCI")  
![Circle CI Test Run](./assets/circleci_run.png "CircleCI")  
![Newman Report](./assets/newman_report.png "Newman Report")

### Task 2:
![Test Case Scenario 2](./assets/test_case_scenario.png "Task 2")  

There are a few unknowns and considerations that need to be made for this scenario. First I do not have all the context for this scenario since I have never run this test manually (which is usually what I would do for any new test before autoamting it) so some of the things that I say may be completely unviable. Here are some of the assumptions that I made:
1. We have an APi that lets us simulate that a user has abandoned the shopping cart.
2. We can use the API in assumption 1 to save the cart data to the database and retrieve it.
3. We also have an API that is sending the triggering request to the cron job (probably the same one in 1, it's also fine if it's different).
4. We can set up a webhook to send the SMS from twilio as an email.

If we have all the means mentioned in the assumption then we can formulate a test case as follows using Cypress/Playwright:
1. Start the test when we receive the response that a shopping cart has been abandoned.
2. Verify that the cart data is saved to the database.
3. Verify that the cart data can be retrieved from the database for our cron job to trigger.
4. Simulate the passing of time via a wait.
5. Send the SMS as an email.
6. Use Gmail API to parse the SMS message.
7. Validate the SMS message details.
