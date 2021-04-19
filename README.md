# Erlang
Erlang - функциональный язык программирования с сильной динамической типизацией, предназначенный для создания распределённых вычислительных систем. Разработан и поддерживается компанией Ericsson. Язык включает в себя средства порождения параллельных легковесных процессов и их взаимодействия через обмен асинхронными сообщениями в соответствии с моделью акторов.

Erlang был целенаправленно разработан для применения в распределённых, отказоустойчивых, параллельных системах реального времени, для которых, кроме средств самого языка, имеется стандартная библиотека модулей и библиотека шаблонных решений (так называемых поведений) — фреймворк OTP (англ. Open Telecom Platform). Программа на Erlang транслируется в байт-код, исполняемый виртуальными машинами, находящимися на различных узлах распределённой вычислительной сети. Erlang-системы поддерживают горячую замену кода, что позволяет эксплуатировать оборудование безостановочно.
# Основные особенности
## Высокоуровневые конструкции
Erlang является декларативным языком программирования, который скорее используется для описания того, что должно быть вычислено нежели как. Например, определение функции, которое использует сопоставление с образцом для выбора одного из вариантов вычисления или извлечения элемента данных из составной структуры, напоминает уравнение. Сопоставление с образцом распространено даже на битовые строки, что упрощает реализацию телекоммуникационных протоколов.

Функции являются объектами первого класса в Erlang. В языке также широко применяются характерные для функциональной парадигмы программирования списковые включения (генераторы списков)
## Параллельные вычисления
Отличительной особенностью языка является применение легковесных процессов в соответствии с моделью акторов. Такой подход позволяет выполнять одновременно сотни тысяч и даже миллионы таких процессов, каждый из которых может иметь скромные требования по памяти. Процессы изолированы друг от друга и не имеют общего состояния, но между ними можно установить связь и получать сообщения об их состоянии. Для взаимодействия процессов используется асинхронный обмен сообщениями. Каждый процесс имеет свою очередь сообщений, обработка которой использует сопоставление с образцом. Процесс, отправивший сообщение, не получает уведомления о доставке, даже если идентификатор процесса-получателя недействителен или получатель игнорирует сообщение. Таким образом, ответственность за правильно организованное взаимодействие между процессами лежит на разработчике
## Распределённые вычисления
Erlang с самого начала проектировался для распределённых вычислений и масштабируемости. Распределение вычислений встроено в синтаксис и семантику языка, поэтому построение системы можно вести, абстрагируясь от конкретного места вычислений. В стандартной поставке Erlang может наладить связь процессов по протоколу TCP/IP независимо от поддерживаемых им нижележащих платформ (операционных систем).

Работающий экземпляр среды выполнения Erlang (англ. Erlang runtime system) называется узлом (англ. node). Программы, написанные на Erlang, способны работать на нескольких узлах. Узлами могут быть процессоры, многие ядра одного процессора, и даже целый кластер машин. Узел имеет имя и «знает» о существовании других узлов на данной машине или в сети. Создание и взаимодействие процессов разных узлов не отличается от организации взаимодействия процессов внутри узла. Для создания процесса на другом узле процессу достаточно знать его имя и, без особых на то оснований, он может не интересоваться физическим расположением взаимодействующего с ним процесса. Синтаксис отправки сообщения процессу на своём узле и удалённом — один и тот же.

Благодаря встроенным в язык возможностям распределённых вычислений объединение в кластер, балансировка нагрузки, добавление узлов и серверов, повышение надёжности вызывают лишь небольшие затраты на дополнительный код. По умолчанию узлы спроектированы для работы внутри обособленного сегмента сети (DMZ), но, если необходимо, коммуникация между узлами может происходить с применением защищённого криптографическими методами протокола SSL
## Горячая замена кода
Для систем, которые не могут быть остановлены для обновления кода, Erlang предлагает горячую замену кода (англ. hot code upgrade). При этом в приложении могут одновременно работать старая и новая версии кода. Таким способом программное обеспечение на Erlang может быть модернизировано без простоев, а выявленные ошибки исправлены


## Функции
Программы на Erlang состоят из функций, которые вызывают друг друга. Количество параметров функции называется арностью. При вызове функции заголовочные части описания функции сопоставляются с образцом. В случае совпадения параметров вызова, формальные параметры связываются с фактическими и исполняется соответствующая часть тела функции. Запись варианта вычисления функции для некоторого образца может называется клозом от англ. clause, а определение функции — это набор из одного или более клозов.

Для уточнения сопоставления с образцом в функциях можно использовать охранные выражения, которые следуют после ключевого слова when. В примере ниже определена функция вычисления знака числа, которая рассчитывается в зависимости от сравнения параметра с нулём:

'''
sign(X) when X > 0 -> 1;
sign(X) when X == 0 -> 0;
sign(X) when X < 0 -> -1.
'''

Клозы Erlang перебирает в том порядке, в котором они записаны, пока не будет найден подходящий заголовок. В охранных выражениях можно использовать только ограниченный набор встроенных функций, так как эти функции не должны иметь побочных эффектов.

Разумеется, функции Erlang поддерживают рекурсивные вызовы. В случае, когда определение функции оканчивается рекурсивным вызовом (хвостовая рекурсия), Erlang использует оптимизацию: стек вызовов не применяется.

Как параметром, так и результатом функции может быть другая функция. В следующем примере функция одного аргумента возвращает функцию для прибавления аргумента:

'''
1> Plus = fun (X) -> fun(Y) -> X+Y end end. % Определение функции, возвращающей функцию
#Fun<erl_eval.6.82930912>
2> Plus(2).                                 % Функция возвращает Fun-объект 
#Fun<erl_eval.6.82930912>
3> Plus(2)(3).                              % Такой синтаксис не работает
* 1: syntax error before: '('
4> (Plus(2))(3).                            % Дополнительные скобки позволяют добиться требуемого результата
5
5> Plus2 = Plus(2), Plus2(3).               % То же самое с использованием дополнительной переменной
5
'''

## Примеры
Вычисление факториала на Erlang:
'''

-module(fact).
-export([fac/1]).

fac(0) -> 1;
fac(N) when N > 0, is_integer(N) -> N * fac(N-1).
'''

Алгоритм сортировки, напоминающий быструю сортировку:

-module(qsort).
-export([qsort/1]).

qsort([]) -> []; % Тривиальный случай пустого списка
qsort([Pivot|Rest]) ->
    % Конкатенация списка элементов до Pivot, списка из одного элемента Pivot и после Pivot
    qsort([Front || Front <- Rest, Front < Pivot])
    ++ [Pivot] ++
    qsort([Back || Back <- Rest, Back >= Pivot]).
В этом примере функция qsort вызывается рекурсивно до исчерпания всех элементов. Выражение [Front || Front <- Rest, Front < Pivot] собирает список Front из элементов Rest таких, что элемент Front меньше Pivot. Оператор ++ склеивает списки.

## Условные выражения
Кроме выбора описания в определении функции, в Erlang есть и другие условные выражения: case-выражения (выражение выбора) и if-выражения. Выражение выбора позволяет организовать сопоставление с образцом внутри функции и обычно имеет следующий синтаксис:

case выражение-выбора of
  образец1 when охрана1 -> выражение11, выражение12, ...;
  образец2 when охрана2 -> выражение21, выражение22, ...;
  ...
  образецN when охранаN -> выражениеN1, выражениеN2, ...
end
Это выражение всегда возвращает значение, соответствующее последнему вычисленному выражению в строке с подошедшим образцом. Это возвращаемое значение может служить возвращаемым значением функции, а может быть присвоено переменной. Как и в заголовочной части функции, после образца может следовать охранное выражение.

Упрощённым вариантом case-выражения является if-выражение:

if
  охрана1 -> выражение11, выражение12, ...;
  охрана2 -> выражение21, выражение22, ...;
  ...
  охранаN -> выражениеN1, выражениеN2, ...
end
Здесь охранаi — охранное выражение. Первое истинное охранное выражение вызывает выполнение соответствующих выражений, последнее из которых и является значением всего if-выражение. Следует заметить, что и здесь в охранном выражении можно применять только ограниченный набор операций и встроенных функций.

Запятые в охранном выражении работают как операция and, например:

if
  X =< 0 -> 'меньше или равно нулю';
  X > 0, X < 10 -> 'больше нуля и меньше десяти';
  X >= 10 -> 'больше или равно десяти';
end
Компилятор Erlang следит за безопасностью связывания переменных внутри условных выражений, как видно из следующего примера модуля:

-module(badexample).
-export([broken_if/1]).
broken_if(X) ->
  if
    X < 0 -> Z = -1;
    X >= 0 -> Y = 1
  end,
  Y * Z.
При попытке откомпилировать модуль возникают сообщения об ошибках, так как в таком коде одна из переменных не связывается со значением:

1> c(badexample).
badexample.erl:8: variable 'Y' unsafe in 'if' (line 4)
badexample.erl:8: variable 'Z' unsafe in 'if' (line 4)
error
Правильным было бы определить все используемые далее по коду переменные во всех ветвях if-выражения.

## Препроцессор и макросы
Препроцессор Erlang (EPP) позволяет вкладывать файлы с исходным кодом один в другой, определять макросы и осуществлять простые и параметризованные макроподстановки[80]. Макрос определяется с помощью директивы -define, а макроподстановка осуществляется указанием имени макроса и возможных параметров после вопросительного знака (?). Следующий пример показывает определение и применение параметризованного макроса:

-define(ZERO(X),X == 0)
is_zero(T) when ?ZERO(X) -> true;
is_zero(T) -> false.
Имя макроса обычно пишется прописными буквами. Определение макроса должно содержать лексемы Erlang целиком (например, попытка задать часть имени переменной с помощью макроса вызовет синтаксическую ошибку). Макросы могут использоваться для повышения удобочитаемости кода в охранных выражениях, для операторов отладки и т. п. Препроцессор имеет несколько предопределённых макросов, которые нельзя переопределить: ?MODULE, ?MODULE_STRING, ?FILE, ?LINE, ?MACHINE.

Заголовочный файл (расширение .hrl) с определениями макросов и записей можно включить при помощи директивы -include.

## Обработка ошибок
Для обработки исключительных ситуаций в Erlang можно применять конструкцию try-catch, в общем случае записываемую в следующем виде:

try вычисляемое-выражение of
  образец1 when охрана1 -> выражение1;
  образец2 when охрана2 -> выражение2;
  ...
  образецN when охранаN -> выражениеN
catch
  класс1:образецИскл1 when охранаИскл1 -> выражениеИскл1;
  ...
  классM:образецИсклM when охранаИсклM -> выражениеИсклM;
end
Как и в случае case-выражения, вычисляемое выражение сопоставляется с образцом (части между of и catch) для получения результата. После ключевого слова catch следуют части обработки исключений, в которых в дополнение к образцам исключений могут быть указаны классы исключений (перед двоеточием): error, throw и exit. Подчёркивание может использоваться как в образце, так и в классе исключения. Следующий простой пример иллюстрирует перехват ошибки класса error при вычислении квадратного корня:

1> try math:sqrt(-1) catch error:Error -> {error, Error} end.
{error, badarith}
2> try math:sqrt(4) catch error:Error -> {error, Error} end.
2.0
Для создания исключений, определённых пользователем, используется функция throw/1, которая принимает кортеж с более детальным описанием возникшей ошибки
 и генерирует исключение класса throw. Использование этой функции нежелательно из-за ухудшения удобочитаемости кода программы, но может потребоваться в некоторых случаях при работе с вложенными структурами данных, например, при разборе XML[86]. Исключения класса exit возникают в результате вызова встроенной функции exit/1 или сигнала выхода.

До разработки Ричардом Карлссоном (Richard Carlsson) из команды проекта HiPE описанного выше нового механизма обработки исключений (появился в версии R10B) в Erlang использовались catch-выражения.

## Модули
Код программы на Erlang можно разбить на отдельные модули. Модуль — имя для набора функций, организованных в одном файле. Имя модуля должно совпадать с именем файла (если отбросить расширение). Модуль можно откомпилировать в байт-код как из командной строки операционной системы, так и из командной оболочки Erlang. В файле модуля можно записать объявления функций и директивы (иногда называются атрибутами). Обязательным атрибутом является только -module(атом_имени_модуля). Другой часто используемый атрибут — -export — применяется для указания списка экспортируемых функций, то есть функций, которые можно использовать за пределами модуля.

Функции в Erlang однозначно определяются модулем, именем и арностью. Например, math:cos/1 соответствует функции cos из модуля math, принимающей один аргумент. Вызвать функцию можно так: math:cos(1.2).

Исходный текст модуля компилируется в BEAM-файл — файл, содержащий байт-код виртуальной машины BEAM (англ. Bogdan’s/Björn's Erlang Abstract Machine). В свою очередь, ERTS (англ. Erlang Runtime System — система времени выполнения Erlang) выполняет этот код.

## Процессы
Основной абстракцией параллельного программирования в Erlang является процесс. Процессы могут порождать другие процессы, выполняться одновременно, обмениваться сообщениями, реагировать на завершение друг друга.

## Создание процессов
Для создания нового процесса служит несколько встроенных функций (spawn и её аналоги). Функции возвращают идентификатор процесса, который может использоваться, например, для отправки сообщений вновь созданному процессу. В интерактивной консоли erl можно получить список процессов и другую информацию посредством вызова функций processes(). и i(). соответственно
