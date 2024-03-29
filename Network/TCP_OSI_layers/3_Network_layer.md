# Сетевой уровень
Сетевой уровень является основой интернета и предназначен для объединения сети с построением на основе разных технологий:
+ Ethernet
+ Wi-Fi
+ 5G/4G/3G
+ ...
Так как все эти технологии различаются во многих аспектах, например таких как: Сервисы(С гарантией доставки, Без гарантии доставки), Адресация(Разный размер, разные идентификаторы), Широковещание(Есть или нет),  Размер кадра(1500 или 2304) итд, был придуман сетевой уровень, он **согласует различия в сетях**.

Также сетевой уровень предлагает **масштабируемость**, за счёт:
+ Агрегации адресов - работа не с отдельными адресами, а с блоками адресов(сеть)
+ Запрет пересылки мусорных пакетов - пакет отбрасывается, если нельзя определить, куда нужно его отправить
+ Возможность наличия нескольких путей в сети - маршрутизация

**Итог - задачами сетевого уровня является:**
+ Объединение сетей
+ Маршрутизация
+ Обеспечение качества обслуживания

**Оборудованием сетевого уровня являются _маршрутизаторы_**
Маршрутизатор - это устройство для объединения сетей, у которого есть несколько интерфейсов к которым подключаются сети. У каждого интерфейса есть адрес.
![Маршрутизация](https://zvondozvon.ru/wp-content/uploads/2020/02/variant-deistv-mars.jpg)

**Что такое маршрутизация?**
Маршрутизация(routing)- это поиск маршрута доставки пакета между сетями через транзитные узлы - маршрутизаторы. Сложность маршрутизации заключается в учете изменений в топологии сети, и в учете загрузки каналов связи и маршрутизаторов.

**Протоколы сетевого уровня:**
+ IP(Internet Protocol) - используется для передачи данных  
+ ICMP(Internet Count Message Protocol) - используется для управления сетью
+ ARP(Address Resolution Protocol) - используется для того чтобы по глобальному адресу сетевого уровня определить адрес канального уровня
+ DHCP(Dynamic Host Configuration Protocol) - используется для того чтобы автоматически назначать IP адреса в составной сети

## IP-адреса
IP-адреса - глобальные адреса в стеке протоколов TCP/IP, используются для уникальной идентификации компьютеров в составной сети.
В сетях используется два типа адресов: 
+ Локальные - используются на канальном уровне
+ + Адреса в технологии канального уровня: MAC или IMEI
+ + Привязаны к конкретной технологии
+ Глобальные - используются на сетевом уровне 
+ + Адреса сетевого уровня: IP-адреса
+ + Не привязаны к технологии
+ + Применяются при объединении сетей 

_Подсеть_ - это множество компьютеров, у которых старшая часть IP-адреса одинаковая, например:
+ 213.***.***.***
+ 213.***.***.***
+ итд...
Маршрутизаторы работают с подсетями, а не с отдельными компьютерами.

**Структура IP адреса:**
+ Номер подсети - старшие биты
+ Номер хоста - младшие биты

**Маска подсети** - показывает, где в IP-адресе номер сети, где номер хоста. Маска работает по следующему принципу: там где в позициях единицы - это номер сети, а где нули - это номер хоста. Маску можно записать в двух видах:
+ В десятичном представлении - 255.255.255.0
+ В виде префикса - /24 - после слэша указывается сколько первых бит идет на номер сети, все остальное будет номером хоста. 

**У IP протокола есть две версии:**
+ IPv4 - адрес 4 байта
+ IPv6 - адрес 16 байт 

**IPv4** - форма представления 4 десятичных числа 0-255 разделенных точкой
Сетевой уровень использует агрегацию адресов, поэтому масштабирование - это работа не с отдельными адресами, а с подсетями(subnet)

### Типы IP-адресов
+ Индивидуальный(Unicast) - это адрес конкретного компьютера в сети
+ Групповой(Multicast) - это адрес использующиеся несколькими компьютерами, если мы отправим данные по этому адресу, то его получат все компьютеры с одинаковым адресом в подсети
+ Широковещательный(Broadcast) - это адрес использующийся всеми компьютерами в сети, если мы отправим данные по этому адресу, то его получат все компьютеры в подсети

**Широковещательный адрес** - имеет все единицы единицы в конце, т.е. ***.***.***.255. Широковещательные пакеты передаются только внутри подсети. 

**Специальные IP-адреса:**
+ Битовые единицы в номере хоста(***.***.***.255) - это широковещательный адрес
+ Битовые нули в номере хоста(***.***.***.0) - это адрес подсети
+ Хост с номером 1 (***.***.***.1)(по умолчанию) - маршрутизатор
+ Адрес из всех нулей (000.000.000.000) - текущий хост(подсеть)
+ Адрес из всех 255 (255.255.255.255) - все хосты в текущей подсети
+ 127.0.0.0/8 - обратная петля(loopback) - сеть для тестирования, данные не передаются
+ 169.254.0.0/16 - Link-local адреса


## Протокол IP
IP(Internet Protocol) - межсетевой протокол, задачей протокола является объединение сетей построенных на разных технологиях канального уровня
+ internet working - объединение сетей
+ internet - объединенная сеть / subnet - подсеть
+ Internet - название самой крупной сети построенной на протоколе IP

> Хотя сетевой уровень имеет разные протоколы, основным протоколом для передачи данных является IP, остальные служат для обеспечения крупной составной сети.

**Передача данных в протоколе IP:**
+ Без гарантии доставки
+ Без сохранения порядка следования сообщений

> В протоколе IP используется передача данных без установки соединения

**Задачи протокола IP:**
+ Объединение сетей
+ Маршрутизация(поиск маршрута)
+ Качество обслуживание

Пакет в протоколе IP:
+ Заголовок
+ + **1-ая Строка**
+ + Номер версии(4 бита) - IPv4 / IPv6
+ + Длинна заголовка(4 бита) - записывается полая длинна заголовка, если если доп опции то они также идут в длину заголовка
+ + Тип сервиса(8 бит) - на практике используется редко, служит для качества обслуживания
+ + Общая длина(16 бит) - длина пакета, включая заголовок и данные
+ + **2-ая Строка** - фрагментация
+ + Идентификатор пакета(16 бит)
+ + Флаги(3 бита)
+ + Смещение фрагмента(13 бит)
+ + **3-я Строка**
+ + Время жизни(TTL)(8 бит) - максимальное время, в течении которого пакет может перемещаться по сети, создано для того чтобы пакеты не гуляли по сети. Измеряется в количестве прохождения через маршрутизатор (hop)
+ + Тип протокола(8 бит) - поле нужно для реализации функций мультиплексирования/демультиплексирования(передача с помощью протокола IP, данных от разных протоколов следующего уровня). Примеры протоколов - TCP - 6, UDP - 17...
+ + Контрольная сумма(16 бит) - используется для правильности доставки пакета
+ + IP-Адрес отправителя(32 бита)
+ + IP-Адрес получателя(32 бита)
+ + Опции(Заголовок IP пакета может включать до поля, в данный момент опции почти не используются):
+ + + Запись маршрута
+ + + Маршрут отправителя
+ + + + Жесткая маршрутизация
+ + + + Свободная маршрутизация
+ + + Временные метки
+ Данные

### Маршрутизация
Маршрутизация - это поиск маршрута доставки пакета между сетями через транзитные узлы - маршрутизаторы.

**Этапы:**
1. Изучение сети - какие подсети и маршрутизаторы есть в сети, как маршрутизаторы объединены между собой
2. Продвижение пакетов на маршрутизаторе

Если мы передаем пакет на маршрутизатор то нам необходимо знать на какой именно маршрутизатор передать пакет чтобы он дошел до подсети. Для этого существует ***таблица маршрутизации***, в упрощенном виде она состоит из таких столбцов как:
+ Адрес подсети:
+ + Адрес
+ + Маска
+ Шлюз - данный столбец говорит о том что делать с пакетом которые вышел через данный шлюз, если интерфейс подсоединен к подсети напрямую в строке указывается _подсоединен_, иначе(если необходимо передать пакет на следующий маршрутизатор) то в строке пишется _ip-адрес маршрутизатора_
+ Интерфейс - данный столбец говорит о том через какой интерфейс маршрутизатора нам необходимо отправить пакет
+ Метрика - число характеризующие расстояние от одной сети до другой

***Формирование записей в таблицу маршрутизации:***
+ Статическое
+ + Настройка вручную 
+ Динамическое
+ + Автоматическая настройка

***Правила маршрутизации:***
+ Поиск маршрута к хосту (маска /32)
+ Поиск маршрута к сети (маска максимальной длинны)
+ Маршрут по умолчанию (маска /0, проходит все)

### Фрагментация
Фрагментация - разделение пакета на несколько частей(фрагментов) для передачи по сети с маленьким MTU(максимальный размер передаваемы данных). Для реализации фрагментации в заголовке пакета в протоколе IP, используются такие поля как:
+ *Идентификатор пакета* - задает номер пакета который разбит на фрагменты
+ *Флаги*
+ + Первый бит не используется
+ + Второй бит - не фрагментировать
+ + Третий бит - есть еще фрагменты
+ *Смещение фрагмента* -  так как протокол IP не обеспечивает гарантию доставки и следование порядка передачи сообщения, используется данное поле. 

Пример смещения фрагментов:
1. Исходный пакет 4000 байт(20 байт - заголовок, 3980 байт - данные)
2. MTU - 1500 байт (20 байт - заголовок, 1480 байт - данные)
3. Данные делятся на три фрагмента:
    + 0-1479
    + 1480-2959
    + 2960-3980
4. Для того чтобы вычислить смещение необходимо взять значение первого байта фрагмента, и разделить на 8 => 0/8=0, 1480/8=185, 2960/8=370

## Управляющие протоколы сетевого уровня
+ ICMP - протокол межсетевых управляющих сообщений, сообщает об ошибках в работе сети, позволяет тестировать сеть 
+ ARP - протокол разрешения адресов, позволяет определить по IP-адресу компьютера его MAC-адрес 
+ DHCP - протокол динамической конфигурации хостов, позволяет автоматически назначить компьютерам в сети IP-адреса

### DHCP
DHCP - протокол динамической конфигурации хостов. Для работы в сети каждому компьютеру нужен IP-адрес, данный протокол решает задачу выдачи адресов. У протокола есть два метода выдачи адресов:
+ Вручную
+ Автоматически 
Для использования протокола, необходимо создание инфраструктуры(DHCP сервера).

**Протокол DHCP работает по принципу клиент-сервер:**
+ Клиент DHCP - компьютер который получает IP-адрес автоматически
+ Сервер DHCP - компьютер который обеспечивает назначение IP-адресов и ведет таблицу выделенных адресов(чтобы избежать дублирования)

**Принцип работы DHCP сервера:**
1. Когда клиент подключается у него нет информации о сети, первая задача узнать где находится DHCP сервер, для этого он посылает сообщение DHCP-Discover на широковещательный MAC-адрес (FF:FF:FF:FF:FF:FF)
2. В ответ на сообщение *сервер* посылает Offer который включает в себя IP-адрес
3. В ответ *клиент* посылает Request с тем же IP-адресом
4. Сервер высылает подтверждающие сообщение Ack, туда включается IP-адрес

> Данное взаимодействие называют DORA -  Discover, Offer, Request, Ack

**Другие виды сообщений:**
+ NACK - Запрет использования запрошенного DHCP клиентом IP-адреса
+ RELEASE - Освобождение IP-адреса
+ INFORM - Запрос и передача дополнительной конфигурационной информации

**Назначение адресов DHCP**
+ Фиксированный - выделенный IP-адрес для каждого Mac-адреса
+ Динамический - выделение компьютеру любого IP-адреса из пула адресов

> Пул адресов - это список IP-адресов, которые назначает сервер, DHCP следит за уникальностью распределения адресов.

> IP-адрес выделяется DHCP клиенту на ограниченное время, после окончания времени аренды IP-адрес освобождается. DHCP клиент может продлить использование IP-адреса.

**Опции:**
Для работы в сети нужен не только IP-адрес, также существуют конфигурационные параметры передающиеся DHCP в качестве опций:
+ Маска подсети
+ Маршрутизатор по умолчанию
+ Адреса DNS-серверов
+ Адреса серверов времени
+ Маршруты
+ ...  

### ARP
ARP - протокол разрешения адресов, позволяет автоматически определить MAC-адрес компьютера по его IP-адресу. APR работает в режим запрос-ответ.

**Действия протокола в подсети:**
1. Компьютер отправляет на широковещательный адрес ARP запрос с IP-адресом
2. Компьютер у которого совпал IP-адрес возвращает ARP ответ с IP-адресом и MAC-адресом

**Пакет ARP протокола:**
+ Служебная информация:
+ + Тип сети
+ + Тип протокола
+ + Длина локального адреса
+ + Длина глобального адреса
+ Операция 
+ Локальный адрес отправителя
+ Глобальный адрес отправителя
+ Локальный адрес получателя
+ Глобальный адрес получателя

> Протокол ARP стоит между канальным и сетевым уровнем, он не может преобразовывать IP-адреса в MAC-адреса другой подсети - то есть не работает с маршрутизаторы.  

Компьютеры в сети кэшируют найденные MAC-адреса, записывая их в соответствующую таблицу - _ARP таблицу_, где есть такие столбцы как:
+ IP-адрес
+ MAC-адрес
+ Тип:
+ + Статический - запись которая занесена в таблицу вручную
+ + Динамический - запись которая занесена в таблицу автоматически, имеют определенный срок жизни, после чего удаляются 

### ICMP
ICMP - протокол межсетевых управляющих сообщений, используется для оповещении об ошибке или для тестирования сети.

**Формат ICMP пакета:**
+ Тип сообщения(1 байт) - тип ошибки
+ Код сообщения(1 байт) - подробное описание ошибки
+ Контрольная сумма(2 байта) - проверка правильности доставки
+ Служебная информация(4 байта) - зависит от кода сообщения
+ Поле данных - фрагменты пакета при котором произошла ошибка 

**Типы ICMP-сообщений**:
0. Эхо-ответ - проверка доступности компьютера в сети
3. Узел назначения недостижим
5. Перенаправление маршрута
8. Эхо-запрос - проверка доступности компьютера в сети
9. Сообщение о маршрутизаторе
10. Запрос сообщения о маршрутизаторе 
11. Истечение времени жизни пакета 
12. Проблемы с параметрами
13. Запрос отметки времени
14. Ответ отметки времени

**Диагностика сети**
Для диагностики сети протокол ICMP предлагает следующие утилиты:
+ ping -  используется для проверки доступности компьютера в сети(Эхо-запрос и Эхо-ответ)
+ traceroute - определяет маршрут отправителя к получателю

## Передача пакетов на сетевом и канальном уровнях

**Передача данных в одном сегменте сети:**
Допустим у нас есть два компьютера в сети. _Формируем пакет_: 
1. В заголовок  адрес отправителя вставляем свой IP-адрес и MAC-адрес, в адрес получателя вставляем IP-адрес получателя(MAC-адреса как правило не знаем, для того чтобы узнать MAC-адрес используется протокол ARP)
2. Нам нужен MAC-адрес поэтому отправляем ARP-запрос, получаем ответ с MAC-адресом и вставляем в заголовок
3. Пакет готов к отправке по сети

**Передача данных в разных сегментах сети:**
Допустим у нас есть два компьютера в сети. _Формируем пакет_: 
1. В заголовок  адрес отправителя вставляем свой IP-адрес и MAC-адрес, в адрес получателя вставляем IP-адрес получателя, нам необходим MAC-адрес, для начала сравниваем IP-адреса на подсеть(в нашем случае она будет разной так как компьютеры находятся в разных сегментах сети), так как IP-адреса подсети разные пакет с MAC-адресом маршрутизатора в виде получателя передается на маршрутизатор
2. Далее маршрутизатор меняет MAC-адрес отправителя на свой и передает пакет в подсеть или на другой маршрутизатор итд пока пакет не дойдет в подсеть, далее конечный маршрутизатор посмотрит в таблицу MAC-адресов, изменит MAC-адрес получателя и передаст пакет соответствующему компьютеру    

**Итог:**
+ IP-адреса в в пакете сохраняются постоянными
+ MAC-адреса постоянно меняются 
+ Вспомогательные средства при передаче пакетов:
+ + Протокол ARP
+ + Маска подсети
+ + Таблица маршрутизации
