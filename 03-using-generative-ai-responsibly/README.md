# Ответственное использование генеративного ИИ (принципы Responsible AI)

[![Ответственное использование генеративного ИИ](./images/03-lesson-banner.png?WT.mc_id=academic-105485-koreyst)]() 

> **Видео скоро появится**

Легко увлечься искусственным интеллектом и, в частности, генеративным искусственным интеллектом, но вам нужно подумать о том, как вы будете использовать его ответственно. Вам необходимо подумать о том, как обеспечить честность, безвредность результатов и многое другое. Цель этой главы — предоставить вам упомянутый контекст, узнать, что следует учитывать и как предпринять активные шаги для улучшения использования ИИ.

## Введение

В этом уроке будут рассмотрены:

- Почему вам следует использовать Responsible AI при создании приложений генеративного ИИ.
- Основные принципы Responsible AI и их отношение к генеративному ИИ.
- Как реализовать принципы Responsible AI на практике с помощью стратегии и инструментов.

## Цели обучения

Пройдя этот урок, вы будете знать:

- Важность Responsible AI при создании приложений генеративного ИИ.
- Когда следует подумать и применить основные принципы Responsible AI при создании приложений генеративного ИИ.
- Какие инструменты и стратегии вам доступны для реализации концепции Responsible AI на практике.

## Responsible AI принципы

Волнение от генеративного искусственного интеллекта никогда не было таким высоким. Это волнение привлекло в отрасль множество новых разработчиков, внимание и финансирование. Хотя это очень позитивно для всех, кто хочет создавать продукты и компании с использованием генеративного искусственного интеллекта, также важно, чтобы мы действовали ответственно.

На протяжении всего этого курса мы концентрируемся на создании нашего стартапа и образовательного продукта в области искусственного интеллекта. Мы будем использовать принципы Responsible AI: справедливость, инклюзивность, надежность/безопасность, безопасность и конфиденциальность, прозрачность и подотчетность. Используя эти принципы, мы исследуем, как они связаны с использованием генеративного искусственного интеллекта в наших продуктах..

## Почему вам следует отдавать приоритет ответственному ИИ

При создании продукта использование человекоориентированного подхода, учитывающего интересы пользователя, приводит к лучшим результатам.

Уникальность генеративного искусственного интеллекта заключается в его способности создавать полезные ответы, информацию, рекомендации и контент для пользователей. Это можно сделать без большого количества ручных действий, что может привести к очень впечатляющим результатам. Без надлежащего планирования и стратегии это, к сожалению, может привести к некоторым вредным последствиям для ваших пользователей, вашего продукта и общества в целом.

Давайте посмотрим на некоторые (но не на все) из этих потенциально вредных результатов:

### Галлюцинации

Галлюцинации — это термин, используемый для описания случаев, когда LLM создает контент, который либо совершенно бессмысленен, либо что-то, что, как мы знаем, фактически неверно на основании других источников информации.

Давайте, например, создадим функцию для нашего стартапа, которая позволяет студентам задавать модели исторические вопросы. Студент задает вопрос: «Кто был единственным выжившим на Титанике?»

Модель выдает ответ, подобный приведенному ниже:

![Подсказка: «Кто был единственным выжившим на Титанике?»](../03-using-generative-ai-responsibly/images/ChatGPT-titanic-survivor-prompt.webp?WT.mc_id=academic-105485-koreyst)

> *(Источник: [Flying bisons](https://flyingbisons.com?WT.mc_id=academic-105485-koreyst))*

Единственным выжившим после катастрофы «Титаника» был Чарльз Джоуин. Он был британским пекарем и главным пекарем на борту «Титаника». Джогину удалось выжить при затоплении, как сообщается, цепляясь за перевернутую спасательную шлюпку и проведя несколько часов в холодной воде, прежде чем его спасло судно RMS Carpathia. Его выживание часто связывают с чрезмерным употреблением алкоголя, который, возможно, помог ему пережить сильный холод. Джоуин дожил до 1956 года и позже предоставил свидетельства о своем опыте во время катастрофы «Титаника».

Это очень уверенный и обстоятельный ответ. К сожалению, это неверно. Даже при минимальном объеме исследований можно было бы обнаружить, что после катастрофы «Титаника» выжило несколько человек. Для студента, который только начинает исследовать эту тему, этот ответ может быть достаточно убедительным, чтобы его не подвергали сомнению и не воспринимали как факт. Последствия этого могут привести к тому, что система искусственного интеллекта станет ненадежной и негативно отразится на репутации нашего стартапа.

С каждой итерацией любого LLM мы наблюдали улучшение производительности в плане минимизации галлюцинаций. Даже несмотря на это улучшение, нам, разработчикам приложений и пользователям, по-прежнему необходимо помнить об этих ограничениях.

### Вредный контент

В предыдущем разделе мы рассмотрели случаи, когда LLM выдает неправильные или бессмысленные ответы. Еще один риск, о котором нам нужно знать, — это когда модель отвечает вредоносным контентом.

Вредный контент можно определить как:

- Предоставление инструкций или поощрение членовредительства или причинения вреда определенным группам.
- Ненавистнический или унизительный контент.
- Руководство планированием любого типа нападения или насильственных действий.
- Предоставление инструкций о том, как найти незаконный контент или совершить незаконные действия.
- Демонстрация контента откровенно сексуального характера.

Что касается нашего стартапа, мы хотим убедиться, что у нас есть правильные инструменты и стратегии, чтобы студенты не видели этот тип контента.

### Отсутствие справедливости

Справедливость определяется как «гарантия того, что система ИИ свободна от предвзятости и дискриминации и что они относятся ко всем справедливо и одинаково». В мире генеративного искусственного интеллекта мы хотим гарантировать, что исключительные мировоззрения маргинализированных групп не подкрепляются результатами модели.

Подобные результаты не только разрушительны для формирования положительного опыта использования продукта у наших пользователей, но и наносят дополнительный вред обществу. Как разработчики приложений, мы всегда должны учитывать широкую и разнообразную базу пользователей при создании решений с использованием генеративного ИИ.

## How to Use Generative AI Responsibly

Now that we have identified the importance of Responsible Generative AI, let's look at 4 steps we can take to build our AI solutions responsibly:

![Mitigate Cycle](./images/mitigate-cycle.png?WT.mc_id=academic-105485-koreyst)

### Measure Potential Harms

In software testing, we test the expected actions of a user on an application. Similarly, testing a diverse set of prompts users are most likely going to use is a good way to measure potential harm.

Since our startup is building an education product, it would be good to prepare a list of education-related prompts. This could be to cover a certain subject, historical facts, and prompts about student life.

### Mitigate Potential Harms

It is now time to find ways where we can prevent or limit the potential harm caused by the model and its responses. We can look at this in 4 different layers:

![Mitigation Layers](./images/mitigation-layers.png?WT.mc_id=academic-105485-koreyst)

- **Model**. Choosing the right model for the right use case. Larger and more complex models like GPT-4 can cause more of a risk of harmful content when applied to smaller and more specific use cases. Using your training data to fine-tune also reduces the risk of harmful content.

- **Safety System**. A safety system is a set of tools and configurations on the platform serving the model that help mitigate harm. An example of this is the content filtering system on the Azure OpenAI service. Systems should also detect jailbreak attacks and unwanted activity like requests from bots.

- **Metaprompt**. Metaprompts and grounding are ways we can direct or limit the model based on certain behaviors and information. This could be using system inputs to define certain limits of the model. In addition, providing outputs that are more relevant to the scope or domain of the system.

 It can also be using techniques like Retrieval Augmented Generation (RAG) to have the model only pull information from a selection of trusted sources. There is a lesson later in this course for [building search applications](../08-building-search-applications/README.md?WT.mc_id=academic-105485-koreyst)

- **User Experience**. The final layer is where the user interacts directly with the model through our application’s interface in some way. In this way we can design the UI/UX to limit the user on the types of inputs they can send to the model as well as text or images displayed to the user. When deploying the AI application, we also must be transparent about what our Generative AI application can and can’t do.  

We have an entire lesson dedicated to [Designing UX for AI Applications](../12-designing-ux-for-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)

- **Evaluate model**. Working with LLMs can be challenging because we don’t always have control over the data the model was trained on. Regardless, we should always evaluate the model’s performance and outputs. It’s still important to measure the model’s accuracy, similarity, groundedness, and relevance of the output. This helps provide transparency and trust to stakeholders and users.

### Operate a Responsible Generative AI solution

Building an operational practice around your AI applications is the final stage. This includes partnering with other parts of our startup like Legal and Security to ensure we are compliant with all regulatory policies. Before launching, we also want to build plans around delivery, handling incidents, and rollback to prevent any harm to our users from growing.

## Tools

While the work of developing Responsible AI solutions may seem like a lot, it is work well worth the effort. As the area of Generative AI grows, more tooling to help developers efficiently integrate responsibility into their workflows will mature. For example, the [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview?WT.mc_id=academic-105485-koreyst ) can help detect harmful content and images via an API request.

## Knowledge check

What are some things you need to care about to ensure responsible AI usage?

1. That the answer is correct.
1. Harmful usage, that AI isn't used for criminal purposes.
1. Ensuring the AI is free from bias and discrimination.

A: 2 and 3 are correct. Responsible AI helps you consider how to mitigate harmful effects and biases and more.

## 🚀 Challenge

Read up on [Azure AI Content Saftey](https://learn.microsoft.com/azure/ai-services/content-safety/overview?WT.mc_id=academic-105485-koreyst) and see what you can adopt for your usage.

## Great Work, Continue Your Learning

After completing this lesson, check out our [Generative AI Learning collection](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) to continue leveling up your Generative AI knowledge!

Head over to Lesson 4 where we will look at [Prompt Engineering Fundamentals](../04-prompt-engineering-fundamentals/README.md?WT.mc_id=academic-105485-koreyst)!
