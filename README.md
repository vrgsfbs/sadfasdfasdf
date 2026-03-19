using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace stacklaba
{
    internal class Program
    {
        class Stack
        {
            private int ukazatel = -1;
            private const int stacklenght = 5;
            private int[] StackArr = new int[stacklenght];
            public void Push(int val)
            {
                ukazatel++;
                if (ukazatel >= stacklenght)
                {
                    throw new StackOverflowException("Стек переполнен");
                }
                else
                {
                    StackArr[ukazatel] = val;
                }
            }
            override public string ToString()
            {
                string str = string.Empty;
                for (int i = 0; i <= ukazatel; i++)
                {
                    str += $"{StackArr[i]} ";
                }
                str += "\n";
                return str;
                }
            public void Pop()
            {
                ukazatel--;
            }
            public int Val { get { return StackArr[ukazatel]; } }
            public int Pos {get { return ukazatel; }}
            public int Length { get { return stacklenght; } }
        }
        static void Main(string[] args)
        {
            Stack stack = new Stack();
            ConsoleKeyInfo K;
            do
            {
                Console.Clear();
                Console.WriteLine("1.Вывести стек");
                Console.WriteLine("2.Добавить элемент в стек");
                Console.WriteLine("3.Убрать из стека последний элемент");
                Console.WriteLine("4. Добавить на дно стека произведение всех его элементов");
                Console.WriteLine("Esc. Выход из программы");
                K = Console.ReadKey();
                switch (K.Key)
                {
                    case ConsoleKey.D1:
                    case ConsoleKey.NumPad1: // если нажата клавиша с цифрой 1
                        {
                            Console.WriteLine(stack.ToString());
                            break;
                        }
                    case ConsoleKey.D2:
                    case ConsoleKey.NumPad2:// если нажата клавиша с цифрой 2
                        {
                            Console.WriteLine("Введите число, которое хотите добавить в стек");
                            try
                            {
                                stack.Push(int.Parse(Console.ReadLine()));
                            }
                            catch
                            {
                                Console.WriteLine("Произошла ошибка при поытке добавить элемент в стек, возможно вы ввели не число");
                            }
                            break;
                        }
                    case ConsoleKey.D3:
                    case ConsoleKey.NumPad3:// если нажата клавиша с цифрой 3
                        {
                            stack.Pop();
                            Console.WriteLine("Верхний элемент удалён");
                            break;
                        }
                    case ConsoleKey.D4:
                    case ConsoleKey.NumPad4:// если нажата клавиша с цифрой 4
                        {
                            try { 
                            zadanie(stack);
                            Console.WriteLine("Произведение элементов стека добавлено на дно");
                            }
                            catch (Exception e)
                            {
                                Console.WriteLine($"Произошла ошибка {e.Message}");
                            }
                            break;
                        }
                    default:
                        break;
                }
            }
            while (K.Key != ConsoleKey.Escape);// цикл заканчивается, если нажата клавиша Esc
          

            zadanie(stack);
            Console.WriteLine(stack.ToString());




        }
        static void zadanie(Stack stack)
        {
            int proisved = 1;
            Stack tmpstack = new Stack();
            for (int _ = stack.Pos; _ >= 0; _--)
            {
                proisved *= stack.Val;
                tmpstack.Push(stack.Val);
                stack.Pop();
            }
            stack.Push(proisved);
            for (int _ = tmpstack.Pos; _ >= 0; _--)
            {
                stack.Push(tmpstack.Val);
                tmpstack.Pop();
            }
        }
    }
}


using System;
using System.Collections.Generic;
using System.Data.SqlTypes;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace formulaEvklida
{
    /*
     12. Даны два натуральных числа N и M. Написать рекурсивную функцию для
        поиска наибольшего общего делителя по формуле Евклида.
    */
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("N:");
            int N = int.Parse(Console.ReadLine());
            Console.WriteLine("M:");
            int M = int.Parse(Console.ReadLine());

            Stopwatch swr = new Stopwatch();
            Stopwatch swc = new Stopwatch();
            swr.Start();
            Console.WriteLine(Evklid(N, M));
            swr.Stop();
            Console.WriteLine($"{swr.Elapsed} - время выполнения рекурсией");

            swc.Start();
            Console.WriteLine(cycleEvklid(N, M));
            swc.Stop();
            Console.WriteLine($"{swc.Elapsed} - время выполнения циклом");
        }
        static int Evklid(int n, int m)
        {
            if (n != 0 & m != 0)
            {
                if (n > m) return Evklid(n % m, m);
                else return Evklid(n, m % n);
            }
            else
            {
                if (n == 0) return m;
                else return n;
            }

        }
        static int cycleEvklid(int n, int m)
        {
            int i;
            for (i = minn(n, m);  ((n % i) != 0) | ((m % i) != 0); i--);
            return i;
        }
        static int minn(int n, int m)
        {
            if (n >= m) return m; else return n;
        }
    }
}
