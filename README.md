# Misinformation_Detection_Using_LLM
In this Repository we explore how LLMs can be utilized for fact-checking.

The proliferation of misinformation and fake news is one of the biggest curses of the modern humanity [4]. The human factcheckers are struggling to get their grip on the ever-increasing volume of deepfakes. The work on this project was inspired by [1], where the authors were looking at various linguistic cues to automatically distinguish between facts and misinformation.

In this project, we are taking the approach of the linguistic cues to the extreme, that is to LLMs, where the volume of parameters is measured in billions. Additionally, the LLM literature [3] provides suggestions that the growth of LLM size brings with it the ‘emergent abilities’, particularly ‘factchecking’ ability in GPT-3.5-turbo from OpenAI. So naturally we use this LLM for our project.

To test LLM factchecking ability we took the Politifact Fact Check Dataset [5]. It is high-quality fact-check dataset collected from a popular fact check website PolitiFact (https://www.politifact.com/). The dataset contains 21,152 statements that are fact checked by experts. All the statements are categorized into one of 6 categories: true, mostly true, half true, mostly false, false, and pants on fire. Along with various details around fact checking, Also included are the sources where the statement appeared, which could be crucial for extracting various insights about fact checking. Furthermore, provided are the links to the fact check article published on Politifact so that extra text can be extracted regarding the published fact check story if needed.

The most important factor in using LLM is the prompt. Literally how one prompts LLM is what is one gets from LLM in return. After several prompt iterations we have engineered our prompt as following:

“Your task is to fact-check a claim \
 When factchecking use clear language such as ‘true’ and ‘false’, and avoid negations.”

Also for demonstration purposes we took the subset of the original dataset with verdicts of only ‘true’ and ‘false’, which is still 8088 records.

The available LLM subscription places the constraints of 3 requests per minute, or 180 requests per hour, i.e. two days running non-stop is needed to test the 8088 records. Therefore less ambitious number of records of 400 was randomly taken from the ‘true-false’ subset of the original dataset. Still, when running the automated factchecking query the LLM stopped responding on 132nd request (read timeout=600). That was our best result, while other attempts have generated smaller number of LLM responses, with error statements of ‘server overload’ or ‘connection is broken’.

When comparing the outcome of the automated LLM factchecking with the verdicts of human factcheckers, the confusion matrix showed that 92 ‘false’ and 2 ‘true’ statements were identified correctly, 36 statements were false negatives, and 2 statements were false positives.

That brought us to the accuracy of 71%, which of course not much, however better then random. It is also similar to the accuracy result in more thorough research described in [2].

Moving forward, we believe that LLM factchecking is very promising domain, especially because large LLMs, like GPT4, are expected to have better abilities for factchecking. So LLMs might one day be able to help the human factcheckers to effectively and efficiently fight the ever-growing volume of misinformation.

References
1.	Astrid Krickl, Sabrina Kirrane. "Misinformation Detection: Using Linguistic Cues" Semantics Vienna 2022, Sep 14, 2022. (accessed May 18, 2023). https://ceur-ws.org/Vol-3235/paper9.pdf 
2.	Hoes, Emma, Sacha Altay, and Juan Bermeo. 2023. “Using Chatgpt to Fight Misinformation: Chatgpt Nails 72% of 12,000 Verified Claims.” PsyArXiv. April 3. doi:10.31234/osf.io/qnjkf
3.	Wei, Jason, Yi Tay, Rishi Bommasani, Colin Raffel, Barret Zoph, Sebastian Borgeaud, Dani Yogatama, Maarten Bosma, Denny Zhou, Donald Metzler, Ed Huai-hsin Chi, Tatsunori Hashimoto, Oriol Vinyals, Percy Liang, Jeff Dean and William Fedus. “Emergent Abilities of Large Language Models.” Trans. Mach. Learn. Res. 2022 (2022): https://arxiv.org/abs/2206.07682
4.	MIT Open Documentary Lab. (2023) „Just Joking! Deepfakes, Satire, and the Politics of Synthetic Media“ (accessed July 2, 2023). https://cocreationstudio.mit.edu/just-joking/
5.	Misra, Rishabh (2022). "Politifact Fact Check Dataset." DOI: 10.13140/RG.2.2.29923.22566
