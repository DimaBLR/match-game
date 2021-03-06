Инструкция по написанию игры match-match-game

Я не буду рассматривать создание форм входа в игру, таймеров, input, select, таблицы рекордов и т.д., а лишь покажу как создать саму логику игры.

Предположим, у нас есть переменная, которая получена от игрока при выборе кол-ва карт -> const numberCards = 10;

Для начала, нам необходимо создать массив(объект) случайных чисел. Я буду рассматривать вариант с массивом. Так как карт в игре у нас будет 10, следовательно можно сделать вывод, что 10/2 = 5 уникальных карт в игре, имеющих пару. Соответственно создаём массив из 5 элементов, например так, new Array(numberCards/2). Затем делаем из каждого элемента(пока пустого) порядокове число и получаем [1,2,3,4,5]. Так как логика игры - это пара, то делаем concat массива с собой же и получаем [1,2,3,4,5,1,2,3,4,5]. После чего рандомно перемешиваем наш новый массив.

Массив рандомного расположения карт создали. Теперь переходим к созданию игрового поля. Будем считать, что 1 карта - это 1 DIV в DOM. Создать игровое поле можно циклом, рекурсией, методами и т.д. Вариантов тут много. Рассмотрим вариант с циклом. Запускаем цикл с количеством итерацией равной кол-ву карт. В него пишем код , который создает div, например, document.createElement('div'). В итоге мы получили игровое поле (надеюсь вы уже задали стили в css для этих div). Но все карты у нас пока полностью идентичны, поэтому давайте в цикле пропишем еще и добавление в div, например атрибута random="x", где x при каждой итерации будет браться из нашего рандомного массива. Вот теперь всё в порядке, карты на игровом поле теперь не идентичны.

Далее, нам нужно "навесить" обработчик события по клику. Его можно навесить каждой карте прямо в цикле(выше), НО лучше пойти путём делегирования и навесить на родительский div всех карт и отлавливать клики по event.target. Затем нам нужно как-то связать рандом карты с изображением. Как вы догадались уже, атрибут random и будет нашим изображением обратной стороны карты). Для начала скачиваем папку с картами, удобнее всего гуглятся(для скачивания) "карты taro", кроме того они ещё и пронумерованы числами! А теперь при клике на карту она будет просто менять свой background, где атрибут random будет равен имени картинки в папке. Например, при клике на карту получаем атрибут Random='3' и задаём ей background:url(img/${random}.jpg);

Теперь у нас открываются карты, но не переварачиваются обратно. Перевернуть можно по SetTimeout. Но давайте сначала добавим в нашу функцию-обработчик инструкции. Проверяем на кол-во открытых карт (удобнее завести переменную clkickCounter) и отслеживать кол-во открытых карт, например так if (clickCounter % 2 == 0). То есть как только кол-во кликов стало чётным, значит открыто 2 карты(только не забудьте заблокировать клик по уже открытой карте). Для удобства, можно помечать открытые карты путём добавления класса, например opened, а затем удалять его. Сначала делаем проверку, равны ли атрибуты Random этих открытых карт. Если нет, то закрываем все карты, путем удаления у них Backgraund полученного из атрибута Random по SetTimeout. Если карты равны, то делаем, например display: none / opacity:0 или как-то ещё.

Чтобы избежать открытия более 2-х карт, можно после открытия второй карты, пройтись по всем картам и дать атрибут pointer-events: none, либо просто удалить обработчик click, а по setTimeout вернуть его обратно.

Чтобы вывести поздравление игроку после победы, заводим переменную равную кол-ву карт и при каждом совпадении отнимаем у неё 2. Добавляем эту проверку в нашу функцию-обработчик. И тут же удобно добавлять результаты игры в indexedDB ка ктолько остаток карт станет равным 0

Прежде чем начать работу с indexedDB, рекомендую сначала реализовать это через window.localStorage, для наилучшего понимания приницпа работы

Буду благодарен за отзыв, помогла ли вам статья в решении таска! Dmitry Belov(@DimaBLR)
