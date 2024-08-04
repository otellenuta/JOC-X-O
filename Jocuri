int[,] tabla = new int[3,3]; 
 
while (VerificaCastig(tabla) == 0) //ciclul while, atat timp cat functia VerificaCastig returneaza 0, intram in functia MiscareJucator 1/2
{
    MiscareJucator(tabla, 1);
    if (VerificaCastig(tabla) != 0 || JocFinisat(tabla))
        break; //daca dupa prima miscare, functia VerificaCastig returneaza != 0 sau functia JosFinisat returneaza true, jocul se finiseaza.
    MiscareJucator(tabla, 2);
}
 
 
static int VerificaCastig(int[,] tabla) //Functia VerificaCastig, unde se verifica randuri, coloane, diagonale
{
    bool verificare = false;
    //verificam randurile   
    for (int i = 0; i < tabla.GetLength(0); i++)
    {
        verificare = true;  //se va reseta conditia true la fiecare rand!!!
        for (int j = 0; j < tabla.GetLength(1) - 1; j++)
        {
            if (tabla[i, j] != tabla[i, j+1])
            {
                verificare = false;                
            }           
        }
        if (verificare == true && tabla[i, 0] != 0)
        {
            Console.WriteLine("Jucatorul " + TransformaXsau0(tabla[i, 0]) + " a castigat!");
            return tabla[i,0];
        }
    }
 
    //Verificam coloanele
    for (int j = 0; j < tabla.GetLength(1); j++)
    {
        verificare = true;  //se va reseta conditia true la fiecare coloana!!!
        for (int i = 0; i < tabla.GetLength(0)-1; i++)
        {
            if (tabla[i, j] != tabla[i + 1, j])
            {
                verificare = false;
            }
        }
        if (verificare == true && tabla[0, j] != 0)
        {
            Console.WriteLine("Jucatorul " + TransformaXsau0(tabla[0, j]) + " a castigat!");
            return tabla[0, j];
        }
    }
 
    
    while (TablaPatrata(tabla)) //initial vom verifica daca tabla corespunde cerintelor lungime=latime, ca sa putem controla diagonalele
    {
        //verificam diagonala principala
        verificare = true; //se va reseta conditia true initial pentru diagonala!!!
        for (int i = 0; i < tabla.GetLength(0) - 1; i++)
        {
            if (tabla[i, i] != tabla[i + 1, i + 1])
            {
                verificare = false;
                break; //daca gasim o divergenta, iesim din ciclu.
            }
        }
        if (verificare == true && tabla[tabla.GetLength(0) - 1, tabla.GetLength(0) - 1] != 0)
        {
            Console.WriteLine("Jucatorul " + TransformaXsau0(tabla[0, 0]) + " a castigat!");
            return tabla[0, 0];
        }
 
        //verificam diagonala secundara
        verificare = true; //se va reseta conditia true initial pentru diagonala secundara!!!
        for (int i = 0; i < tabla.GetLength(0) - 1; i++)
        {
            if (tabla[i, tabla.GetLength(0) - i - 1] != tabla[i + 1, tabla.GetLength(0) - (i + 1) - 1])
            {
                verificare = false;
                break; //daca gasim o divergenta iesim din ciclu.
            }
        }
        if (verificare == true && tabla[tabla.GetLength(0) - 1, 0] != 0)
        {
            Console.WriteLine("Jucatorul " + TransformaXsau0(tabla[0, tabla.GetLength(0) - 1]) + " a castrigat!");
            return tabla[0, tabla.GetLength(0) - 1];
        }
        break;
    }
    return 0; //in cazul ca nu a fost depistat castigatorul.
}
 
static bool TablaPatrata(int[,] tabla) //Functie pentru a concretiza daca tabla este patrata, lungimea = latimea, pentru a verifica diagonalele, de altfel se vor verifica numai randurile si coloanele.
{
    if(tabla.GetLength(0) != tabla.GetLength(1))
    {
        return false; //daca lungimile sunt diferite, lungime != latime, returneaza false.
    }    
    return true;
}   
 
 
void MiscareJucator(int[,] tabla, int jucator)//functia nu returneaza nimic!!!                                                  //Functia MiscareJucator unde:
{                                                                                                                               //utilizatorul primeste un mesaj ca sa introduca randul sau coloana,                                                                                                                                                          
    int rand, coloana;                                                                                                          //dupa care acestea se controleaza sa fie in limitele tablii,                                                                                                    
    do                                                                                                                          //dupa care vom controla daca e libera celula, vom afisa tabla dupa fiecare miscare
    {                                                                                                                           //vom controla daca mai sunt celule libere, daca nu - jocul se finiseaza.
        Console.WriteLine("Jucatorul " + jucator + ", introduceti randul si coloana la care vreti sa plasati caracterul");  
        GetRandSiColoana(out rand, out coloana); 
 
        //daca valorile introduse pentru rand si coloana se afla in afara limitelor, afisam valori invalide si reluam ciclul do-while
        if (rand >= tabla.GetLength(0) || coloana >= tabla.GetLength(1))
        {
            Console.WriteLine("Valori invalide, mai incearca!");
            continue;
        }
        //daca functia AdaugaXSauO permite a ocupa o celula atunci finisam ciclul do-while
        if (AdaugaXSauO(tabla, jucator, rand, coloana))
        {
            break;
        }
    }
    while (true);   //Condiția care este evaluată după executarea blocului de cod. Dacă această condiție este adevărată (true), blocul de cod va fi executat din nou.
    AfiseazaTabla(tabla); //dupa fiecare celula ocupata afisam tabla
 
    while (JocFinisat(tabla)) //daca functia JocFinisat returneaza true, vom afisa mesajul de mai jos si iesim din ciclu while
    {
        Console.WriteLine("Miscarile s-au finisat!");
        Console.WriteLine();
        Console.WriteLine("JOC FINISAT!");
        Console.WriteLine();
        return;    //iesi din functie.       
    }
}
 
 
void GetRandSiColoana(out int rand, out int coloana)//Functie GetRandSiColoana nu returneaza nimic!!!
                                                    //vom permite utilizatorului sa introduca randul si coloana
{
    rand = int.Parse(Console.ReadLine());
    coloana = int.Parse(Console.ReadLine());
}
 
 
static bool AdaugaXSauO(int[,] tabla, int caracter, int rand, int coloana) //functie unde controlez celula goala, in caz contrar afisez "pozitia ocupata"
{   
    if (tabla[rand, coloana] == 0)
    {
        tabla[rand, coloana] = caracter;
        return true;
    }
    else 
    { //verific daca mai sunt celule libere si afisez posibilitatea de a mai incerca odata!
        for (int i = 0; i < tabla.GetLength(0); i++)
        {
            for (int j = 0; j < tabla.GetLength(1); j++)
            {
                if (tabla[i, j] == 0)
                {
                    Console.WriteLine("Pozitie ocupata, mai incearca!");
                    Console.WriteLine();
                    return false;
                }               
            }                      
        }           
    }
    return false;
}
 
 
static char TransformaXsau0(int numar) //Functie TransformaXsau0 care transforma din 1 in x si 2 in O pentru a afisa castigatorul
{
    if (numar == 1)
    {
        return 'X';
    }
    if (numar == 2)
    {
        return 'O';
    }
    return '-';
}
 
 
static bool JocFinisat(int[,] tabla) //functie care ar merge prin toate celulele si daca toate sunt ocupate sa nu mai ofere posibilitatea de a pune valori noi
{
    bool jocfinisat = true;
    for (int i = 0; i < tabla.GetLength(0); i++)
    {
        for (int j = 0; j < tabla.GetLength(1); j++)
        {
            if (tabla[i, j] == 0)
            {
                return false;
            }
        }                  
    }
    if (jocfinisat == true)
    {        
        Console.WriteLine();
    }
    return true;
}
 
 
static void AfiseazaTabla(int[,] tabla) // Afisarea tablii: 0 - celula goala; 1 - X; 2 - O;
{
    for (int i = 0; i < tabla.GetLength(0); i++)
    {       
        for (int j = 0; j < tabla.GetLength(1); j++)
        {
            if (tabla[i, j] == 0 )
            {
                Console.Write(" ");
            }
            else if (tabla[i, j] == 1)
            {
                Console.Write("X");
            }
            else if (tabla[i, j] == 2)
            {
                Console.Write("O");
            }
            if (j < tabla.GetLength(1) - 1)
            {
                Console.Write("|");
            }
        }
        Console.WriteLine();
        if (i < tabla.GetLength(0) - 1)
        {
            for (int k = 0;  k < tabla.GetLength(1) * 2 - 1;  k++)
            {
                Console.Write("-");
            }
        }
        Console.WriteLine();
    }
}
