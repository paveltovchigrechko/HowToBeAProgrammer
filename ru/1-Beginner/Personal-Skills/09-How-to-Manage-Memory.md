# Как управлять памятью
[//]: # (Version:1.0.0)
Память - это ценнейший ресурс, который вы не можете себе позволить исчерпать. Какое-то время вы можете игнорировать ее, но в один момент вам придется решать, как ею управлять.

Пространство памяти, которое должно сохраняться за пределами одной подпрограммы, часто называется *выделенной кучей*. Участок памяти без указателей на него бесполезен и называется *мусором*. В зависимости от системы, которую вы используете, вы можете решить удалить в явном виде память, выделенную под данные, которые вот-вот станут мусором. Но чаще всего у вас будет возможность использовать *сборщик мусора*. Он определяет мусорную память и освобождает ее автоматически, без вмешательства программиста. Сборщик мусора это прекрасное средство, оно уменьшает число ошибок в коде, позволяет писать его короче и понятнее с наименьшими затратами. Используйте его, когда это возможно.

Но даже со сборщиком мусора вы можете забить всю память мусорными данными. Классическая ошибка - использовать хеш-таблицу в качестве кэша и забыть удалить ссылки в ней. Поскольку ссылка остается, данные по ней недосягаемы, и ссылка бесполезна. Это называется *утечкой памяти*. С самого начала разработки следует следить за утечками памяти и устранять их. Если у вас есть долгоработающие системы, то память может никогда не заканчиваться при тестировании, но будет исчерпана пользователями при реальной работе.

Создание новых объектов это относительно затратная операция в любых системах. Память, выделенная напрямую под локальные переменные подпрограммы, однако, обычно дешевле из-за простой политики ее высвобождения. Избегайте создания ненужных объектов.

Важный момент происходит, когда вы можете определить верхнюю границу числа требуемых объектов. Если все объекты занимают одинаковый объем памяти, то вы можете выделить под них один блок памяти или буфер. Все необходимые вам объекты можно создавать и удалять внутри этого блока по принципу ротации, так что иногда это называют кольцевым или циклическим буфером. Обычно он быстрее, чем выделенная куча. 

Иногда вам придется явно освобождать выделенное пространство памяти вместо того, чтобы полагаться на сборщик мусора. В этом случае вы должны тщательно проанализировать каждую часть выделенной памяти и разработать способ ее высвобождения в нужный момент времени. Способ может отличаться для каждого типа объектов, который вы создаете. Вы должны убедиться, что каждой операции выделения памяти соответствует операция ее освобождения. Это непросто, поэтому для упрощения задачи программисты как правило реализуют сборщик мусора в простой форме, например, в виде подсчета ссылок на объекты.

Следующее: [Как устранять плавающие баги](10-How-to-Deal-with-Intermittent-Bugs.md)
