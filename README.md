#include <iostream>
#include <stdlib.h>
#include <windows.h>
#include <conio.h>
#include <locale.h>
#include <wchar.h>
#include <iomanip>
#include <string>

using namespace std;

void pattacks(struct stats,int);
void level_opening();
int player_sorter(stats a, stats b);
//sort(player,player+3,player_sorter);
void clase (string cl, stats &);
void clear_screen();
int movement_lv1();
int getKey();
struct{
	int x=10;
	int y=2;
}player;//for movement

struct stats {
	string nombre;
	int ataque=10;
	int vida=50;
	int defensa=50;
	int velocidad=50;
	int magia=50;
	void (*attack)(stats);//=&pattacks;
}Hero,Karsus,Aballister;;
const short unsigned int Keyleft  = 37; //left
const short unsigned int Keytop   = 38; //up
const short unsigned int Keyright = 39; //right
const short unsigned int Keydown  = 40; //down
const short unsigned int Keyexit  = 81; //q

int main()
{
	int level=1;//va ser extern
	switch(level){
	case 1:

    	level_opening();
    	movement_lv1();
    	for(int i=0;i<10;i++)
        	cout<<"test";

	}
	return 0;
}
void pattacks(struct stats member_b,int mem_num){
	int op, target;
	cin>>op;
	switch(op){
	case 1:
    	cin>>target;
    	//turns[target+1].health-=player.itl*2;
    	break;

	case 2:
    	cin>>target;
        	//member_b[target-1].vida+=member_b.magia*2;
	default:
    	cout<<"Can you pick a number";



	}
}
int player_sorter(stats a, stats b) {
   if(a.velocidad<b.velocidad)
    	return 1;
	else
    	return 0;
}

void level_opening()
{
	setlocale(LC_ALL, "");
	int i=0;
	string cl="0";
	string n;
	system ("color 05" );
	cout << "   Después de una sangrienta pelea contra un dragón en el monte de la oscuridad " << endl;
	cout <<"   Y tras naufragar junto con la tripulacion del barco mientras viajaban por el mar de Marloc"<<endl;
	getch();
	clear_screen();
	cout<<"  	Nuestro héroe por fin ha llegado a tierra"<<endl;
	getch();
	clear_screen();
	cout<<" 	Ahora dime aventurero, ¿cuál es tu nombre?\n\n	";
	cin>>Hero.nombre;
	cout<<"	Perfecto "<<Hero.nombre<<endl;
	getch();
	clear_screen();
	cout<<  	"Recuerdame ¿Que clase de aventurero eres "<<Hero.nombre<<"?"<<endl;
	cout<<endl;
	clase(cl,Hero);
	getch();
	clear_screen();
	cout<<" 	Espero que estés listo para tu próxima aventura"<<endl;
	cout<<" 	..."<<endl;
	Sleep(2000);
	cout<<" 	Porque muy posiblemente sera la ùltima"<<endl;
 	getch();
	clear_screen();
	cout<<" 	Un pequeño flashback viene a la mente de "<<Hero.nombre<<endl;
	cout<<endl;
	cout<<" 	Se encuentra en el barco del que naufragó, cuando uno de sus compañeros,le susurró:"<<endl;
	cout<<endl;
	cout<<"  	'Nuestra vida depende de lo que encontremos en esta isla'"<<endl;
	cout<<endl;
	cout<<" 	Después, todo se vuelve oscuro para nuestro heroe"<<endl;
  	getch();
	clear_screen();
	cout<<" 	Tras caminar unos cuantos días, "<<Hero.nombre<<" se encuentra con 2 viejos conocidos"<<endl;
	cout<<endl;
	cout<<" 	Los valientes aventureros,Karsus Y Aballister"<<endl;
 	getch();
	clear_screen();
	cout<<  	"¡"<<Hero.nombre<<" cuánto tiempo!-exclamó Aballister-después del accidente,Karsus y yo hemos perdido nuestras habilidades"<<endl;
	getch();
	cout<<endl;
	cout<<  	"Ayudanos a escoger cuáles quieres que desarrollemos Aballister y yo"<<endl;
	cout<<endl;
	getch();
	cout<<  	"Recuerda que una vez escogidas no habrá marcha atrás"<<endl;
	cout<<endl;
	getch();
	clear_screen();
	cout<<  	"Entonces dime, ¿cuál es tu elección para Aballister?"<<endl;
	cout<<endl;
	clase(cl,Aballister);
	getch();
	system("cls");
	cout<<  	"¿Y tú elección para Karsus?"<<endl;
	clase(cl,Karsus);
	getch();
	clear_screen();
	cout<<"Perfecto, entonces encontremos lo que veniamos buscando"<<endl;
	getch();
	clear_screen();
	cout<<"Al caminar por varios minutos encuentran un templo antiguo"<<endl;
	cout<<endl;
	cout<<"En la entrada, se encuentra una ornamenta y al lado, un mensaje que dice lo siguiente: "<<endl;
	cout<<endl;
	cout<<"'No existe recompensa alguna, aquel que entre aquí, no lograra salir'"<<endl;
	cout<<endl;
	cout<<"'Bueno podríamos estar muertos'-dijo Karsus-"<<endl;
	cout<<endl;
	cout<<endl;
	cout<<"INICIA LA AVENTURA"<<endl;
}
int movement_lv1(){
	 /** Variables **/
    bool firstIteration=1; /** revisa que sea la primera iteracion y que sucedan las cosas de inicio **/
    char niebla=177; /** valor ascii que representa la niebla **/
    char muro=219; /** valor ascii que representa el muro **/
    char pasillo=255; /** valor ASCII que representa el pasillo pasable plano donde las personas pasan **/
    const short int tamanioX=12; /** Centinela de la matriz en X **/
    const short int tamanioY=12; /** Centinela de la matriz en Y **/

    /** Matriz del mapa real que esta debajo de la niebla, aqui estan todos los datos funcionales del juego **/
    char mapa[tamanioX][tamanioY]={// 0       1       2       3       4       5       6       7       8       9      10      11  /**y**/
             /**x**/    /** 0 **/  muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,
                        /** 1 **/  muro,   muro,pasillo,   muro,   muro,pasillo,pasillo,pasillo,pasillo,   muro,   muro,   muro,
                        /** 2 **/  muro,   muro,pasillo,   muro,   muro,pasillo,pasillo,pasillo,pasillo,   muro,   muro,   muro,
                        /** 3 **/  muro,   muro,pasillo,   muro,   muro,pasillo,   muro,   muro,   muro,   muro,   muro,   muro,
                        /** 4 **/  muro,   muro,pasillo,   muro,   muro,pasillo,   muro,   muro,   muro,   muro,   muro,   muro,
                        /** 5 **/  muro,   muro,pasillo,pasillo,pasillo,pasillo,pasillo,pasillo,pasillo,   muro,   muro,   muro,
                        /** 6 **/  muro,   muro,pasillo,pasillo,pasillo,pasillo,pasillo,pasillo,pasillo,   muro,   muro,   muro,
                        /** 7 **/  muro,   muro,   muro,   muro,   muro,pasillo,   muro,   muro,pasillo,   muro,   muro,   muro,
                        /** 8 **/  muro,   muro,   muro,   muro,   muro,pasillo,   muro,   muro,pasillo,   muro,   muro,   muro,
                        /** 9 **/  muro,   muro,pasillo,pasillo,pasillo,pasillo,   muro,   muro,pasillo,   muro,   muro,   muro,
                        /** 10 **/ muro,   muro,pasillo,pasillo,pasillo,pasillo,   muro,   muro,pasillo,   muro,   muro,   muro,
                        /** 11 **/ muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro,   muro};

    /** c q se ve un desvergue pero esta mamalon **/
    char mapaVisible[tamanioX][tamanioY]={niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,
                                          niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla,niebla};

    /** Vista del jugador a traves de la niebla en su alrededor cuando empieza **/
    if(firstIteration)
    {
        firstIteration=0; /** quita la primera iteracion **/

        /** TO DO **/
        for(int i=0;i<3;i++)
        {
            for(int j=0;j<3;j++)
            {
                mapaVisible[player.x-1+j][player.y-1+i]=mapa[player.x-1+j][player.y-1+i];
            }
        }
        mapaVisible[player.x][player.y]=64; /** /@-representa al jugador en el mapa **/
    }

    /** i es la coordenada y de la impresion de pantalla, j  es la coordenada x de la impresion de pantalla
        y k es el input de la tecla que se guarda como valor entero **/
	int i=0,j=0,k=0;

	while (true)
	{
	    for(i=11;i>=0;i--)
        {
            cout<<endl;
            for(j=0;j<12;j++)
            {
                cout<<mapaVisible[j][i];
            }
        }
		k = getKey();

		switch(k)
		{
            case Keyleft:
            {
                cout <<endl<< "you pressed : left" <<endl;
                try
                {
                    player.x--;
                    if(mapa[player.x][player.y]==muro)
                    {
                        player.x++;
                        throw 1;
                    }
                    for(int i=0;i<3;i++)
                    {
                        for(int j=0;j<3;j++)
                        {
                            mapaVisible[player.x-1+j][player.y-1+i]=mapa[player.x-1+j][player.y-1+i];
                        }
                    }
                    mapaVisible[player.x][player.y]=64;
                    mapaVisible[player.x+1][player.y]=pasillo;
                }
                catch(int e)
                {
                    cout<<endl<<"No se puede salir ;v"<<endl;
                }
            }
            break;
            case Keytop:
            {
                cout << endl<<"you pressed : up" <<endl;
                try
                {
                    player.y++;
                    if(mapa[player.x][player.y]==muro)
                    {
                        player.y--;
                        throw 1;
                    }
                    for(int i=0;i<3;i++)
                    {
                        for(int j=0;j<3;j++)
                        {
                            mapaVisible[player.x-1+j][player.y-1+i]=mapa[player.x-1+j][player.y-1+i];
                        }
                    }
                    mapaVisible[player.x][player.y]=64;
                    mapaVisible[player.x][player.y-1]=pasillo;
                }
                catch(int e)
                {
                    cout<<endl<<"No se puede salir ;v"<<endl;
                }
            }
            break;
            case Keyright:
            {
                cout << endl<<"you pressed : right" <<endl;
                try
                {
                    player.x++;
                    if(mapa[player.x][player.y]==muro)
                    {
                        player.x--;
                        throw 1;
                    }
                    for(int i=0;i<3;i++)
                    {
                        for(int j=0;j<3;j++)
                        {
                            mapaVisible[player.x-1+j][player.y-1+i]=mapa[player.x-1+j][player.y-1+i];
                        }
                    }
                    mapaVisible[player.x][player.y]=64;
                    mapaVisible[player.x-1][player.y]=pasillo;
                }
                catch(int e)
                {
                    cout<<endl<<"No se puede salir ;v"<<endl;
                }
            }
            break;
            case Keydown:
            {
                cout <<endl<< "you pressed : down" <<endl;
                try
                {
                    player.y--;
                    if(mapa[player.x][player.y]==muro)
                    {
                        player.y++;
                        throw 1;
                    }
                    for(int i=0;i<3;i++)
                    {
                        for(int j=0;j<3;j++)
                        {
                            mapaVisible[player.x-1+j][player.y-1+i]=mapa[player.x-1+j][player.y-1+i];
                        }
                    }
                    mapaVisible[player.x][player.y]=64;
                    mapaVisible[player.x][player.y+1]=pasillo;
                }
                catch(int e)
                {
                    cout<<endl<<"No se puede salir ;v"<<endl;
                }
            }
            break;
            default:
                {
                    cout<<endl<<"Tecla No Valida"<<endl;
                }
        };
        Sleep(100);
        clear_screen();
    }
	system("pause");
	return 0;

}
int getKey()
{
	while (true)
	{
    	for(int i = 8; i <= 256; i++)
    	{
        	if(GetAsyncKeyState(i) & 0x7FFF)
        	{
            	//if( ( i >= 37 && i <= 40 ) || i == 81 )
                	return i;
        	}
    	}
	}
}
void clear_screen()
{
  DWORD n;                     	/* Number of characters written */
  DWORD size;                  	/* number of visible characters */
  COORD coord = {0};           	/* Top left screen position */
  CONSOLE_SCREEN_BUFFER_INFO csbi;

  /* Get a handle to the console */
  HANDLE h = GetStdHandle ( STD_OUTPUT_HANDLE );

  GetConsoleScreenBufferInfo ( h, &csbi );

  /* Find the number of characters to overwrite */
  size = csbi.dwSize.X * csbi.dwSize.Y;

  /* Overwrite the screen buffer with whitespace */
  FillConsoleOutputCharacter ( h, TEXT ( ' ' ), size, coord, &n );
  GetConsoleScreenBufferInfo ( h, &csbi );
  FillConsoleOutputAttribute ( h, csbi.wAttributes, size, coord, &n );

  /* Reset the cursor to the top left position */
  SetConsoleCursorPosition ( h, coord );
}

void clase (string cl,stats &Hero){
	cout<<setw(15)<<" Clase"<<setw(15)<<"Ataque"<<setw(15)<<"Defensa"<<setw(15)<<"Vida"<<setw(15)<<"Magia"<<setw(15)<<"Velocidad"<<setw(8)<<"Tecla"<<endl;
	cout<<setw(15)<<" Gladiator"<<setw(15)<<"15"<<setw(15)<<"40"<<setw(15)<<"60"<<setw(15)<<"0"<<setw(15)<<"35"<<setw(8)<<"1"<<endl;
	cout<<setw(15)<<" Rogue"<<setw(15)<<"10"<<setw(15)<<"50"<<setw(15)<<"40"<<setw(15)<<"0"<<setw(15)<<"55"<<setw(8)<<"2"<<endl;
	cout<<setw(15)<<" Priest"<<setw(15)<<"5"<<setw(15)<<"50"<<setw(15)<<"60"<<setw(15)<<"55"<<setw(15)<<"50"<<setw(8)<<"3"<<endl;
	cout<<setw(15)<<" Bard"<<setw(15)<<"10"<<setw(15)<<"55"<<setw(15)<<"50"<<setw(15)<<"50"<<setw(15)<<"0"<<setw(8)<<"4"<<endl;
	cout<<setw(15)<<" Spellcaster"<<setw(15)<<"4"<<setw(15)<<"40"<<setw(15)<<"40"<<setw(15)<<"60"<<setw(15)<<"50"<<setw(8)<<"5"<<endl;
	cout<<endl;

	cout<<"Nota: El ataque normal es de 10, mientras que para las demás estadisticas el valor normal es de 50"<<endl;


	while(cl!="1"&&cl!="2"&&cl!="3"&&cl!="4"&&cl!="5"){
    	cout<<"Introduzca una clase"<<endl;

    	cin>>cl;
    	if(cl!="1"&&cl!="2"&&cl!="3"&&cl!="4"&&cl!="5")
        	continue;

    	int yes=stoi(cl);
    	switch(yes)
    	{
    	case 1:
        	cout<<"Se ha escogido la clase Gladiator"<<endl;
        	Hero.ataque=15;
        	Hero.defensa=40;
        	Hero.vida=60;
        	Hero.magia=0;
        	Hero.velocidad=35;
        	break;
    	case 2:
        	cout<<"Se ha escogido la clase Rogue"<<endl;
        	Hero.ataque=10;
        	Hero.defensa=50;
        	Hero.vida=40;
        	Hero.magia=0;
        	Hero.velocidad=55;
        	break;
    	case 3:
        	cout<<"Se ha escogido la clase Priest"<<endl;
        	Hero.ataque=5;
        	Hero.defensa=50;
        	Hero.vida=60;
        	Hero.magia=55;
        	Hero.velocidad=50;
        	break;
    	case 4:
        	cout<<"Se ha escogido la clase Bard"<<endl;
        	Hero.ataque=10;
        	Hero.defensa=55;
        	Hero.vida=50;
        	Hero.magia=50;
        	Hero.velocidad=0;
        	break;
    	case 5:
        	cout<<"Se ha escogido la clase Spellcaster"<<endl;
        	Hero.ataque=4;
        	Hero.defensa=40;
        	Hero.vida=40;
        	Hero.magia=60;
        	Hero.velocidad=50;
        	break;
    	default:
        	cout<<"Escoge un numero valido"<<endl;
    	}
	}
return ;

}


