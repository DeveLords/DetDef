Данная документация является опорной точкой вообще всего данного проекта. Идея данного проекта основана на том, что при использовании термографического метода исследования различного рода объектов, т.е. исследование изменение температуры на поверхности какого-либо объекта с целью его диагностики и проверки на наличие каких-либо дефектов, утечек и других проблем. В данной работе поднимается вопрос о том, возможно ли при помощи термограмм обнаруживать дефекты на тепловых сетях и если возможно ли сделать этот процесс автоматизированным. Рассмотрим первую задачу. Изучив несколько различных источников, поговорив с людьми, занимающихся в сфера теплоэнергетики, я пришел к следующему выводу: устройства для получения термограмм – тепловизоры, являются достаточно дорогостоящим приобретением, однако в руках профессионала это настоящее оружие, способное обнаружить начиная от перегрева элементов электрических цепей, заканчивая обнаружением конденсата в теплоизоляционном слое дома, однако данные процесс довольно сложен, необходимы верные условия, точная настройка тепловизора и правильная интерпретация обнаруженных дефектов. Итак, на первый задачу ответ был найден, но остается вторая задача, нужно проверить гипотезу о том, что данное решение позволит решить огромное количество задач связанных с мониторингом теплосетей. 
Первоначальная этап решения данной задачи является выяснение вопроса, а какие вообще уже существуют решения. Исследования данного вопроса позволили выявить несколько таких компаний, которые занимаются решением данного вопроса, однако в чем же отличие нашего решения, вероятно в том, что данное решение будет способно работать с любым типом тепловизоров, с различной точность измерения. В решении данной задачи точно нужна лишь до 1-2 градусов по цельсию, с подомным отлично справляются большинство тепловизоров на рынке подобных устройств. Вопрос, который последовал следующим, какие вообще программные средства можно использовать для этих целей, ведь как известно, имеется огромное количество программ обработки изображений, однако в данном случае требуется разработать такое программное средство, которое было бы способно на основе клиент-серверной архитектуры приложения выполнять анализ изображений и представлять готов результат ЛПР в удобном для него виде. Кроме того, требуется широкий и гибкий инструментарий для разработки, к тому же способный эффективно работать на сервере. В связи с этим, серверным языком был выбран python, в качестве языка десктопного приложения был выбран язык java. Помимо будет разрабатываться так же мобильное приложение на основе движка unity. В качестве базы данных для хранения информации о прошедших исследованиях, так как хранить всю эту информацию в оперативной памяти компьютера бессмысленно будет разработана база данных, пока еще не точно, но вероятно будет использоваться технология PostgreSQL. Выбор python в качестве серверного языка обусловлена прежде всего тем, что он имеет огромное множество различного рода надстроек, в том числе веб-надстроек – flask и Django. Разработчик, т.е. Я пока еще в раздумьях, какой же фреймворк использовать, однако в скором времени я приду к решению и будет уже ясно, что под данные задачи будет подходить наилучшим образом. Кроме того, так как я занимаюсь всей этой темой с сервером, следовательно, я должен понимать все механизмы работы, а также составить алгоритмы обработк, сформировать полноценную модель описывающий данный модуль. Я думаю это должно получиться, поэтому на следующему шаге я приступаю к разработке непосредственно структуры серверного приложения. Итак…
Поиск конкретной горячей области на изображении
1) Загружаем оригинал.
2) Передаем полученную маску с предыдущего этапа от работы программы.
3) Накладываем маску, при этом преобразовывваем ее путем порогового преобразования.
4) Совмещаем маску и оригнал обрабатываем и получаем матрицу, элементы которой явялется сумма RGB соотвествующего пиксела.
5) Ищмем минимальный ненулевой элемент в данной матрице.
6) Ищем максимальный элемент данной матрицы.
7) Суммируем все ненулевые элементы, предварительно каждый из них преобразованный в температуру.
8) Суммируем разброс диапазона среднего по формуле:

- элемент матрицы сумм составляющих пикселей, где comb_origIJ(R) - красная составляющая пиксела, comb_origIJ(G) - Зеленая составляющая пиксела. В данной цветовй палитре синяя составляющая не изспользуется 
