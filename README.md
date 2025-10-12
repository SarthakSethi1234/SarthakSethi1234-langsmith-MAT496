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

MODULE 2

Video 1: Datasets

I learned about datasets which are primarily a list of examples which are used to test and evaluate our llm application rather than just doing a few random "gut checks". In this module we created datasets which comprised of both inputs and outputs. I also learned how to tag a paricular version of a dataset. These version tag are helpful when we want to test our appllication on previous versions of the application after making a few changes to the initial versions. I also learned how to add new data to the dataset directly from the trace runs and manually. Then i leanred about schema which enssures our data (current and future) is stored in a fomatted way. I also explored the feature to add some AI genrated examples. I also explored split which is used to isolate a few examples which we think are very important for our llm application to score good on. I also learned that we can share the dataset with others, download it or clone it.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/dataset_upload.ipynb

Changes I made:
I created my own dataset and followed all the instructions given in the video and attached the screenshots of all the steps followed.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/dataset_upload_example.ipynb

Video 2:

I learned about evauluators in this module. They are essentially functions or processes used to score and quantify the performance of your Large Language Model (LLM) application or agent on specific test cases. They compare the dataset example against the output of our llm and rate them based on a score. Furthermore evaluators can be defined in both the jupyter notebook or LangSmith website directly inside the database. We can define evaulators using our own custom code or use an llm as a judge.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/evaluators.ipynb

Changes I made:
I added my own carefully selected examples to the existing evaluator in the source code to show how the evaluator’s score changes as the quality of the output improves based on a chosen metric — in this case, coherence. I also defined a new evaluator that measures the coherence score of an LLM’s response compared to a reference response, using another LLM as a judge. The score ranges from 1 to 5, where 1 means highly coherent and 5 means poorly structured or inconsistent. I tested this evaluator with different types of outputs to check its reliability, and it worked as expected. I also attached the screenshots of my observations in the above link.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/evaluators_example.ipynb

Video 3: Experiments

Experiments are basically running your llm application over a dataset and evauluating its performance with evaluators. We can run experiments in our SDK( using evaluate() ) or in the langsmith UI. I also analysed the impact of chanhing the llm model on the evaulation of the performance. I also learned how to run our experiment on specific subsets of examples like the initial version of the dataset and the split versions, and individual examples. I also learned that we can run our experiment over a certain example for x number of times this ensures us that we get consitent results. We can also run our experimnets with different parameters such as repetition, concurrent threads and metadata.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/experiments.ipynb

Changes I made:
I created my own dataset based on a few facts about the planets and ran all the code snippets I had written on it. I carefully observed the outputs to see how the evaluators scored different responses and how the metrics behaved with my data. I also attached screenshots from my LangChain portal to show the results and the run trees for each example, giving a clear picture of how everything worked end-to-end.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/experiments_example.ipynb

Video 4: Analysing Experiments

I learned how to systematically evaluate LLM applications using multiple evaluators - both code-defined (is_concise) and UI-configured (correctness) - to track performance trends over time as I iterate on my application. The platform's filtering capabilities allowed me to isolate specific model runs (like gpt-4o) and compare experiments side-by-side through summary charts and latency metrics, providing hard empirical data to justify production deployments. Most valuable was the ability to deep dive into individual experiment runs and trace how each dataset example performed, enabling me to identify specific failure patterns and make data-driven optimizations with confidence before pushing changes to production.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/analysing_experiments.ipynb

Video 5: [Optional] Pairwise Experiments

I learned that the core value of pairwise experiments is to perform a direct, comparative evaluation between two distinct versions of your application (e.g., a new prompt vs. the old one). This is achieved by running both versions on the same dataset and then using a sophisticated LLM-as-a-Judge to objectively score which output is better.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/pairwise_experiments.ipynb

Changes I made:
I used a different customer data set and asked the llm to summarize them then compared which summary is better and then analysed the results. This example was quite similar to the example done in the tutorial

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/pairwise_experiments_example.ipynb

Video 6: [Optional] Summary Evaluators

What I learned from this is that summary evaulators take in a list as input rather than normal evaulator which take in a single input and compare that against a single output and after taking in the list these summary evaulators calculate a aggregate metrics for the entire dataset. Thus F1 score makes sense for the entrire dataset and not just a single example.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%202/summary_evaluators.ipynb

MODULE 3

Video 1: Playground

I learned the difference between the prompt templates and hardcoded prompts. Prompt templates gives user more flexibility by having certain variables. Further I learned how to use Playground on langsmith desktop. On exploring a few prompts, I noticed how dramatically our output changes on changing our system prompt. In the playground I can also test out different models on different parameters and compare their performace and outputs on same prompts. We can also see our outputs in a non streaming way. Next I lerned about output schema, which forces the model's output to follow a certain format. I also learned that we could use a tool instead of output schema here. I also leaned that we can run tests on our datasets in the playground

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%203/playground_experiments.ipynb

Changes I made:

Since this video contained breif introduction to playground and its features, I explored all of it with the tutorial and attached all of its screenshots in the notebook.

Link: https://github.com/SarthakSethi1234/SarthakSethi1234-langsmith-MAT496/blob/main/MODULE%203/Playground.ipynb

Video 2: Prompt Hub

I learned about langsmith's prompt hub which is a great place for users to store their prompt templates. This typically contains a list of messages which can be either system message or human message. These are not just strings but modifiable template which can contain variables that the user will input at the run time. A prompt template contains: Templated messages, model configuration and may or may not contain an output schema.

Link:

Chnages I made:

Firstly, I followed the tutorial and pasted all the observations as screenshots in the original notebook. Secondly, I created a new notebook wherein I created my own prompts and tested them out. I explored Pulling prompts from Prompt Hub, commiting changes to that prompt and uploading prompts via SDK.

Link:






  
