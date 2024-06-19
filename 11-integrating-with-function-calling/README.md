# Интеграция с вызовом функций

![изображение урока](./images/11-lesson-banner.png?WT.mc_id=academic-105485-koreyst)

Вы усвоили немало информации в предыдущих уроках. Однако мы можем продолжить совершенствоваться. Некоторые вещи, с которыми мы можем справиться, - это получение более однородного формата ответа, чтобы упростить работу с ответом на следующих этапах. Кроме того, мы можем добавить данные из других источников, чтобы дополнить наше приложение.

Проблемы, упомянутые выше, и являются темой данной главы.

> **Видео скоро будет**

## Введение

В этом уроке будет рассмотрено:

- Объяснение, что такое вызов функции и в каких случаях он используется.
- Создание вызова функции с использованием Azure OpenAI.
- Как интегрировать вызов функции в приложение.

## Цели обучения

После завершения этого урока вы сможете:

- Объяснить цель использования вызова функции.
- Настроить вызов функции с использованием сервиса Azure OpenAI.
- Разработать эффективные вызовы функций для вашего приложения.

## Сценарий: улучшение нашего чатбота с помощью функций

В этом уроке мы хотим создать функцию для нашего стартапа в сфере образования, которая позволит пользователям использовать чатбота для поиска технических курсов. Мы будем рекомендовать курсы, соответствующие их уровню навыков, текущей роли и интересующей технологии.

Для выполнения этого сценария мы будем использовать комбинацию следующих инструментов:

- `Azure OpenAI` для создания чат-опыта для пользователя.
- `API-каталог Microsoft Learn` для помощи пользователям в поиске курсов на основе их запросов.
- `Вызов функции` для получения запроса пользователя и отправки его в функцию для выполнения запроса к API.

Давайте вначале рассмотрим, почему мы хотим использовать вызов функции:

## Почему вызов функции

До появления вызова функции ответы от LLM были неструктурированными и несогласованными. Разработчикам требовалось писать сложный код проверки, чтобы обрабатывать каждую вариацию ответа. Пользователи не могли получить ответы на вопросы вроде "Какая текущая погода в Стокгольме?". Это связано с тем, что модели ограничены данными, на которых было проведено обучение.

Вызов функции - это функциональность сервиса Azure OpenAI, которая позволяет преодолеть следующие ограничения:

- **Однородный формат ответа**. Если мы можем лучше контролировать формат ответа, мы сможем более легко интегрировать его с другими системами.
- **Внешние данные**. Возможность использовать данные из других источников в контексте чата приложения.

## Иллюстрирование проблемы через сценарий

> Мы рекомендуем вам использовать [блокнот](/11-integrating-with-function-calling/Lesson11-FunctionCalling.ipynb) Если вы хотите выполнить приведенный ниже сценарий, вы также можете просто читать его, поскольку мы пытаемся проиллюстрировать проблему, в которой функции могут помочь справиться с проблемой.

Давайте рассмотрим пример, иллюстрирующий проблему формата ответа:

Предположим, мы хотим создать базу данных с данными о студентах, чтобы мы могли предложить им подходящий курс. Ниже приведены два описания студентов, которые очень похожи по содержанию данных.

1. Установите соединение с нашим ресурсом Azure OpenAI:

   ```python
   import os
   import json
   from openai import AzureOpenAI
   from dotenv import load_dotenv
   load_dotenv()

   client = AzureOpenAI(
   api_key=os.environ['AZURE_OPENAI_KEY'],  # это также является значением по умолчанию и может быть опущено
   api_version = "2023-07-01-preview"
   )

   deployment=os.environ['AZURE_OPENAI_DEPLOYMENT']
   ```

   Ниже приведен некоторый код на языке Python для настройки соединения с Azure OpenAI, где мы устанавливаем значения `api_type`, `api_base`, `api_version` и `api_key`.

2. Создание двух описаний студентов с использованием переменных `student_1_description` и `student_2_description`.

   ```python
   student_1_description="Эмили Джонсон - второкурсница, обучающаяся по специальности компьютерные науки в Дюкском университете. У нее средний балл 3.7. Эмили активно участвует в шахматном клубе и дебатном клубе университета. Она надеется сделать карьеру в области программной инженерии после окончания учебы."

   student_2_description = "Майкл Ли - второкурсник, обучающийся по специальности компьютерные науки в Стэнфордском университете. У него средний балл 3.8. Майкл известен своими навыками программирования и является активным членом робототехнического клуба университета. Он надеется сделать карьеру в области искусственного интеллекта после окончания учебы."
   ```

   Мы хотим отправить указанные выше описания студентов на обработку LLM для анализа данных. Эти данные могут быть использованы в нашем приложении и отправлены в API или сохранены в базе данных.

3. Создадим два идентичных запроса, в которых мы указываем LLM, какую информацию мы интересуемся:

   ```python
   prompt1 = f'''
   Пожалуйста, извлеките следующую информацию из данного текста и верните ее в виде JSON-объекта:

   имя
   специальность
   университет
   оценки
   клуб

   Это текст, из которого нужно извлечь информацию:
   {student_1_description}
   '''

   prompt2 = f'''
   Пожалуйста, извлеките следующую информацию из данного текста и верните ее в виде JSON-объекта:

   имя
   специальность
   университет
   оценки
   клуб

   Это текст, из которого нужно извлечь информацию:
   {student_2_description}
   '''
   ```

   В указанных выше запросах мы указываем LLM извлекать информацию и возвращать результат в формате JSON.
   
4. После настройки запросов и соединения с Azure OpenAI мы отправим запросы на обработку LLM с помощью `openai.ChatCompletion`. Мы сохраняем запрос в переменной `messages` и присваиваем роль `user`. Это сделано для имитации сообщения от пользователя, написанного чат-боту.

   ```python
   # Ответ на первый запрос
   openai_response1 = client.chat.completions.create(
   model=deployment,
   messages=[{'role': 'user', 'content': prompt1}]
   )
   openai_response1.choices[0].message.content

   # Ответ на второй запрос
   openai_response2 = client.chat.completions.create(
   model=deployment,
   messages=[{'role': 'user', 'content': prompt2}]
   )
   openai_response2.choices[0].message.content
   ```

   Теперь мы можем отправить оба запроса LLM и изучить полученный ответ, найдя его таким образом `openai_response1['choices'][0]['message']['content']`.

5. Наконец, мы можем преобразовать ответ в формат JSON, вызвав `json.loads`:

   ```python
   # Загрузка ответа в виде JSON-объекта
   json_response1 = json.loads(openai_response1.choices[0].message.content)
   json_response1
   ```

   Ответ 1:

   ```json
   { "name": "Emily Johnson", "major": "компьютерные науки", "school": "Дюкский университет", "grades": "3.7", "club": "Шахматный клуб" }
   ```

   Ответ 2:

   ```json
   { "name": "Michael Lee", "major": "компьютерные науки", "school": "Стэнфордский университет", "grades": "3.8 GPA", "club": "Робототехнический клуб" }
   ```

   Несмотря на то, что запросы одинаковые, а описания похожи, мы видим, что значения свойства `grades` отформатированы по-разному, например, может быть формат `3.7` или `3.7 GPA`.

   Это происходит потому, что LLM принимает неструктурированные данные в виде написанного запроса и также возвращает неструктурированные данные. Нам нужно иметь структурированный формат, чтобы знать, что ожидать при сохранении или использовании этих данных.

Как же мы решаем проблему форматирования? Используя функциональный вызов, мы можем убедиться, что получаем структурированные данные. При использовании функционального вызова LLM фактически не вызывает или выполняет какие-либо функции. Вместо этого мы создаем структуру, которую LLM должен следовать в своих ответах. Затем мы используем эти структурированные ответы, чтобы знать, какую функцию запускать в наших приложениях.

![поток функций](./images/Function-Flow.png?WT.mc_id=academic-105485-koreyst)

Затем мы можем взять то, что возвращает функция, и отправить это обратно в LLM. LLM затем отвечает, используя естественный язык, чтобы ответить на запрос пользователя.

## Примеры использования функционального вызова

Существует множество различных случаев использования, в которых функциональные вызовы могут улучшить ваше приложение, такие как:

- **Вызов внешних инструментов**. Чат-боты отлично подходят для предоставления ответов на вопросы пользователей. Используя функциональный вызов, чат-боты могут использовать сообщения от пользователей для выполнения определенных задач. Например, студент может попросить чат-бота "Отправить электронное письмо моему преподавателю, сказав, что мне нужна дополнительная помощь по этому предмету". Это может вызвать функцию `send_email(to: string, body: string)` для отправки электронного письма.

- **Создание запросов к API или базе данных**. Пользователи могут искать информацию, используя естественный язык, который преобразуется в форматированный запрос или запрос к API. Примером может быть запрос учителя "Кто из студентов сдал последнее задание", который может вызвать функцию с названием `get_completed(student_name: string, assignment: int, current_status: string)`.

- **Создание структурированных данных**. Пользователи могут взять блок текста или CSV и использовать LLM для извлечения важной информации из него. Например, студент может преобразовать статью из Википедии о соглашениях о мире, чтобы создать карточки с вопросами и ответами для обучения искусственного интеллекта. Это можно сделать с помощью функции под названием `get_important_facts(agreement_name: string, date_signed: string, parties_involved: list)`.

## Создание вашего первого функционального вызова

Процесс создания функционального вызова включает 3 основных шага:

1. **Вызов** API Chat Completions с указанием списка ваших функций и сообщения пользователя.
2. **Чтение** ответа модели для выполнения действия, например, выполнение функции или вызов API.
3. **Создание** еще одного вызова к API Chat Completions с ответом от вашей функции для использования этой информации и создания ответа пользователю.

![LLM Поток](./images/LLM-Flow.png?WT.mc_id=academic-105485-koreyst)

### Шаг 1 - создание сообщений

Первый шаг - создать сообщение пользователя. Его можно динамически присвоить, взяв значение из текстового поля, либо можно присвоить значение здесь. Если вы впервые работаете с API Chat Completions, нам необходимо определить `роль` и `содержание` сообщения.

`Роль` может быть `system` (создание правил), `assistant` (модель) или `user` (конечный пользователь). Для функционального вызова мы присваиваем роль `user` и задаем пример вопроса.

```python
messages = [{"role": "user", "content": "Найдите мне хороший курс для начинающего студента по изучению Azure."}]
```

Различные роли помогают LLM понять, говорит ли что-то система или пользователь, что помогает строить историю разговора, на которой LLM может основываться.

### Шаг 2 - создание функций

Затем мы определим функцию и параметры этой функции. Здесь мы будем использовать только одну функцию с именем `search_courses`, но вы можете создать несколько функций.

> **Важно**: Функции включаются в системное сообщение для LLM и будут включены в количество доступных токенов.
Below, we create the functions as an array of items. Each item is a function and has properties `name`, `description` and `parameters`:

```python
functions = [
   {
      "name": "search_courses",
      "description": "Извлекает курсы из индекса поиска на основе предоставленных параметров",
      "parameters": {
         "type": "object",
         "properties": {
            "role": {
               "type": "string",
               "description": "Роль учащегося (например, разработчик, специалист по обработке данных, студент и т. д.)"
            },
            "product": {
               "type": "string",
               "description": "Продукт, который охватывает урок (например, Azure, Power BI и т. д.)"
            },
            "level": {
               "type": "string",
               "description": "Уровень опыта учащегося перед прохождением курса (например, начинающий, средний, продвинутый)"
            }
         },
         "required": [
            "role"
         ]
      }
   }
]
```

Давайте подробнее опишем каждый экземпляр функции ниже:

- `name` - Название функции, которую мы хотим вызвать.
- `description` - Это описание того, как функция работает. Здесь важно быть конкретным и ясным.
- `parameters` - Список значений и формата, которые вы хотите, чтобы модель использовала в своем ответе. Массив параметров состоит из элементов, у которых есть следующие свойства:
  1. `type` - Тип данных, в котором будут храниться свойства.
  2. `properties` - Список конкретных значений, которые модель будет использовать в своем ответе.
     1. `name` - Ключ - это имя свойства, которое модель будет использовать в своем отформатированном ответе, например, `product`.
     2. `type` - Тип данных этого свойства, например, `string`.
     3. `description` - Описание конкретного свойства.

Также есть необязательное свойство `required` - обязательное свойство для завершения функционального вызова.

### Шаг 3 - Выполнение функционального вызова

После определения функции мы теперь должны включить ее в вызов API Chat Completions. Мы делаем это, добавляя `functions` в запрос. В данном случае `functions=functions`.

Также есть возможность установить `function_call` в значение `auto`. Это означает, что мы позволим LLM самостоятельно решить, какую функцию вызвать на основе сообщения пользователя, а не назначать ее сами.

Вот пример кода, в котором мы вызываем `ChatCompletion.create`. Обратите внимание, как мы устанавливаем `functions=functions` и `function_call="auto"`, предоставляя LLM возможность самому решить, когда вызывать функции, которые мы предоставляем:

```python
response = client.chat.completions.create(model=deployment,
                                        messages=messages,
                                        functions=functions,
                                        function_call="auto")

print(response.choices[0].message)
```

Ответ, который мы получаем, выглядит следующим образом:

```json
{
  "role": "assistant",
  "function_call": {
    "name": "search_courses",
    "arguments": "{\n  \"role\": \"student\",\n  \"product\": \"Azure\",\n  \"level\": \"beginner\"\n}"
  }
}
```

Here we can see how the function `search_courses` was called and with what arguments, as listed in the `arguments` property in the JSON response.

The conclusion the LLM was able to find the data to fit the arguments of the function as it was extracting it from the value provided to the `messages` parameter in the chat completion call. Below is a reminder of the `messages` value:

```python
messages= [ {"role": "user", "content": "Find me a good course for a beginner student to learn Azure."} ]
```

As you can see, `student`, `Azure` and `beginner` was extracted from `messages` and set as input to the function. Using functions this way is a great way to extract information from a prompt but also to provide structure to the LLM and have reusable functionality.

Next, we need to see how we can use this in our app.

## Integrating Function Calls into an Application

After we have tested the formatted response from the LLM, now we can integrate this into an application.

### Managing the flow

To integrate this into our application, let's take the following steps:

1. First, let's make the call to the Open AI services and store the message in a variable called `response_message`.

   ```python
   response_message = response.choices[0].message
   ```

1. Now we will define the function that will call the Microsoft Learn API to get a list of courses:

   ```python
   import requests

   def search_courses(role, product, level):
     url = "https://learn.microsoft.com/api/catalog/"
     params = {
        "role": role,
        "product": product,
        "level": level
     }
     response = requests.get(url, params=params)
     modules = response.json()["modules"]
     results = []
     for module in modules[:5]:
        title = module["title"]
        url = module["url"]
        results.append({"title": title, "url": url})
     return str(results)
   ```

   Note how we now create an actual Python function that maps to the function names introduced in the `functions` variable. We're also making real external API calls to fetch the data we need. In this case, we go against the Microsoft Learn API to search for training modules.

Ok, so we created `functions` variables and a corresponding Python function, how do we tell the LLM how to map these two together so our Python function is called?

1. To see if we need to call a Python function, we need to look into the LLM response and see if `function_call` is part of it and call the pointed out function. Here's how you can make the mentioned check below:

   ```python
   # Check if the model wants to call a function
   if response_message.function_call.name:
    print("Recommended Function call:")
    print(response_message.function_call.name)
    print()

    # Call the function.
    function_name = response_message.function_call.name

    available_functions = {
            "search_courses": search_courses,
    }
    function_to_call = available_functions[function_name]

    function_args = json.loads(response_message.function_call.arguments)
    function_response = function_to_call(**function_args)

    print("Output of function call:")
    print(function_response)
    print(type(function_response))


    # Add the assistant response and function response to the messages
    messages.append( # adding assistant response to messages
        {
            "role": response_message.role,
            "function_call": {
                "name": function_name,
                "arguments": response_message.function_call.arguments,
            },
            "content": None
        }
    )
    messages.append( # adding function response to messages
        {
            "role": "function",
            "name": function_name,
            "content":function_response,
        }
    )
   ```

   These three lines, ensure we extract the function name, the arguments and make the call:

   ```python
   function_to_call = available_functions[function_name]

   function_args = json.loads(response_message.function_call.arguments)
   function_response = function_to_call(**function_args)
   ```

   Below is the output from running our code:

   **Output**

   ```Recommended Function call:
   {
     "name": "search_courses",
     "arguments": "{\n  \"role\": \"student\",\n  \"product\": \"Azure\",\n  \"level\": \"beginner\"\n}"
   }

   Output of function call:
   [{'title': 'Describe concepts of cryptography', 'url': 'https://learn.microsoft.com/training/modules/describe-concepts-of-cryptography/?
   WT.mc_id=api_CatalogApi'}, {'title': 'Introduction to audio classification with TensorFlow', 'url': 'https://learn.microsoft.com/en-
   us/training/modules/intro-audio-classification-tensorflow/?WT.mc_id=api_CatalogApi'}, {'title': 'Design a Performant Data Model in Azure SQL
   Database with Azure Data Studio', 'url': 'https://learn.microsoft.com/training/modules/design-a-data-model-with-ads/?
   WT.mc_id=api_CatalogApi'}, {'title': 'Getting started with the Microsoft Cloud Adoption Framework for Azure', 'url':
   'https://learn.microsoft.com/training/modules/cloud-adoption-framework-getting-started/?WT.mc_id=api_CatalogApi'}, {'title': 'Set up the
   Rust development environment', 'url': 'https://learn.microsoft.com/training/modules/rust-set-up-environment/?WT.mc_id=api_CatalogApi'}]
   <class 'str'>
   ```

1. Now we will send the updated message, `messages` to the LLM so we can receive a natural language response instead of an API JSON formatted response.

   ```python
   print("Messages in next request:")
   print(messages)
   print()

   second_response = client.chat.completions.create(
      messages=messages,
      model=deployment,
      function_call="auto",
      functions=functions,
      temperature=0
         )  # get a new response from GPT where it can see the function response


   print(second_response.choices[0].message)
   ```

   **Output**

   ```python
   {
     "role": "assistant",
     "content": "I found some good courses for beginner students to learn Azure:\n\n1. [Describe concepts of cryptography] (https://learn.microsoft.com/training/modules/describe-concepts-of-cryptography/?WT.mc_id=api_CatalogApi)\n2. [Introduction to audio classification with TensorFlow](https://learn.microsoft.com/training/modules/intro-audio-classification-tensorflow/?WT.mc_id=api_CatalogApi)\n3. [Design a Performant Data Model in Azure SQL Database with Azure Data Studio](https://learn.microsoft.com/training/modules/design-a-data-model-with-ads/?WT.mc_id=api_CatalogApi)\n4. [Getting started with the Microsoft Cloud Adoption Framework for Azure](https://learn.microsoft.com/training/modules/cloud-adoption-framework-getting-started/?WT.mc_id=api_CatalogApi)\n5. [Set up the Rust development environment](https://learn.microsoft.com/training/modules/rust-set-up-environment/?WT.mc_id=api_CatalogApi)\n\nYou can click on the links to access the courses."
   }

   ```

## Assignment

To continue your learning of Azure OpenAI Function Calling you can build:

- More parameters of the function that might help learners find more courses.
- Create another function call that takes more information from the learner like their native language
- Create error handling when the function call and/or API call does not return any suitable courses

Hint: Follow the [Learn API reference documentation](https://learn.microsoft.com/training/support/catalog-api-developer-reference?WT.mc_id=academic-105485-koreyst) page to see how and where this data is available.

## Great Work! Continue the Journey

After completing this lesson, check out our [Generative AI Learning collection](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) to continue leveling up your Generative AI knowledge!

Head over to Lesson 12 where we will look at how to [design UX for AI applications](../12-designing-ux-for-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)!
