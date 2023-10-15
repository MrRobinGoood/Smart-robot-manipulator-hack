# Кейс МФТИ и Центра Робототехники Сбера "Помоги роботу навести порядок"!

## Как мы решали задачу:

Перед нами была поставлена задача по разработке LLM модели с возможностью распознавания объектов с изображений робота-помощника.

Наша концепция решения задачи следующая:

- Стартовое изображение робота попадает в модель MiniGPT-4, модель определяет положение руки робота, а также формирует текстовую информацию об окружении робота, указывает есть ли предметы в руке робота.
- В случае если у робота есть предмет в руке, или его рука неходится не в исходном положении, информация сохраняется и передаётся на следующий этап обработки.
- Задача, поставленная пользователем на естественном языке попадает в модель llama-2-chat-hf, а также в неё доставляется обработанная информация из MiniGPT-4.
- С помощью специального промпта модель понимает поставленную задачу и генерирует алгоритм действия робота в формате json.

### Нюансы работы:

Для того чтобы LLM модель могла корректно формировать алгоритм действий робота, согласно правилам установленным центром робототехники модель необходимо дообучить(finetuning) на [специальном датасете](), полученном в качестве материалов для хакатона.

Для того чтобы модель MiniGPT-4 могла распознавать объекты в механической руке робота, необходимо сделать finetuning данной модели, с помощью специально созданного нами [датасета]().

### В процессе разработки мы также попробовали модели:
- FORMAGe
- Saiga2
- Yolo
- Vicuna

Yolo продемонстрировала достойные результаты, однако мы не успели её адаптировать под нашу задачу, т.к требуется более обширное её дообучение.

FORMAGe не оправдало себя, качество распознавания объектов не достаточное для нашей задачи.

Saiga2 рассматривалась нами как русскоязычная версия для LLM модели, однако не потребовалось её задействовать из-за требований кейсодателей. 

### Работа

- Мы успешно запустили и протестировали MiniGPT-4, сразу поняли, что её нужно тюнить. Попробовали затюнить(тюнинг это второй этап обучения модели, для тюнинга нам необходимы веса первого тяжёлого этапа обучения модели) её версию с llama2 под капотом, однако не оказалось файла с весами первого этапа обучения в открытом доступе в сети. Поэтому мы переставили внутреннюю модель на Vicun_V0. Нами был создан свой собственный [датасет]() для обучения.
- Также мы провели тюнинг модели llama-2-chat-hf, на основании датасета данного нам кейсодателями.
- Также нами была запущена модель Yolo, с помощью которой мы протестировали распознавание объектов в реальном времени на видео, в дальнейшем её можно дообучать на необходимых объектах для распознавания.
