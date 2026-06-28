## LLM Evaluation

```python
# Pytest -
import os
import pytest

from langchain_openai import ChatOpenAI
from ragas import SingleTurnSample
from ragas.llms import LangchainLLMWrapper
from ragas.metrics import LLMContextPrecisionWithoutReference


#user input => Query
#response => response
#reference => Ground truth
#retrived context => Top k retrieved docs

@pytest.mark.asyncio
async def test_context_precision():
    # create object of class for that specific metric

    os.environ["OPENAI_API_KEY"] = "API Key"



    # power of LLM + method metric => score
    llm = ChatOpenAI(model="gpt-4",temperature=0)
    langchain_llm = LangchainLLMWrapper(llm)
    context_precision = LLMContextPrecisionWithoutReference(llm = langchain_llm)

    # Feed data -
    sample = SingleTurnSample(
        user_input="How many articles are there in the Selenium webdriver python course?",
        response='There are 23 articles in the course.',
        retrieved_contexts=[
            "Selenium WebDriver with Python - Introduction: This course includes 23 detailed articles covering topics like installation, locators, waits, and automation frameworks using Selenium WebDriver in Python.",
            "Course Outline: The Selenium WebDriver Python course is divided into 23 modules, each focusing on specific aspects of web automation.",
            "FAQs: Q: How many articles are there in the course? A: The course has a total of 23 articles."
        ]

    )

    #score
    score = await context_precision.single_turn_ascore(sample)
    print(score)

```