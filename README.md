# Tarea-Semana-11
using System;
using System.Collections.Generic;

public class Traductor
{
    private Dictionary<string, string> diccionario = new Dictionary<string, string>
    {
        {"time", "tiempo"},
        {"person", "persona"},
        {"year", "año"},
        {"way", "camino/forma"},
        {"day", "día"},
        {"thing", "cosa"},
        {"man", "hombre"},
        {"world", "mundo"},
        {"life", "vida"},
        {"hand", "mano"},
        {"part", "parte"},
        {"child", "niño/a"},
        {"eye", "ojo"},
        {"woman", "mujer"},
        {"place", "lugar"},
        {"work", "trabajo"},
        {"week", "semana"},
        {"case", "caso"},
        {"point", "punto/tema"},
        {"government", "gobierno"},
        {"company", "empresa/compañía"}
    };

    public void TraducirFrase()
    {
        Console.Write("Ingrese la frase: ");
        string frase = Console.ReadLine().ToLower();

        string[] palabras = frase.Split(' ');
        List<string> fraseTraducida = new List<string>();

        foreach (string palabra in palabras)
        {
            if (diccionario.ContainsKey(palabra))
            {
                fraseTraducida.Add(diccionario[palabra]);
            }
            else
            {
                // Intenta buscar la palabra en español en el diccionario
                bool encontrada = false;
                foreach (var kvp in diccionario)
                {
                    if (kvp.Value.Contains(palabra))
                    {
                        fraseTraducida.Add(kvp.Key);
                        encontrada = true;
                        break;
                    }
                }
                if (!encontrada)
                {
                    fraseTraducida.Add(palabra);
                }
            }
        }

        Console.WriteLine("Su frase traducida es: " + string.Join(" ", fraseTraducida));
    }

    public void AgregarPalabra()
    {
        Console.Write("Ingrese la palabra en inglés: ");
        string ingles = Console.ReadLine().ToLower();

        Console.Write("Ingrese la traducción en español: ");
        string espanol = Console.ReadLine().ToLower();

        diccionario[ingles] = espanol;
        Console.WriteLine("Palabra agregada al diccionario.");
    }

    public void Menu()
    {
        while (true)
        {
            Console.WriteLine("\nMENU");
            Console.WriteLine("=======================================================");
            Console.WriteLine("1. Traducir una frase");
            Console.WriteLine("2. Ingresar más palabras al diccionario");
            Console.WriteLine("0. Salir");
            Console.Write("Seleccione una opción: ");

            string opcion = Console.ReadLine();

            switch (opcion)
            {
                case "1":
                    TraducirFrase();
                    break;
                case "2":
                    AgregarPalabra();
                    break;
                case "0":
                    return;
                default:
                    Console.WriteLine("Opción inválida.");
                    break;
            }
        }
    }

    public static void Main(string[] args)
    {
        Traductor traductor = new Traductor();
        traductor.Menu();
    }
}
