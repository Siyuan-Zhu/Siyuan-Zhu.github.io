---
title: Large Language Models for 5 Digit OECD Health Sector Classification
categories:
- Research 
- Applied Machine Learning
excerpt: |
  This is an semi-formal documentation paper for my ongoing applied ML research project at Aid Data 
feature_text: |
  ## Applied ML Research at Aid Data
  
feature_image: "https://picsum.photos/2560/600?image=733"
image: "https://picsum.photos/2560/600?image=733"
---

<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>5-Digit Coding Project</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html">
<h2 id="introduction">Introduction</h2>
<p>Aid Data’s TUFF (<a href="https://www.aiddata.org/methods/tracking-underreported-financial-flows">Tracking Underreported Financial Flows</a>) team aims to provide comprehensive information about aid and credit from official sector donors and lenders who do not publish comprehensive or detailed information about their overseas activities according to existing global reporting systems, such as the <a href="http://stats.oecd.org/">OECD’s Creditor Reporting System</a> and the International <a href="http://www.aidtransparency.net/">Aid Transparency Initiative (IATI)</a>. Sector classification based on <a href="https://www.oecd.org/dac/financing-sustainable-development/development-finance-standards/purposecodessectorclassification.htm">OECD’s guidelines</a> are represented by 3 and 5 digit purpose codes. These purpose codes provide fine-grained information that aims to answer the question: “which specific area of the recipient’s economic or social structure is the transfer intended to foster?”</p>
<p>Currently, within Aid Data’s workflow, 3-digit (CRS) purpose codes are recorded for each project. However, 3-digit codes contain less fine-grained sectorial information compared to 5-digit codes. Having 5-digit purpose codes adds a new variable to the TUFF dataset, which would provide more detailed sectoral information for each project on the record and support more accurate sectoral research &amp; analysis.</p>
<p>In our work, we frame the task of OECD 5-digit coding as a <a href="https://arxiv.org/abs/1910.10683">sequence-to-sequence conditional generation</a> problem. We rely on the strong in-context learning and instruction-following capabilities of large language models and prompt the LLM with task instructions that include the OECD sector guidelines, as well as in-context examples in the form of input-output pairs in order to facilitate the model to generate the desired representation of the 5-digit code. The dataset we use contains 481 hand-coded and verified historical projects (1965-1999) in the health sector. Our best results are achieved by implementing <a href="https://arxiv.org/abs/2101.06804">semantic similarity-based in-context example selection</a>, with an average accuracy of over 96% (k=5,8,10), and best accuracy of 96.84% (k=10).</p>
<p>Currently, our method has only been applied and experimented in the health sector, partially due to the lack of labeled datasets for benchmarking in other sectors. Future work direction includes exploring standardized procedures to extend our prompt-based framework in other sectors, as well as further exploring the reliability and sensitivity of this framework. Particularly considering how the model reacts to longer, more diverse project description texts, as well as more complex instructions for categorization.</p>
<h2 id="problem-statement">Problem Statement</h2>
<p>The creation of 5-digit codes for recorded projects involves the following steps:</p>
<ol>
<li>For each project recorded using the TUFF methodology, a project title and description are developed by research assistants, providing detailed information about the project.</li>
<li>Additionally, a 3-digit CRS code is assigned to each project. These 3 and 5 digit codes are formatted hierarchically, meaning an additional 2 digits are added to each 3-digit sector code to represent more specific sectorial information, thereby forming a 5-digit sectorial code.</li>
<li>Given the detailed information for each project and the 3-digit code, the coder reviews the relevant information and determines which specific area of the recipient’s economic or social structure the transfer is intended to foster, according to the OECD guidelines.</li>
</ol>
<p>Previously, this process was conducted manually by research assistants, posing a significant challenge due to high costs and time consumption. The utilization of machine learning and large language models for encoding will not entirely eliminate the need for human verification, but it will significantly reduce the time, effort, and organization required to encode projects on a larger scale.</p>
<h2 id="dataset-description">Dataset Description</h2>
<p>The labeled dataset currently in use is a product of a collaboration between Aid Data and Ignite Lab in the summer of 2022. This dataset, which covers historical Chinese development finance health projects, contains 481 projects that document China’s foreign health-sector aid history in Africa before 2000. For each project, research assistants (including myself) manually produced the 5-digit code, which was then verified by staff members during the quality assurance process. The dataset columns are as follows:</p>
<ul>
<li>project_id: internal id for identification</li>
<li>flow: financial flow type</li>
<li>title: title of the project</li>
<li>year: year of the project</li>
<li>year_uncertain: certainty of which the project occurred in “year” column</li>
<li>description: detailed description of the project</li>
<li>all_recipients: recipient country of the project</li>
<li>official_sources_count: number of official sources on record</li>
<li>non_official sources: list of non-official sources</li>
</ul>
<p><strong>For this project, only the “title” and “description” columns are used for 5-digit coding with large language models.</strong></p>
<h2 id="large-language-model-application-and-selection">Large Language Model Application and Selection</h2>
<p>Due to recent advancements in the field of AI, transformer-based Large Language Models (LLMs) have become more powerful, achieving human-level or superior performance in various NLP tasks. Our work aims to semi-automate the process of 5-digit coding in various sectors using publicly available language models.</p>
<p>In this work, we treat the process of 5-digit coding as a sequence-to-sequence conditional text generation problem. We use the recently released, open-source model <a href="https://arxiv.org/abs/2205.05131">FLAN-UL2</a> <a href="https://huggingface.co/google/flan-ul2">published by Google</a> to achieve strong results in our experiments. FLAN-UL2 is a pre-trained and instruction-tuned 20B parameter model with an encoder-decoder <a href="https://arxiv.org/abs/1706.03762">transformer architecture</a>. It currently ranks as the best open-source model on comprehensive NLP benchmarks such as <a href="https://arxiv.org/abs/2210.09261">Big-Bench hard</a> and <a href="https://paperswithcode.com/dataset/mmlu">MMLU</a>. We provide more details about our methodology below.</p>
<h2 id="methodology">Methodology</h2>
<p>We leverage the strong in-context learning and instruction-following capabilities of FLAN-UL2 to facilitate the task of 5-digit coding. We frame this task as a reading-comprehension and text-categorization problem in the task instruction, concatenating in-context examples in the form of input-output pairs.</p>
<p>We experimented with 0-shot and few-shot prompting, achieving an initial accuracy of 88% with 0-shot prompting, 92% (k=5) and 95% (k=7) with hand-selected in-context examples. However, the process of manually selecting in-context examples proved to be suboptimal because it requires an iterative, trial and error process. Furthermore, the selection of effective examples relies heavily on intuition. Motivated by the need to eliminate the manual selection process and increase accuracy and robustness, we implemented similarity-based in-context example selection, as detailed by <a href="https://arxiv.org/abs/2101.06804">Liu et al</a>. We used the standard pre-trained sentence transformer from <a href="https://arxiv.org/abs/1908.10084">SBERT</a> as the embedding model. The semantic similarity-based selection consistently improved overall accuracy (k = 5, 8, 10) compared to manual selection, with an average accuracy of over 96% (best 96.84% , k=10). Further, we tested the effect of permuting the order of in-context examples to account for <a href="https://arxiv.org/abs/2104.08786">recency bias</a>. We observed little variance introduced by the reversal of example order. The number of in-context examples (k) is limited by the model context length of 2048 tokens.</p>
<p>For the manual example selection process, we began by including five random examples. After comparing the model’s results with the human-labeled results, we found that the most miscoded projects by the model fell into the 12191 Medical services category (confusing “equipment” with “infrastructure”). We thus added two more examples for code 12191 involving such cases to the prompt, aiding the model in understanding this coding criterion. The model was able to learn to distinguish this detail with just two demonstrations. Finally, with seven examples included in the prompt, we achieved a 95% accuracy on the testing data.</p>
<h2 id="future-development-directions">Future Development Directions</h2>
<p>There are several directions for the further development of this project. The first is to explore and develop a standardized procedure to expand and apply our prompt-based method to other sectors. A few challenges are presented when generalizing our method. Because our experiments conducted so far only involve projects in the health sector, there are only about 12 different 5-digit level criteria for consideration, all of which fall under the 120 and 121 3-digit CRS codes. In a more general scenario where projects span many different sectors (each falling under a specific 3-digit CRS code), there will be many more 5-digit criteria of varying lengths to consider under each 3-digit CRS code.</p>
<p>Theoretically, this challenge can be overcome by dynamically switching between different prompts (including instructions and demonstrations) for projects under each sector. Assuming each project has already been assigned a 3-digit CRS code, the number of 5-digit level criteria to consider can be reduced to only those under the 3-digit CRS code, similar to the case for the health sector in our experiments. Therefore, we propose to construct prompts for each sector (i.e., for each 3-digit CRS code, construct instructions that include only 5-digit criteria expanding upon the 3-digit code). Then at inference time, we feed the model the corresponding prompt based on the 3-digit code of individual projects. It is important to note that under our current method, there is no need to train specialized sub-models for each sector (i.e., for each prompt), since we did not modify the weights of the FLAN-UL2 model via fine-tuning and rely only on in-context learning at inference time to achieve our results. This means that we can use the same set of model weights for all specialized prompts.</p>
<p>Another challenge is the lack of readily available labeled data in other sectors to construct a sufficiently large pool for semantic similarity-based demonstration selection. One critical aspect that contributed to the success of experiments in the health sector is the ability to utilize already labeled data for dynamic demonstrations. However, in-context learning is much more sample-efficient than traditional supervised learning. A practical way to overcome the lack of labeled data is to follow the vote-k selective annotation framework detailed by Su et al. This framework selects a few (&lt;100) diverse and representative unlabeled projects to manually annotate. Paired with semantic similarity retrieval, this framework achieves better results with small annotation budgets. We plan to implement and follow this framework for different sectors in order to construct small but effective demonstration selection pools for in-context learning, paired with sector-specific instruction prompts.</p>
</div>
</body>

</html>
