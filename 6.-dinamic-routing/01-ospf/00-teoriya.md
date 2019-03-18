# Теория

Рассмотрим его работу на примере вот такой упрощённой сети:

![](http://img-fotki.yandex.ru/get/6520/83739833.1f/0_9da12_d1d6fb5c_XL.jpg)

Для начала надо сказать, что для того, чтобы между маршрутизаторами завязалась дружба \(отношения смежности\) должны выполниться следующие условия:

1\) в OSPF должны быть настроены одинаковые **Hello Interval** на тех маршрутизаторах, что подключены друг к другу. По умолчанию это 10 секунд в Broadcast сетях, типа Ethernet. Это своего рода KeepAlive сообщения. То есть каждые 10 секунд каждый маршрутизатор отправляет Hello пакет своему соседу, чтобы сказать: “Хей, я жив”,  
2\) Одинаковыми должны быть и **Dead Interval** на них. Обычно это 4 интервала Hello — 40 секунд. Если в течение этого времени от соседа не получено Hello, то он считается недоступным и начинается ПАНИКА процесс перестроения локальной базы данных и рассылка обновлений всем соседям,  
3\) Интерфейсы, подключенные друг к другу, должны быть в **одной подсети**,  
4\) OSPF позволяет снизить нагрузку на CPU маршрутизаторов, разделив Автономную Систему на зоны. Так вот **номера зон** тоже должны совпадать,  
5\) У каждого маршрутизатора, участвующего в процессе OSPF есть свой **уникальный** индентификатор — **Router ID**. Если вы о нём не позаботитесь, то маршрутизатор выберет его автоматически на основе информации о подключенных интерфейсах \(выбирается высший адрес из интерфейсов, активных на момент запуска процесса OSPF\). Но опять же у хорошего инженера всё под контролем, поэтому обычно создаётся Loopback интерфейс, которому присваивается адрес с маской /32 и именно он назначается Router ID. Это бывает удобно при обслуживании и траблшутинге.  
6\) Должен совпадать размер MTU

Далее пьеса в восьми частях.