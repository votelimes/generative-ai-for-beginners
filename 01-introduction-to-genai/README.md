# Введение в генеративный искусственный интеллект и большие языковые модели

[![Introduction to Generative AI and Large Language Models](./images/01-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://learn.microsoft.com/_themes/docs.theme/master/en-us/_themes/global/video-embed.html?id=36c6795a-e63c-46dd-8d69-df8bbe6e7bc9?WT.mc_id=academic-105485-koreyst)

*(Click the image above to view video of this lesson)*

Генеративный ИИ — это искусственный интеллект, способный генерировать текст, изображения и другие типы контента. Что делает эту технологию фантастической, так это то, что она распространяет ИИ: любой может использовать ее, используя естественный язык. Вам не нужно изучать такой язык, как Java или SQL, чтобы добиться чего-то стоящего, все, что вам нужно, это использовать свой язык, сформулировать то, что вы хотите, и получить ответ от модели ИИ. Возможности использования этой технологии огромны: вы создаете или конспектируете отчеты, пишете программы и многое другое, и все это за секунды. 

В этом курсе мы рассмотрим, как наш стартап использует генеративный искусственный интеллект для открытия новых сценариев в мире образования и как мы решаем неизбежные проблемы, связанные с социальными последствиями его применения и технологическими ограничениями.

## Введение

В этом уроке будут рассмотрены:

* Введение в бизнес-сценарий: идея и миссия нашего стартапа.
* Генеративный искусственный интеллект и как мы попали в современный технологический ландшафт.
* Внутреннее устройство большой языковой модели.
* Основные возможности и варианты практического использования больших языковых моделей.

## Цели обучения

Пройдя этот урок, вы поймете:

* Что такое генеративный искусственный интеллект и как работают большие языковые модели.
* Как можно использовать большие языковые модели для различных случаев использования с акцентом на сценарии обучения.

## Сценарий: наш образовательный стартап 

Генеративный искусственный интеллект (ИИ) представляет собой вершину технологии ИИ, отодвигая границы невозможного дальше. Генеративные модели ИИ имеют различные возможности применения, но в этой учебной программе мы рассмотрим, как они революционизируют образование с помощью вымышленного стартапа. Мы будем называть этот стартап *наш стартап*. Наш стартап работает в сфере образования с амбициозной миссией: 

> *улучшение доступности обучения в глобальном масштабе, обеспечение справедливого доступа к образованию и предоставление индивидуального опыта обучения каждому учащемуся в соответствии с его потребностями*.

Наша команда стартапа осознает, что мы не сможем достичь этой цели без использования одного из самых мощных инструментов современности — больших языковых моделей. (БЯМ(LargeLanguageModel, LLM)).

Ожидается, что генеративный искусственный интеллект произведет революцию в том, как мы учимся и обучаем сегодня: учащиеся будут иметь в своем распоряжении виртуальных учителей 24 часа в сутки, которые предоставляют из себя огромные объемы информации и примеров, а учителя смогут использовать инновационные инструменты для оценки своих учеников и предоставления обратной связи.

![Five young students looking at a monitor - image by DALLE2](./images/students-by-DALLE2.png?WT.mc_id=academic-105485-koreyst)

Для начала давайте определим некоторые основные понятия и терминологию, которые мы будем использовать в учебной программе.

## Как мы получили генеративный ИИ?

Несмотря на необычайный *хайп*, вызванный в последнее время анонсом генеративных моделей искусственного интеллекта, эта технология разрабатывается десятилетиями, а первые исследовательские усилия относятся к 60-м годам. Сейчас мы подошли к моменту, когда ИИ обладает человеческими когнитивными способностями, такими как разговор, как показано, например, [OpenAI ChatGPT](https://openai.com/chatgpt) или [Bing Chat](https://www.microsoft.com/edge/features/bing-chat?WT.mc_id=academic-105485-koreyst), который также использует модель GPT для построения диалогов Bing в веб-поиске.

Возвращаясь немного в прошлое, самые первые прототипы ИИ представляли собой машинописные чат-боты, опиравшиеся на базу знаний, разработанную группой экспертов и представленную в компьютере. Ответы в базе знаний выискивались по ключевым словам, появляющимися во входном тексте(в запросе).
Однако вскоре стало ясно, что такой подход с использованием машинописных чат-ботов плохо масштабируется.

### Статистический подход к ИИ: машинное обучение

Поворотный момент наступил в 90-е годы с применением статистического подхода к анализу текста. Это привело к разработке новых алгоритмов, известных под названием машинное обучение, способных изучать закономерности на основе данных без явного программирования. Этот подход позволяет машине имитировать понимание человеческого языка: статистическая модель обучается на парах входные-выходные данные(text-label), что позволяет модели классифицировать неизвестный входной текст с помощью заранее определенной категории, отражающей смысл сообщения.

### Нейронные сети и современные виртуальные помощники

В последнее время технологическая эволюция аппаратного обеспечения, способного обрабатывать большие объемы данных и более сложные вычисления, стимулировала исследования в области искусственного интеллекта, что привело к разработке передовых алгоритмов машинного обучения, называемых нейронными сетями или алгоритмами глубокого обучения.

Нейронные сети (и, в частности, рекуррентные нейронные сети – RNN) значительно улучшили обработку естественного языка, позволяя более осмысленно представлять смысл текста, оценивая контекст слова в предложении.

Это технология, которая позволила виртуальным помощникам, рожденным в первом десятилетии нового века, очень хорошо интерпретировать человеческий язык, определять потребности и выполнять действия – например, отвечать заранее заданным сценарием или потреблять Сторонний сервис.

### Сегодняшний день, Генеративный ИИ

Вот как сегодня мы пришли к генеративному искусственному интеллекту, который можно рассматривать как разновидность глубокого обучения.

![AI, ML, DL and Generative AI](./images/AI-diagram.png?WT.mc_id=academic-105485-koreyst)

После десятилетий исследований в области искусственного интеллекта новая архитектура модели, названная *Transformer*, преодолела ограничения RNN и смогла получать на вход гораздо более длинные последовательности текста. Трансформаторы основаны на механизме внимания, позволяющем модели придавать разные веса входным данным, которые она получает, «уделяя больше внимания» тем местам, где сосредоточена наиболее релевантная информация, независимо от их порядка в текстовой последовательности.

Большинство последних генеративных моделей ИИ, также известных как большие языковые модели (БЯМ, LLM), поскольку они работают с текстовыми вводами и выводами, действительно основаны на этой архитектуре. Что интересно в этих моделях, обученных на огромном количестве неразмеченных данных из различных источников, таких как книги, статьи и веб-сайты, так это то, что их можно адаптировать к широкому спектру задач и генерировать грамматически правильный текст с подобием творчества. Таким образом, они не только невероятно увеличили способность машины «понимать» вводимый текст, но и позволили ей генерировать оригинальный ответ на человеческом языке.

## Как работают большие языковые модели?

В следующей главе мы собираемся изучить различные типы моделей генеративного ИИ, а пока давайте посмотрим, как работают большие языковые модели, уделив особое внимание моделям OpenAI GPT (генеративный предварительно обученный преобразователь(трансформер)).

* **Tokenizer, text to numbers**: Large Language Models receive a text as input and generate a text as output. However, being statistical models, they work much better with numbers than text sequences. That’s why every input to the model is processed by a tokenizer, before being used by the core model. A token is a chunk of text – consisting of a variable number of characters, so the tokenizer's main task is splitting the input into an array of tokens. Then, each token is mapped with a token index, which is the integer encoding of the original text chunk.

![Example of tokenization](./images/tokenizer-example.png?WT.mc_id=academic-105485-koreyst)

* **Predicting output tokens**: Given n tokens as input (with max n varying from one model to another), the model is able to predict one token as output. This token is then incorporated into the input of the next iteration, in an expanding window pattern, enabling a better user experience of getting one (or multiple) sentence as an answer. This explains why, if you ever played with ChatGPT, you might have noticed that sometimes it looks like it stops in the middle of a sentence.

* **Selection process, probability distribution**: The output token is chosen by the model according to its probability of occurring after the current text sequence. This is because the model predicts a probability distribution over all possible ‘next tokens’, calculated based on its training. However, not always the token with the highest probability is chosen from the resulting distribution. A degree of randomness is added to this choice, in a way that the model acts in a non-deterministic fashion - we do not get the exact same output for the same input. This degree of randomness is added to simulate the process of creative thinking and it can be tuned using a model parameter called temperature.

## How can our startup leverage Large Language Models?

Now that we have a better understanding of the inner working of a large language model, let’s see some practical examples of the most common tasks they can perform pretty well, with an eye to our business scenario.
We said that the main capability of a Large Language Model is *generating a text from scratch, starting from a textual input, written in natural language*.

But what kind of textual input and output?
The input of a large language model is known as prompt, while the output is known as completion, term that refers to the model mechanism of generating the next token to complete the current input. We are going to dive deep into what is a prompt and how to design it in a way to get the most out of our model. But for now, let’s just say that a prompt may include:

* An **instruction** specifying the type of output we expect from the model. This instruction sometimes might embed some examples or some additional data.

    1. Summarization of an article, book, product reviews and more, along with extraction of insights from unstructured data.
    
    ![Example of summarization](./images/summarization-example.png?WT.mc_id=academic-105485-koreyst)

    <br>
    
    2. Creative ideation and design of an article, an essay, an assignment or more.
    
    ![Example of creative writing](./images/creative-writing-example.png?WT.mc_id=academic-105485-koreyst)

    <br>
    
* A **question**, asked in the form of a conversation with an agent.
  
![Example of conversation](./images/conversation-example.png?WT.mc_id=academic-105485-koreyst)

<br>

* A chunk of **text to complete**, which implicitly is an ask for writing assistance.
   
![Example of text completion](./images/text-completion-example.png?WT.mc_id=academic-105485-koreyst)

<br>

* A chunk of **code** together with the ask of explaining and documenting it, or a comment asking to generate a piece of code performing a specific task.

![Coding example](./images/coding-example.png?WT.mc_id=academic-105485-koreyst)

<br>

The examples above are quite simple and don’t want to be an exhaustive demonstration of Large Language Models capabilities. They just want to show the potential of using generative AI, in particular but not limited to educational context.

Also, the output of a generative AI model is not perfect and sometimes the creativity of the model can work against it, resulting in an output which is a combination of words that the human user can interpret as a mystification of reality, or it can be offensive. Generative AI is not intelligent - at least in the more comprehensive definition of intelligence, including critical and creative reasoning or emotional intelligence; it is not deterministic, and it is not trustworthy, since fabrications, such as erroneous references, content, and statements, may be combined with correct information, and presented in a persuasive and confident manner. In the following lessons, we’ll be dealing with all these limitations and we’ll see what we can do to mitigate them.

## Assignment

Your assignment is to read up more on [generative AI](https://en.wikipedia.org/wiki/Generative_artificial_intelligence?WT.mc_id=academic-105485-koreyst) and try to identify an area where you would add generative AI today that doesn't have it. How would the impact be different from doing it the "old way", can you do something you couldn't before, or are you faster? Write a 300 word summary on what your dream AI startup would look like and include headers like "Problem", "How I would use AI", "Impact" and optionally a business plan. 

If you did this task, you might even be ready to apply to Microsoft's incubator, [Microsoft for Startups Founders Hub](https://www.microsoft.com/startups?WT.mc_id=academic-105485-koreyst) we offer credits for both Azure, OpenAI, mentoring and much more, check it out!

## Knowledge check

What's true about large language models?

1. You get the exact same response every time.
1. It does things perfectly, great at adding numbers, produce working code etc.
1. The response may vary despite using the same prompt. It's also great at giving you a first draft of something, be it text or code. But you need to improve on the results.

A: 3, an LLM is non-deterministic, the response vary, however, you can control its variance via a temperature setting. You also shouldn't expect it to do things perfectly, it's here to do the heavy-lifting for you which often means you get a good first attempt at something that you need to gradually improve.

## Great Work! Continue the Journey 

After completing this lesson, check out our [Generative AI Learning collection](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) to continue leveling up your Generative AI knowledge!

Head over to Lesson 2 where we will look at how to [explore and compare different LLM types](../02-exploring-and-comparing-different-llms/README.md?WT.mc_id=academic-105485-koreyst)!
