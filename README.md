# lab-alineamiento-prot



PRIMERA PARTE



Abrir VMD, ir a pdb y descargar 1AFO.



Abrir extensions, analysis, sequence viewer. Si se hace click en un residuo, ese aparecerá en el modelo tridimensional.




Luego, graphic representet, create rep,  name CA.  Esto es para ver todos los carbonos alfas. Luego, create rep resname PHE. Esto sirve para ver aminoacidos especificos.






apretando el numero 2 en la pantalla donde esta la proteina tridimensional, se puede calcular la distancia entre esos dos atomos.





PARTE 2.



PRoteínas usadas: 2XNE y 1AFO.



Viendo en sequence viewer, vemos que en la proteina 2XNE la alfa helice mas larga esta entre los aminoacidos 230 a 250.



La proteína 1AFO la alfa helice esta entre los aminoacidos 72 y 98.



Luego fui a consola : Extensions ---> Tk console. y ahi puse help.




Luego se pone:     set all [atomselect ID (el id de la proteina que esta en vmd main) "SELECCION"]



En selección va lo que quiero usar, por ejemplo yo puse "protein and resid 72 to 98" para seleccionar la alfa helice de la proteina 1AFO.




todo lo que puse respecto a 1AFO fue:


>Main< (VMD) 2 % set allahuakbar [atomselect 0 "protein and resid 72 to 98"]




atomselect9 (resultado)




>Main< (VMD) 3 % measure center $allahuakbar 




2.311387300491333 -0.8143188953399658 0.7358484864234924 (resultado en coordenadas. El primero es x, el segundo y y el tercero z)




>Main< (VMD) 4 % measure minmax $allahuakbar





{-20.533000946044922 -16.20800018310547 -16.91200065612793} {22.46500015258789 11.418000221252441 16.139999389648438} (resultado de la localizacion verdadera de la proteina. Los primeros 3 valores son desde el eje hacia arriba y los otros 3 desde el eje hacia abajo, pór lo que sumando los valores absolutos tenemos el espacio total ocupado por la proteina).





>Main< (VMD) 5 % eval vecadd [$allahuakbar get charge]




0.0 (esto da la carga neta, como es 0 indica carga neutra.).






posteriormente, use: 



>Main< (VMD) 6 % set kakaroto [atomselect 1 "protein and resid 230 to 250"]




atomselect10




>Main< (VMD) 7 % measure center $kakaroto




19.23552131652832 -42.01963806152344 -12.19515323638916




>Main< (VMD) 8 % measure minmax $kakaroto




{9.098999977111816 -56.18199920654297 -24.64299964904785} {26.27199935913086 -28.45199966430664 -0.2770000100135803}




>Main< (VMD) 9 % eval vecadd [$kakaroto get charge]




0.0




>Main< (VMD) 10 % 




Luego, seleccione a la proteina 1AFO:  esto es para centrar a la proteina



>Main< (VMD) 10 % set allahuakbar [atomselect 0 "all"]




atomselect11




>Main< (VMD) 11 % $allahuakbar moveby [vecinvert [measure center $allahuakbar]





Luego use a la 2XNE:


>Main< (VMD) 12 % set kakaroto [atomselect 1 "all"]




atomselect12




>Main< (VMD) 13 % $kakaroto moveby [vecinvert [measure center $kakaroto]]




Asi quedaron las dos centradas





DESPUES para volver a seleccionar los atomos de las alfas helices, puse:



>Main< (VMD) 16 % set allahuakbar [atomselect 0 "chain A and name CA and resid 72 to 99"]




atomselect13





>Main< (VMD) 17 % $allahuakbar num




28




>Main< (VMD) 18 % set kakaroto [atomselect 1 "name CA and resid 230 to 250"]




atomselect14




>Main< (VMD) 19 % $kakaroto num




21







Luego, para calcular el RMSD ambas selecciones DEBEN tener el mismo numero de atomos, por lo que use esto:




>Main< (VMD) 21 % set allahuakbar [atomselect 0 "chain A and name CA and resid 75 to 85"]




atomselect15




>Main< (VMD) 22 % set kakaroto [atomselect 1 "chain A and name CA and resid 235 to 245"]




atomselect16




>Main< (VMD) 23 % measure rmsd $allahuakbar $kakaroto




16.17098617553711





Luego, use:



>Main< (VMD) 24 % set transformation_matrix [measure fit $allahuakbar $kakaroto]




{0.017742440104484558 0.9216606020927429 -0.3875911831855774 0.3710159659385681} {0.8243417143821716 -0.23285804688930511 -0.515982449054718 -3.064300775527954} {-0.5658144354820251 -0.31035277247428894 -0.7638947367668152 -8.250924110412598} {0.0 0.0 0.0 1.0}




>Main< (VMD) 25 % set allahuakbar [atomselect 0 "all"]




atomselect17




>Main< (VMD) 26 % $allahuakbar move $transformation_matrix



ahi quedaron las dos solapadas. El transformation matrix se usa para solapar a las proteinas, las rota y las encaja.






SEGUNDA PARTE 15/11/2017






Hoy trabajaremos con la proteína (PDB) 3OTJ.





En un archivo PDB los datos provienen de un experimento de cristalografía. GEneralmente la técnica suele fallar, por lo que aveces los alineamientos parten por un residuo en una posicion >1.





PAra seleccionar los átomos de una cadena especifica se hace:




Save trajectory (en MAIN del VMD), luego se escribe en sleected atoms Chain A (o la que sea) y se le da a Save y escoger destino.






PAra llegar a Save trajectory, hacemos click en la proteína en VMD Main y click derecho ---> Save coordenates.






Tambien se puede exribir "chain E and name CA" sin comillas.





Grafico de Ramachandran define los residuos que formaran parte de una determinada estructura espacial : laminas beta, alfa helice...






PAra ir a grafico de ramachandran, es en Extensions ---> ramachandran....





Buscar 3 serine proteasas más y guardar la cadena que corresponde a esas serine proteasas.




Usé 1SBT (cadena A), 1AGS (cadenas A,B) y 2SGA (Cadena A).





Para 2SGA usé el comando chain A and protein para sacarle el agua. Se usa and protein para dejar solo la proteina.



Luego de curar a las proteinas (archivos correo) vamos a etensions y a multiseq.



Luego, escojo una region y la mnarco y apreto tool y luego stamp alignment y pongo selected regions , en scanscore puse 2 y en el de abajo puse 5. Este programa rota y centra automaticamente y esto define para la region que selecicone (que creo que esta conservada).



