# Описание действий JVM при запуске программы

public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}

А теперь по порядку :

1.  ClassLoader подгружает System classes и JvmComprehension.class.В stack создаётся frame для метода main().В frame(main()) помещается переменная int i = 1. 

2.  ClassLoader подгружает class Object.В heap создается объект класса Object, а ссылка o на него помещается в frame (main()).

3.  ClassLoader подгружает class Integer.В heap создается объект класса Integer(2),а ссылка ii на него помещается в stack в frame (main()).

4.  В stack будет создаваться новый frame для метода printAll().Туда помещаются ссылки o.i.ii.

5.  В heap создается объект класса Integer(700). Ссылка uselessVar на него помещается в frame(printAll()).

6.  В stack создается frame для метода toString(), в heap сохраняется результат работы метода.

    В stack создается frame для метода println(), после выхода из toString() сборщик мусора удаляет этот frame.

    После выхода из метода println()сборщик мусора удаляет этот frame.

7.  После выхода из метода printAll() сборщик мусора удаляет этот frame.

    Создается frame для метода println(). В heap помещается String("finished"), после выполнения метода сборщик мусора удаляет этот frame.

    После окончания выполнения метода main() удаляется фрейм этого метода.
