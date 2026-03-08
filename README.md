# Actividad-de-evidencia-2_U2-Singleton


## Codigo    


````csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace _2_U2_Singleton
{
    public class Central_911
    {
        private static Central_911 _instance;
        private static readonly object _lock = new object();
        public string Central { get; private set; }
        private Central_911()
        {
            Central = "Central 911";
        }
        public static Central_911 Obtener_Instancia()
        {
            if(_instance==null)
            {
                lock(_lock)
                {
                    if(_instance==null)
                    {
                        _instance = new Central_911();
                    }
                }
            }
            return _instance;
        }

        public void ConectarLlamadas(Operador operador, string tipoEmergencia)
        {
            Console.WriteLine("\nLlamada conectada con el operador " + operador.Nombre);
            operador.AtiendeEmergencia(tipoEmergencia);
        }
        public class Operador
        {
            public int Id_Operador { get; set; }
            public string Nombre { get; set; }
            public Operador(int id, string nombre)
            {
                Id_Operador = id;
                Nombre = nombre;
            }
            public void AtiendeEmergencia(string tipoEmergencia)
            {
                Console.WriteLine($"Operador {Nombre} atendiendo emergencia de tipo: {tipoEmergencia} ");
                switch (tipoEmergencia)
                {
                    case "Intento de suicidio":
                        Console.WriteLine("Enviando unidades de apoyo y rescate");
                        break;
                    case "Incendio":
                        Console.WriteLine("Enviando bomberos");
                        break;
                    case "Accidente":
                        Console.WriteLine("Enviando paramedicos y oficiales");
                        break;
                    case "Violeta":
                        Console.WriteLine("Enviando una patrulla");
                        break;
                    case "Robo":
                        Console.WriteLine("Enviando patrulla");
                        break;
                    case "Medica":
                        Console.WriteLine("Enviando ambulancia y paramedicos");
                        break;
                    default:
                        Console.WriteLine("Tipo de emergencia no reconocido");
                        break;
                }
            }
            internal class Program
            {
                static void Main(string[]args)
                {
                    Central_911 Llamada1 = Central_911.Obtener_Instancia();
                    Central_911 Llamada2 = Central_911.Obtener_Instancia();
                    Central_911 Llamada3 = Central_911.Obtener_Instancia();
                    Central_911 Llamada4 = Central_911.Obtener_Instancia();

                    Operador op1 = new Operador(1, "Laura");
                    Operador op2 = new Operador(2, "Carlos");
                    Operador op3 = new Operador(3, "Juan");
                    Operador op4 = new Operador(4, "Maria");

                    Llamada1.ConectarLlamadas(op1, "Incendio");
                    Llamada2.ConectarLlamadas(op2,"Violeta");
                    Llamada1.ConectarLlamadas(op1, "Accidente");
                    Llamada2.ConectarLlamadas(op2, "Intento de suicidio");
                    Llamada3.ConectarLlamadas(op3, "Robo");
                    Llamada4.ConectarLlamadas(op4, "Medica");

                    Console.WriteLine("\nReferenceEquals: " + ReferenceEquals(Llamada1, Llamada2));

                    Console.ReadKey();
                }
            }
        }
    }
}

````
