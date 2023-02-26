<h1>JVM</h1>

<div>
    <h3>public class JvmComprehension {</h3>
    
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
</div>
1. Локальной переменной <mark>i</mark> присваивается значение <mark>1</mark> и храниться в <mark>heap</mark> после чего она помещается в <mark>Stack</mark> во фрейм <mark>main</mark>.

2. Создается ссылочная переменная <mark>о</mark>, класса <mark>Object</mark>, под нее в <mark>heap</mark> выделяется память. Ссылка о на созданный объект помещается во фрейм <mark>main</mark>.

3. Создается ссылочная переменная <mark>ii</mark> класса <mark>Integer</mark>, которой присваивается значение <mark>2</mark>, под нее в <mark>heap</mark> выделяется память. Ссылка <mark>ii</mark> на созданный объект помещается во фрейм <mark>main</mark>.

4. В <mark>Stack</mark> создаётся новый фрейм для вызова метода <mark>printAll()</mark> с тремя параметрами:
   1. ссылка <mark>o</mark> на ранее созданный <mark>Object</mark> в <mark>heap</mark>
   2. локальная переменная <mark>i</mark>
   3. ссылка <mark>ii</mark> на ранее созданный <mark>Integer</mark> в <mark>heap</mark>
   
5. Создается ссылочная переменная <mark>uselessVar</mark> класса <mark>Integer</mark>, которой присваивается значение <mark>700</mark>, под нее в <mark>heap</mark> выделяется память. Ссылка <mark>ii</mark> на созданный объект помещается во фрейм <mark>printAll</mark>.

6. Для каждого из полей <mark>o</mark>, <mark>i</mark> и <mark>ii</mark> вызывается метод <mark>toString()</mark>:
   1. Для каждого такого вызова создается отдельный фрейм в <mark>Stack</mark>
   2. В <mark>Heap</mark> выделяется память под новый объект класса <mark>String</mark> в который заносится результат конкатенации строк. 
   3. В <mark>Stack</mark> создаётся новый фрейм для метода <mark>println()</mark>. Ссылка на созданный объект помещается во фрейм <mark>println</mark>. 
   4. После выполнения метода <mark>println()</mark> фрейм <mark>println</mark> удаляется из <mark>Stack</mark>.
   5. Новый объект типа <mark>String</mark> может быть удалён из <mark>heap</mark> при следующем запуске <mark>Garbage collector</mark>, т.к. отсутствует ссылка на данный объект. 
   6. После выполнение метода <mark>printAll()</mark> фрейм удаляется из <mark>Stack</mark>

7. System.out.println("finished");
   1. В <mark>heap</mark> выделяется память под новый объект класса <mark>String</mark>, который инициализируется значением <mark>finished</mark>.
   2. В <mark>Stack</mark> создаётся новый фрейм для метода <mark>println()</mark>. Ссылка на созданный объект помещается во фрейм <mark>println</mark>. 
   3. После выполнения метода <mark>println()</mark> фрейм <mark>println</mark> удаляется из <mark>Stack</mark>. Фрейм <mark>main</mark> удаляется из <mark>Stack</mark>.