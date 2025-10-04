MODULE 0

I struggled matching the Python interpreter in PyCharm but figured out how to set it up.
Learned to use load_dotenv() to Safely load environment variables (API keys) instead of hardcoding them.
Successfully cloned a GitHub repo and ran a basic RAG application using the LangSmith docs as data.
Since it bwas a basic setup my only modification was adding more test questions to check if the AI was working correctly.

MODULE 1

Video 1: Traininng Basics

I learned how the @traceable decorator in LangSmith makes it simple to log traces by just adding it to a function. It automatically builds a run tree that shows every step of my application, including inputs, outputs, errors, and responses. This step-by-step view really helps in debugging, tracking latency, and even spotting places where I can parallelize expensive parts of the app. I also explored how metadata works — attaching key-value pairs like app version or environment to each run. This makes it easier to filter, group, and analyze runs later. Together, the run tree and metadata give me a clear picture of my app’s execution and make optimization much easier.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/tree/main/MODULE%201

Changes I made: 

Since there was nothing much to do in the already existing file. I just added a few more questions and observed the Trace tree and the metadata. I creatd a simple chatbot using the same concepts where I traced each call ( question asked by the user) using the "@traceable" decorator and passed the metadata ( question number ) during runtime and observed it in the trace tree in the langsmith desktop.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/tracing_basics_example.ipynb

Video 2: Types of Run

I learned the advantage of tracing over logging. In logging its difficult to find the root cause of an error while iterating through a stack trace. Especially in LLM applications because theres a lot of text to read through. Langsmith solves this issue by providing a very clean UI to track the traces.

LangSmith provides different types of run and we can specify what type our run is in the @traceable decorator
1. LLM: Invokes an LLM
2. Retriver: Retrives documents from databases and other sources
3. Tool: Executes actions with fucntion calls
4. Chain: Combines multiple runs into a larger process. This is a default run type
5. Prompt: Hydrates a prompt to be used with an LLM
6. Parser: Extracts structured data

Playground in LangSmith: It is a sandbox iteration environment where we can quickly iterate and test out new prompts. We get to use this when we use run_type="llm" and when we use the default run_type ie "chain" we do not get this option for it.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/types_of_runs.ipynb

Changes I made:

I wrote a code which tests and shows the use of llm and tools run type (with and without) . I defined a function that calculated the maths expression and a function where llm decides how to solve the expression and whether to call the tool or not. I also added the screenshots for all the codes from my langchain desktop in both of my files.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/types_of_run_example.ipynb

Video 3: Alternative ways to trace

In this video i learned that @traceabel decorator is the default way to set up tracing. Different nodes in a graph makes use of the langChain components. As in Langchain we can also pass metadata in langgraph as well using config argument that invoke takes. I also learned that tracing is done by default after setting up our environment variables and leveraging langchain and langgraph. Using with trace() helps us log any calls done within a specific block of code giving us more granular control. Next, I learned about the wrap_openai() which is for the users who want to use OpenAi SDK directly and it traces all openai calls. So now after wrapping up our openAI client , any calls made to it will be automatically get traced to langsmith. I also learned that we can pass metadata using langsmith_extra feild.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/alternative_tracing_methods.ipynb

Changes I made:

I modified my previous example ie the chatbot that I made and applied the new alternative ways to trace to it and observed the changes in the langsmith portal and added my observations with screenshots.
The alternative ways I applied: 
1. with_trace()
2. wrap_openai()

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/alternative_tracing_methods_example.ipynb

Video 4: Conversational Threads

In this video I learned about threads which basically is an abtraction which contains a series of traces where each trace is an invocation of our app. We can create thereads by passing a uuid as a pair value in the metadata using the langchain_extra feild. This is very useful when we want to debugg a full interaction between a human and the llm application that has multiple traces.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/conversational_threads.ipynb

Changes I made:
I revamped my chatbot to trace all the chats between the user and llm. I generate a new uuiad whenever the chatbot was invoked and provided that as a metadata. This helped me keep a track of all the traces related to a particular conversation between the user and the llm. I also added my observations and screenshots in the notebook.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%201/conversational_threads_example.ipynb
