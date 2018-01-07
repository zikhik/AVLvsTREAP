# AVLvsTREAP
# Формат входных данных и выходных данных.
На стандартном потоке ввода задаётся последовательность команд. Пустые строки игнорируются.
Команды: insert, delete, find, print, min, max
Каждая строка содержит ровно одну команду command [key] [data], где command — заданные операции для данной структуры.
key — ключ, целое число;
data — данные, целое число.

Имена входных и выходных файлов задаются через аргументы командной строки. В моей реализации в качестве аргументов командной строки подаются строки, содержащие имя входного, выходного файлов, а также режим работ.
Шаблоны аргументов ком. строки:
	"in.txt", "out.txt", "file" - обработка команд из файла in.txt с последующей информационной записью в out.txt.
	"in.txt", "out.txt", "correct" - запуск тестов корректности с информационной записью об успешном тестировании в файлы 001.txt и 002.txt (согласно шаблону задания)
	"in.txt", "out.txt", "test" - запуск тестов скорости с информационной записью о скорости сценариев(см. ниже) в файл out.txt
# Логика программы
Программа состоит из 5 файлов, 4 из которых являются header'ами: crtsn.h, avl.h, tests.h, correct.h. Последний файл AVLvsTREAP.cpp содержит исполняемую функцию main(). Содержание файлов-заголовков - такое: 
•	crtsn.h - реализация treap;
•	avl.h - реализация AVL;
•	tests.h - код тестов сценария (на скорость)
•	correct.h - тесты корректности.
С него начинается работа с программой. Необходимо задать шаблоны приведенных ниже аргументов командной строки(рис 3.).
Рис 3. Вращения в AVL-дереве.
Первый и второй аргумент - произвольные, третий - строго из предложенных выше команд.
В случае первого шаблона - интересуемый результат в kekOut.txt, во втором - в файлах 001.txt и 002.txt, в третьем - в kekOut.txt.
Описание тестов-сценариев.
	Для описания тестов смоделируем ситуацию(сценарий их использования). Для этого представлю себя организатором лотерейных розыгрышей. В данном случае в наших структурах планируется хранить номера лотерейных билетов.

# Тест №1:
Описание: Итак представим главную ситуацию. Мои лотерейные билеты я хочу продавать на всей территории нашей протяженной страны. Чтобы не возникало путаницы я организовал производство (то бишь печать билетов) "на местах", и чтобы не запутаться у меня номера напечатанных лотерейных билетов идут по возрастанию по мере перемещения по карте нашей страны с запада на восток. Но продажи я хочу начинать в одно и то же время независимо от региона. Для этого хочется провести "стресс" тест и представить как я буду заполнять базу активированных билетов в случае, если они покупаются то в Калининграде то во Владивостоке. Этим собственно и занимается первый тест - заполнением структур данных чисел с большим разбросом.
Конкретная реализация: вставка 1 000 000 элементов в дерево с диапазоном значений 1 500 000 000
# Тест №2:
Описание: Посидев, подумав, я решил посмотреть, а вдруг мне выгоднее проводить не один большой тираж по всей стране а равное ем число тиражей по регионам. Так, собственно, и  второй тест создает такое же число лотерейных билетов как и Тест №1, однако разбивает его по регионам(делит на мелкие структуры данных).
Конкретная реализация: вставка 1 000 000 элементов в 10 деревьев с диапазоном значений 1 500 000 000

# Тест №3:
Описание: Дела мои с лотерейками пошли в гору, я понял, что сидеть на месте это не мое и пора выходить на новый уровень. Газеты пестрят заголовками что моя сеть расширяется и теперь я организую розыгрыши по всему СНГ - значит мне нужна большая структура. Тест 3 выясняет скорость работы большой структуры данных.
Конкретная реализация: вставка 15 000 000 элементов в дерево

# Тест №4:
Описание: Этот тест показывает как определяются и сколько ищутся среди всех участников победители: 5 000 000 обладателей совсем мелких призов, 1 000 000 обладателей мелких призов, 50 000 -  обладателей"нестыдных призов", и 3 безоговорочных суперультрамега победителя. Стоит сказать , что билеты выбранных победителей могут и не быть куплены или разыграны -  как любят делать организаторы настоящих розыгрышей.
Конкретная реализация: 4 независимых поиска по большому дереву из 3-го теста. В общей сумме 6 000 050 003 поиска.
# Тест №5:
Описание: Форс-мажорные обстоятельства(!!!). Я узнаю об ошибке печати лотереек на конкретном производстве - нужно срочно снять их с розыгрыша(и, возможно, вернуть деньги покупателям;).
Конкретная реализация: Удаление 1 500 000 элементов структуры данных.
# Тест №6:
Описание: -
Конкретная реализация: Время min/max
_______________________________________________________
 *Тесты корректности содержаться в correct.h, всего представлено 8 общих тестов (всего 16): 
1.	Создание структуры;
2.	Первая вставка;
3.	Удаление до пустой структуры;
4.	Несколько вставок подряд;
5.	Поиск элемента;
6.	Поиск минимума и максимума;
7.	Удаление промежуточного(имеет как сына так и родителя) узла;
8.	Удаление листьев;

**Также для treap есть тест проверки соотношения приоритетов.
_______________________________________________________
# Результаты сценарных тестов:
Примечание: тесты были произведены на моноблоке LENOVO 10150 в версии RELEASE x64.

        TEST №1, ms	  TEST №2	  TEST №3	  TEST №4	  TEST №5	  TEST №6
AVL	    1351	        1120	    34332   	134	      99	      1
TREAP	  414	          1017	    5022    	125	      21	      0

