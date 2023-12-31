# SuiGPT

<!--
<img width="1318" alt="image" src="https://github.com/GPTutor/SuiGPT/assets/43432631/0c951180-51dc-4569-9df3-b5046ecd1363">
-->
<img width="1293" alt="image" src="https://github.com/GPTutor/SuiGPT/assets/43432631/897f3139-9dfb-4b73-9012-95849d466c77">

Through tailored Prompt Engineering, SuiGPT empowers GPT-4 to be proficient in the Move language, enabling it to generate corresponding Move code based on user instructions. It can be used through the GPTutor interface, and its API to get Prompt by user instruction is available on the Web. The website version is coming soon.


[Slides link (Pitch Deck)](https://drive.google.com/file/d/1IPKivJn1FpQpimrW9LJq9tF-riP7bBmz/view?usp=sharing)

[Click me to Download GPTutor and try SuiGPT in Visual Studio Code IDE](https://marketplace.visualstudio.com/items?itemName=gptutor.gptutor&ssr=false#overview)

[What Sui Technologies incorporated?](https://github.com/GPTutor/SuiGPT/blob/main/Sui-Technology-integrated.md)


## Introduction

While GPT-4 is incredibly powerful, it lacks knowledge of Sui Move in its training data, resulting in its unfamiliarity with the syntax and writing style of Sui Move. However, we believe that by providing Sui-Move examples through prompts, GPT-4 can generate Sui-Move code accurately. 

<img width="50%" alt="image" src="https://github.com/GPTutor/SuiGPT/assets/43432631/6b66963d-c6b6-4510-865e-dce4e324d1a5">

## How it work?

SuiGPT collect Move codes from the [official Sui example codes](https://github.com/MystenLabs/sui/tree/main/sui_programmability/examples), annotated them, and stored them in a database. When users want to create Move smart contract with SuiGPT. SuiGPT will provides relevant code snippets in prompts for GPT to reference. By doing so, SuiGPT can integrate various existing and executable Move contract functionalities, creating personalized new contracts for users.

<img width="1455" alt="image" src="https://github.com/GPTutor/SuiGPT/assets/43432631/789a85ed-d333-4b95-a12c-dcbacf614537">


## Finished Milestones

During the Taipei Blockchain Week hackathon, we accomplished the following four parts:

1. Annotated Move by Sui-Move Analyzer and GPT-4
2. Create Dataset: Process 68 move files with GPT to add comments and store them in a database
3. Create Prompt: By user’s input, query similar Move codes and assemble them to create a prompt for GPT-4 to reference.
4. Integrated SuiGPT into GPTutor.

All the above are open-source and available by Web API.

### 1. Annotated Move Code by Sui-Move Analyzer and add Comment and Summary by GPT-4
We use Sui-Move Analyzer to add type annotations to the Move code. Then, we utilize GPT-4 to annotate and summarize the code. 

The annotation API is available at https://move-annotate-backend.gptutor.tools/api/docs. Moreover, the source code of the annotation API is available at [GPTutor/sui-move-annotation](https://github.com/GPTutor/sui-move-annotation).

Moreover, SuiGPT's Sui-Move annotation also supports the [smart contract from the Bucket Protocol](https://github.com/Bucket-Protocol/v1-periphery), allowing users to generate smart contract applications that call the Bucket Protocol endpoints using SuiGPT.

<img width="1264" alt="image" src="https://github.com/GPTutor/SuiGPT/assets/43432631/0b144556-b17f-4a54-a17f-6f3e5e49d381">

### 2. Create Dataset
We collected 68 move files from [Sui's official example code](https://github.com/MystenLabs/sui/tree/main/sui_programmability/examples). After processing them through step one, we saved them in the ElasticSearch database, and the processed data [can be downloaded here](https://docs.google.com/spreadsheets/d/1DrjLQnYGKMtJHt0B0jfU3I7MuQPadUYxHnbVZKSNH9w/edit#gid=1582387538).

The source code of data processing and database creation is available at [GPTutor/SuiGPT-backend](https://github.com/GPTutor/SuiGPT-backend).

### 3. Create Prompt
By the users' input about what kinds of Move contracts they want to write, SuiGPT prompt creation backend will query similar Move codes by [ElasticSearch's "more like this"](https://www.google.com/search?q=ElasticSearch+more+like+this+query&oq=ElasticSearch+more+like+this+query&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIGCAEQLhhA0gEIMjI1MmowajGoAgCwAgA&sourceid=chrome&ie=UTF-8) query. Then, pick the top 3 matched codes and assemble them in a prompt for GPT-4 to reference. 

For example, if a user says they want to create a fungible coin with airdrop feature, the backend will query Elasticsearch and find the following Move smart contract with top similarity scores: `Managed Fungible Tokens`, `Cross-Chain Airdrops of NFTs`. Then, SuiGPT API will create a prompt including these codes so GPT-4 can synthesize them to create a fusion of new Move contracts to fit the user's needs.

The prompt creation API is available at [https://backend.suigpt.gptutor.tools/api/docs](https://backend.suigpt.gptutor.tools/api/docs), and it's source code is at [GPTutor/SuiGPT-backend](https://github.com/GPTutor/SuiGPT-backend).

<img width="1455" alt="image" src="https://github.com/GPTutor/SuiGPT/assets/43432631/789a85ed-d333-4b95-a12c-dcbacf614537">


### 4. Integrated SuiGPT into GPTutor
We integrated SuiGPT with GPTutor. GPTutor is a Visual Studio Code extension that enables users to use OpenAI's GPT models for code explanations, comments, and reviews. One of GPTutor's standout features is its open-source nature, which grants users the flexibility to customize their prompts. By dynamically querying prompts created by SuiGPT through the API into GPTutor, GPTutor is now able to compose Sui-Move according to users' instructions.

Furthermore, the API for generating prompts for SuiGPT is publicly available, so anyone can integrate SuiGPT into their AI coding services.

## Future Milestones:

- 2023 (Q4): Include more Move code as data
- 2023 (Q4): Train and Evaluate LLMs, such as GPT and CodeLLaMA, with the Move database we created.
- 2024 (Q1): Integrated SuiGPT into a Website so users can access SuiGPT from a browser
- 2024 (Q2): Write a research paper about SuiGPT
- 2024 (Q2*): Integrated SuiGPT into Sui-Move Web IDE to generate move code (* If Sui plans to lunch a Web IDE)
  

