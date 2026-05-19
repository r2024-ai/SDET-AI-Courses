## AI-Powered Automation with Playwright MCP, GitHub Copilot and & VS Code

## AI Integration with Playwright

* AI is a big umbrella under which we have multiple domains - Robotics, Neural Networks, Data Science
* GenAI - It is basically generate the content based upon the knowledge it already have
* Tools - LLM, Agent, MCP
  * Popular LLMS - ChatGPT, Google Gemini, Claude, DeepSeek
  * LLM's can learn the things but cannot act/execute
* Prompting - Providing inputs/instructions to the LLM
* Agent - It is an assistant that actually does what the LLM says. It can perform actions(execution)

* How do we integrate LLM and agent?

Step 1 - 
1. Install GitHub copilot extension

![alt text](image.png)

Step 2 - 
* Install Playwright

![alt text](image-1.png)

Playwright VSCode extension(Optional)

![alt text](image-2.png)

Step 3 -  

Install Playwright MCP server

![alt text](image-3.png)

Click on Install server

![alt text](image-4.png)

Step 4 -  

* Ctrl + Shift + P
  * Preferences: Open User Settings (JSON) => Not anymore
  * Type - Open User MCP Configuration

Add this there - 

```json
{
  "servers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

![alt text](image-5.png)


* **Prompt**

```txt
you re a playwright test generator.'
you are given a scenario and you need to generate a playwright test for it.
DO NOT generate test code based on the scenario alone.
DO run steps one by one using the tools provided by the Playwright MCP.
Only after all steps are completed, emit a Playwright TypeScript test that uses
@playwright/test based on message history
save generated test file in the tests directory.
Execute the test file and iterate until the test passes.
```

To run the test cases - 

`npx playwright test --project=chromium --headed`

```txt
Open https://petstore.octoperf.com/actions/Catalog.action
Enter "fish" in search box
Click Search button
Verify "Angelfish" is present in results
```

## API Tests

```txt
Create a POM model for below steps :
1. Navigate to https://petstore.octoperf.com/actions/Catalog.action 
2. Search for "Fish" in search box and press enter
3. Verify that "Goldfish" is in the table
```

* Prompt

```txt
You are an API test generator using Playwright MCP.
Use Playwright's 'request' context and "@playwright/test" framework.
The test should : 
- Send HTTP requests to the target API. 
- Validate the status code, response body, and schema(if applicable). 
- Use aync/await syntax. 
- Print useful logs for debugging if needed. 
- Export the test to a ".spec.ts" file under the "/tests" folder.
Do not generate test code until all steps are fully explored and validated.
```

* **API Test**

```txt
Generate a Playwright API test for the following scenario :
1. Define the API endpoint URL:https://fakestoreapi.com/products/1
2. Send a GET request to the endpoint.
3. Verify the response status  is 200
4. Validate the response contains these keys:'id', 'title', 'category', and 'description'.
5. Optionally validate the data types using a JSON Schema(Ajv).
6. Log the product title and price to the console.

```