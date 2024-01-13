# Домашнее задание к занятию 1. «Введение в виртуализацию»
# `Островский Евгений`


### Цели задания
1. Научиться запускать виртуальную машину в Yandex Cloud с минимальным расходом ресурсов.
2. Попрактиковаться в выборе платформы  и системы управления виртуализации для решения требуемых задач.

### Инструкция к выполению

1. Для выполнения задачи 1 ознакомьтесь с [инструкцией](https://github.com/netology-code/devops-materials/blob/master/cloudwork.MD) по экономии облачных ресурсов и затем выполните задачу 1 по шагам.
2. Своё решение к задачам 2,3,4 загрузите в ваш ЛК.
   
## Задача 1

Ознакомьтесь с [инструкцией ](https://github.com/netology-code/devops-materials/blob/master/cloudwork.MD) по экономии облачных ресурсов.


1. Создайте через web-интерфейс Yandex Cloud - VPC и виртуальную машину из инструкции конфигурации "эконом-ВМ" с публичным ip-адресом. В пункте "Выбор образа/загрузочного диска" выберите вкладку "Cloud Marketplace" , щелкните "Посмотреть больше", найдите образ "Yandex Cloud Toolbox".
2. Убедитесь, что вы можете подключиться к консоли ВМ через ssh, используя публичный ip-адрес. Убедитесь, что на ВМ установлен Docker с помощью команды ```docker --version```(команду выполните от имени root пользователя) !
3. Узнайте в инструкции Яндекс, какие еще инструменты предустановлены в данном образе.
4. Оставьте ВМ работать, пока она не выключится самостоятельно! Опция "прерываемая" выключит ее не позже чем через 24 часа. 
5. Для наглядности подождите еще 1 сутки.
6. Перейдите по [ссылке ](https://console.cloud.yandex.ru/billing?section=accounts). Выберите свой платежный аккаунт. Перейдите на вкладку детализация (фильтр "По продуктам") и оцените график потребления финансов.
7. Удалите ВМ или пользуйтесь ею при выполнении последующих домашних заданий курса обучения.

---


## Задача 2

Выберите один из вариантов платформы в зависимости от задачи. Здесь нет однозначно верного ответа так как все зависит от конкретных условий: финансирование, компетенции специалистов, удобство использования, надежность, требования ИБ и законодательства, фазы луны.

Тип платформы:

- физические сервера;
- паравиртуализация (по лекции - Prallels, VirtualBox, Proxmox, KVM);
- виртуализация уровня ОС (Docker, Podman, LXT);

Объясните критерии выбора платформы в каждом случае.

### Ответ
Задачи:

- высоконагруженная база данных MySql, критичная к отказу;

Можно пойти от обратного - паравиртуализация не подойдет, так как получаем расход ресурсов на обслуживание виртуализации и лушче их потратить на работу БД. Виртуализация уровня ОС - наобходимо рассматривать конкретную ситуацию, есть плюсы, но будет необходимо решать ряд вопросов. Больше подойдет **физический сервер** и репликации для обеспечения отказоустойчивости.

- различные web-приложения;

Тут хорошо подходит **виртуализация уровня ОС** - так как позволяет хорошо масштабироваться и реагировать на нагрузку. Из плюсов виртуализации в такой ситуации можно отметить - возможность быстро развернуть или перенести наше приложение - как вариант отказоустойчивости.

- Windows-системы для использования бухгалтерским отделом;

Для работы с Windows системами отличным вариантом будет Hyper-V - **паравиртуализация**. Можно будет делать копии или снепшоты для возможности быстро вернутся или восстановиться - что обеспечит безопасность важных данных.

- системы, выполняющие высокопроизводительные расчёты на GPU.

Нужно брать конкретный случай, если например рассматривать NVIDIA - предлагает свои контейнеры NGC, с оптимизированными версиями различного софта, библиотек и драйверов. Оверхед на использования контейнера около 3%. - Это **виртуализация уровня ОС** - можно считать отличным вариантом, так как позволит проще и эффективнее распределять ресурсы.

## Задача 3

Выберите подходящую систему управления виртуализацией для предложенного сценария. Опишите ваш выбор.

Сценарии:

- 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based-инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.

Для Windows инфраструктуры подойдет Hyper-V, но можно рассмотреть как вариант и решения от VMware. Оба решения обладают вариантами резервного копирования, репликацией (vSpare Replication, Hyper-V Replica) и реализацией балансировщиков нагрузки.

- Требуется наиболее производительное бесплатное open source-решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.

Можно рассмотреть вариант с Porxmox или Xen - бесплатные, есть все стандартные решения для работы с виртуальными машинами. Пишут про возможные проблемы с Windows системами на обоих платформах - поэтому придется брать конкретные случаи и тестировать.

- Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows-инфраструктуры.

Hyper-V Server - это бесплатный продукт с возможностями виртуализации максимально подходящий для Windows.

- Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

 Тут лучше рассмотреть варинты с контейнерами - это Docker или LXD - можно быстро создавать, уничтожать необходимые тестовые среды со всеми возможными вариантами дистрибутивов.

## Задача 4

Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, создавали бы вы гетерогенную среду или нет?

Основная проблема гетерогенной среды - разные технологии - требуют разный подход, а следовательно и больше знаний/специалистов - средств.

Для решения этих проблем необходимо понять что мы делаем с системой. В общем и целом можно на более верхнем уровне стремиться к однородности системы - и следовательно более стандарным возможностям ее обслуживать. Всегда есть подход IaC и при постоянно меняющейся системе можно двигаться в сторону стандартизации.

Я думаю все зависит от задачи. Например при работе и с Windows и с Linux системами необходимо сравнивать производительность и принимать решение исходя из полученных данных и минимилизации затрат. 


### Правила приема

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.
