# proyecto-introduccion-ciencias-de-la-computacion
proyecto de programacion de una aplicacion que te dira que entrenar y se podra llevar un registro y c0ontrol de las calorias consumidas diarias 
from tkinter import *
from tkinter import messagebox
from random import random
import numpy as np
import sqlite3

#_________________________funcion conexion base de datos_______________

def conexionBBDD():
    
    miConexion=sqlite3.connect('Informacion')
    miCursor=miConexion.cursor()
    
    try:
        miCursor.execute('''
                    CREATE TABLE Alimentos(
                    ID INTEGER PRIMARY KEY AUTOINCREMENT,
                    NOMBRE_ALIMENTO VARCHAR(50) UNIQUE,
                    CANTIDAD INTEGER,
                    CALORIAS INTEGER,
                    COMENTARIOS VARCHAR(100))
                 ''')    
        messagebox.showinfo("BBDD","Base creada con exito")

    except:
        
        messagebox.showwarning("!!Atencion ","la base de datos ya existe")
        
#_________________________ funcion crear base alimentos diarios________

#_________________________funcion conexion base de datos_______________

def conexionAli():
    
    miConexion=sqlite3.connect('misAlimentos')
    miCursor=miConexion.cursor()
    
    try:
        miCursor.execute('''
                    CREATE TABLE Alimentos(
                    ID INTEGER PRIMARY KEY AUTOINCREMENT,
                    NOMBRE_ALIMENTO VARCHAR(50) UNIQUE,
                    CANTIDAD INTEGER,
                    CALORIAS INTEGER,
                    COMENTARIOS VARCHAR(100))
                 ''')    
        messagebox.showinfo("BBDD","Base creada con exito")

    except:
        
        messagebox.showwarning("!!Atencion ","la base de datos ya existe")        
#____________________________suma comida diaria___________________________

miConexion=sqlite3.connect('misAlimentos')

miCursor=miConexion.cursor()


#lista con los articulos que cumplen
miCursor.execute("SELECT * FROM Alimentos")

losalimentos=miCursor.fetchall()


def resultado1():
    result=0
    for i in range(0,len(losalimentos)):
        result= result + (losalimentos[i][3])*(losalimentos[i][2])
    return result

def resultado():
    messagebox.showinfo('resultado','hoy llevas '+' '+ str(resultado1()) + ' '  + 'calorias')
#____________________________funcion limpiar campos_________________________

def limpiarCampos():
    
    elalimento.set("")
    lacantidad.set("")
    lascalorias.set("")
    cuadroTexto4.delete(1.0, END)
        
#_____________________________ funcion crear dato en la base________________

def crear():
    miConexion=sqlite3.connect("Informacion")
    miCursor=miConexion.cursor()
    miCursor.execute("INSERT INTO Alimentos VALUES(NULL,'" + elalimento.get()+
                     "','" +  lacantidad.get() + 
                     "','" +  lascalorias.get() + 
                     "','" +  cuadroTexto4.get("1.0", END) + "')") 
    miConexion.commit()
    messagebox.showinfo("BBDD", "Registro creado con exito")
                     
#_________________________________ agregar comida de hoy __________________

def agregarcomidadehoy():
    miConexion=sqlite3.connect("misAlimentos")
    miCursor=miConexion.cursor()
    miCursor.execute("INSERT INTO Alimentos VALUES(NULL,'" + elalimento.get()+
                     "','" +  lacantidad.get() + 
                     "','" +  lascalorias.get() + 
                     "','" +  cuadroTexto4.get("1.0", END) + "')") 
    miConexion.commit()
    messagebox.showinfo("BBDD", "Registro creado con exito")   
#_______________________________ funcion leer datos en la base ____________

def leer():
    miConexion=sqlite3.connect("Informacion")
    miCursor=miConexion.cursor()
    miCursor.execute("select* from Alimentos WHERE NOMBRE_ALIMENTO='" + elalimento.get() + "'")
    
    lavariable=miCursor.fetchall()
    
    for variable in lavariable:
        elalimento.set(variable[1])
        lacantidad.set(variable[2])
        lascalorias.set(variable[3])
        cuadroTexto4.insert(1.0, variable[4])
        
    miConexion.commit()   
        
#________________________________ funcion piernas__________________________


A=['sentadilla profunda','sancadas','puentes','elevacion de talones','sentadillas abiertas']

def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4
    return res

y= random()
z= random()
x= random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(z):
    z=random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(x) or  eleccionpartedelcuerpo(x)==eleccionpartedelcuerpo(z):
    x=random()

m=A[eleccionpartedelcuerpo(y)]
n=A[eleccionpartedelcuerpo(z)]
l=A[eleccionpartedelcuerpo(x)]

   


def infopierna():
    messagebox.showinfo('piernas','hoy vamos a entrenar '+' '+str(m)+' '+','+''+' '+str(n)+' '+'y'+''+' '+str(l))

#_________________________________________funcion brazos______________________
B=['flexiones de pecho', 'extension de tripceps','elevacion lateral de hombros','flexiones inversas apoyada en silla','press']

def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4
    return res

y= random()
z= random()
x= random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(z):
    z=random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(x) or  eleccionpartedelcuerpo(x)==eleccionpartedelcuerpo(z):
    x=random()

o=B[eleccionpartedelcuerpo(y)]
p=B[eleccionpartedelcuerpo(z)]
q=B[eleccionpartedelcuerpo(x)]




def infobrazos():
    messagebox.showinfo('brazos','hoy vamos a entrenar '+' '+str(o)+' '+','+''+' '+str(p)+' '+'y'+''+' '+str(q))

#____________________________________funcion abdomen______________________________ 
C=['raton','abdominales normales','elevacion de piernas','peso lado a lado','planchas ' ]

def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4
    return res

y= random()
z= random()
x= random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(z):
    z=random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(x) or  eleccionpartedelcuerpo(x)==eleccionpartedelcuerpo(z):
    x=random()

abd1=C[eleccionpartedelcuerpo(y)]
abd2=C[eleccionpartedelcuerpo(z)]
abd3=C[eleccionpartedelcuerpo(x)]


def infoabd():
    messagebox.showinfo('abdomen','hoy vamos a entrenar '+' '+str(abd1)+' '+','+''+' '+str(abd2)+' '+'y'+''+' '+str(abd3))
#________________________funcion lumbares ___________________________________

D=['superman','peso muerto','canoa','superman lado a lado ','flexion de espalda']

def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4
    return res

y= random()
z= random()
x= random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(z):
    z=random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(x) or  eleccionpartedelcuerpo(x)==eleccionpartedelcuerpo(z):
    x=random()

lum1=D[eleccionpartedelcuerpo(y)]
lum2=D[eleccionpartedelcuerpo(z)]
lum3=D[eleccionpartedelcuerpo(x)]

def infolum():
    messagebox.showinfo('lumbares','hoy vamos a entrenar '+' '+str(lum1)+' '+','+''+' '+str(lum2)+' '+'y'+''+' '+str(lum3))
#____________________________funcion gluteos__________________________________
    
E=['zancada lateral','zancadas silla','patadas de gluteo','puente','Zancadas Caminando']

def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4
    return res

y= random()
z= random()
x= random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(z):
    z=random()

while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(x) or  eleccionpartedelcuerpo(x)==eleccionpartedelcuerpo(z):
    x=random()

glu1=E[eleccionpartedelcuerpo(y)]
glu2=E[eleccionpartedelcuerpo(z)]
glu3=E[eleccionpartedelcuerpo(x)]


def infoglu():
    messagebox.showinfo('gluteos','hoy vamos a entrenar '+' '+str(glu1)+' '+','+''+' '+str(glu2)+' '+'y'+''+' '+str(glu3))

#____________________________________funcion cardio______________________
cardio=['burpees','saltar lazo','trotar','montar bicicleta','escaladores cruzados']

def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4  
    return res

y= random()

cardio1=cardio[eleccionpartedelcuerpo(y)]

def infocardio():
    messagebox.showinfo('cardiovascular','hoy vamos a entrenar '+' '+str(cardio1))

#_________________________________________________________________________
raiz = Tk()
raiz.title('entrenador personal')
#raiz.resizable(0,0) no se puede redimencionar 
raiz.iconbitmap('D:/Esperanza/Escritorio/proy/logo2.ico')
raiz.geometry('720x550')
raiz.config(bg='black')
raiz.config(bd=10)
raiz.config(relief='groove')
raiz.config(cursor='hand2')
barraMenu=Menu(raiz)
raiz.config(menu=barraMenu)




miFrame=Frame()

miFrame.pack()
#miFrame.pack(side='right', anchor='s')
#miFrame.pack(side='right', anchor='s')
miImagen=PhotoImage(file='D:/Esperanza/Escritorio/proy/entrenar.png')

miotroLabel=Label(miFrame, image=miImagen)
miotroLabel.place(x=20, y=50)
miFrame.config(bg='pink')
miFrame.config(width='650', height='500')
miFrame.config(bd=15)
miFrame.config(relief='groove')
miFrame.config(cursor='pirate')

miLabel=Label(miFrame, text ='hola , es momento de entrenar!!',font=('Comic Sans MS',18))
miLabel.grid(row=1,column=0)
#miLabel.place(x=100, y=10)

elalimento=StringVar()
lacantidad=StringVar()
lascalorias=StringVar()

cuadroTexto=Entry(miFrame,textvariable=elalimento)
#el texvariable el para que el cuadro este asociado con el valor de la variable 
#y el valor de esa variable la asignamos al pulsar el botton
cuadroTexto.grid(row=2,column=1)
cuadroTexto.config(fg='purple')


nombrelabel=Label(miFrame, text='Alimento:')
nombrelabel.grid(row=2,column=0,sticky='e',pady= 5)


cuadroTexto2=Entry(miFrame,textvariable=lacantidad)
cuadroTexto2.grid(row=3,column=1)

nombre2label=Label(miFrame, text='Cantidad:')
nombre2label.grid(row=3,column=0,sticky='e',pady= 5)

cuadroTexto3=Entry(miFrame,textvariable=lascalorias)
cuadroTexto3.grid(row=4,column=1)

nombre3label=Label(miFrame, text='Calorias')
nombre3label.grid(row=4,column=0,sticky='e',pady= 5)
#nombre3label.config(show="*")

cuadroTexto4=Text(miFrame, width=16, height=5)
cuadroTexto4.grid(row=5,column=1)



scrollvert=Scrollbar(miFrame, command=cuadroTexto4.yview)
scrollvert.grid(row=5,column=2,sticky='nsew')
cuadroTexto4.config(yscrollcommand=scrollvert.set)

nombre4label=Label(miFrame, text='comentarios')
nombre4label.grid(row=5,column=0,sticky='e',pady= 5)

def codigoBoton():
    
    minombre.set('daniela')
    #set es para asignarle un valor a una variable
    #get para tener informacion de un cuadro de texto


miprimerboton=Button(miFrame, text='resultado',height=2,width=10,command=resultado)
miprimerboton.grid(row=5,column=0)
botonagregar=Button(miFrame, text='agregar',height=2,width=10,command=crear)
botonagregar.grid(row=6,column=1)
botonaleer=Button(miFrame, text='leer',height=2,width=10,command=leer)
botonaleer.grid(row=7,column=1)
botonaagregarcomida=Button(miFrame, text='agregar comida de hoy',height=2,width=18,command=agregarcomidadehoy)
botonaagregarcomida.grid(row=8,column=1)
operacion=''

resultado=0

#______________pantalla____________________________________

numeroPantalla=StringVar()

pantalla=Entry(miFrame, textvariable=numeroPantalla)
pantalla.grid(row=6,column=2,padx=10, pady=10, columnspan=4)
pantalla.config(background='black', fg="#03f949")

#___________pulsaciones teclado

def numeroPulsado(num):
    global operacion 
    
    if operacion !='':
        
        numeroPantalla.set(num)
        operacion=''
    else:
        numeroPantalla.set(numeroPantalla.get()+num)
    
#_____________________  funcion suma ________

def suma(num):
    
    global operacion
    global resultado
    
    resultado= resultado + int(num)
    operacion='suma'
    
    numeroPantalla.set(resultado)
    
#_____________________ funcion el_resultado  ________    

def el_resultado():
    
    global resultado
    
    numeroPantalla.set(resultado + int(numeroPantalla.get()))
    resultado=0

#_______________fila1 __________________________
boton7=Button(miFrame, text='7',width=3,command=lambda:numeroPulsado('7'))
boton7.grid(row=7,column=2)
boton8=Button(miFrame, text='8',width=3,command=lambda:numeroPulsado('8'))
boton8.grid(row=7,column=3)
boton9=Button(miFrame, text='9',width=3,command=lambda:numeroPulsado('9'))
boton9.grid(row=7,column=4)
botondiv=Button(miFrame, text='/',width=3)
botondiv.grid(row=7,column=5)
#_______________fila2 __________________________
boton4=Button(miFrame, text='4',width=3, command=lambda:numeroPulsado('4'))
boton4.grid(row=8,column=2)
boton5=Button(miFrame, text='5',width=3,command=lambda:numeroPulsado('5'))
boton5.grid(row=8,column=3)
boton6=Button(miFrame, text='6',width=3,command=lambda:numeroPulsado('6'))
boton6.grid(row=8,column=4)
botonmult=Button(miFrame, text='x',width=3)
botonmult.grid(row=8,column=5)

#_______________fila3 __________________________
boton1=Button(miFrame, text='1',width=3,command=lambda:numeroPulsado('1'))
boton1.grid(row=9,column=2)
boton2=Button(miFrame, text='2',width=3,command=lambda:numeroPulsado('2'))
boton2.grid(row=9,column=3)
boton3=Button(miFrame, text='3',width=3,command=lambda:numeroPulsado('3'))
boton3.grid(row=9,column=4)
botonrest=Button(miFrame, text='-',width=3)
botonrest.grid(row=9,column=5)


#_______________fila4 __________________________
boton0=Button(miFrame, text='0',width=3,command=lambda:numeroPulsado('0'))
boton0.grid(row=10,column=2)
botonigual=Button(miFrame, text='=',width=3,command=lambda:el_resultado())
botonigual.grid(row=10,column=3)
botoncoma=Button(miFrame, text=',',width=3,command=lambda:numeroPulsado(','))
botoncoma.grid(row=10,column=4)
botonsuma=Button(miFrame, text='+',width=3,command=lambda:suma(numeroPantalla.get()))
botonsuma.grid(row=10,column=5)

#________________________________

#varOpcion=IntVar()
#def imprimir():
    
    #print(varOpcion.get())
    
#    if varOpcion.get() == 1:
#        etiqueta.config(text='vamos a tener un entrenamiento largo')
#    else:
#        etiqueta.config(text='vamos a tener un entrenamiento corto y muy eficiente')
        
#otroLabel=Label(miFrame, text='tienes suficiente tiempo para entrenar?')    
#otroLabel.grid(row=11,column=0) 

#Radioboton1=Radiobutton(miFrame, text= 'si', variable=varOpcion, value=1, command=imprimir)
#Radioboton1.grid(row=12,column=0)
#Radioboton2=Radiobutton(miFrame, text= 'no', variable=varOpcion, value=2, command=imprimir)
#Radioboton2.grid(row=13,column=0)

#etiqueta=Label(miFrame)
#etiqueta.grid(row=14,column=0)
#____________________________________________________

miLabelchek=Label(miFrame, text= "que entrenaste ayer?", width=20)
miLabelchek.grid(row=8,column=0)


gluteos=IntVar()
brazos=IntVar()
piernas=IntVar()
abdominales=IntVar()
lumbares=IntVar()

def opcionescuerpo():
    
    opcionEscogida=""
    
    if(gluteos.get()==1):
        opcionEscogida = opcionEscogida +  "gluteos"
    if(brazos.get()==1):
        opcionEscogida = opcionEscogida +  "brazos"
    if(piernas.get()==1):
        opcionEscogida = opcionEscogida +  "piernas"
    if(abdominales.get()==1):
        opcionEscogida = opcionEscogida +  "abdominales"
    if(lumbares.get()==1):
        opcionEscogida = opcionEscogida +  "lumbares"
        
    textoFinal.config(text=opcionEscogida)  

michekbutton1=Checkbutton(miFrame, text="gluteos", variable=gluteos, onvalue=1, offvalue=0,command=opcionescuerpo)
michekbutton1.grid(row=9,column=0)
michekbutton2=Checkbutton(miFrame, text="brazos", variable=brazos, onvalue=1, offvalue=0,command=opcionescuerpo)
michekbutton2.grid(row=10,column=0)
michekbutton3=Checkbutton(miFrame, text="piernas", variable=piernas, onvalue=1, offvalue=0,command=opcionescuerpo)
michekbutton3.grid(row=11,column=0)
michekbutton4=Checkbutton(miFrame, text="abdominales", variable=abdominales, onvalue=1, offvalue=0,command=opcionescuerpo)
michekbutton4.grid(row=12,column=0)
michekbutton5=Checkbutton(miFrame, text="lumbares", variable=lumbares, onvalue=1, offvalue=0,command=opcionescuerpo)
michekbutton5.grid(row=13,column=0)


textoFinal=Label(miFrame)
textoFinal.grid(row=14,column=0)


#_____________________________________________________
#__________funcion parte del cuerpo
a='piernas'  
b='brazos'
c='abdomen'
d='lumbares'
e='gluteos'

listapartesdelcuerpo=[a,b,c,d,e]

cardio=['burpees','saltar lazo','trotar',]
A=['sentadillas','sancadas','puentes','elevacion de talones']
B=['flexiones de pecho', 'extension de tripceps','elevacion lateral de hombros']
C=['raton']
D=['superman','peso muerto',]
E=['zancada lateral','subidas al cajon','patadas de gluteo']


def eleccionpartedelcuerpo(y):
    res=-1
    if y >= 0.0 and y < (1.0/5):
            res= 0
    if y >= (1.0/5) and y < (2.0/5):
            res=1
    elif y >= (2.0/5) and y < (3.0/5):
            res= 2 
    elif y > (3.0/5) and y < (4.0/5):
            res = 3 
    elif y > (4.0/5) and y < 1:
            res= 4
    return res





y= random()
z= random()

#para que no sean el mismo 
while  eleccionpartedelcuerpo(y)==eleccionpartedelcuerpo(z):
    z=random()
    


#____________barra de menu_________________________________



def infoAdicional():
    messagebox.showinfo('funcional','hoy vamos a entrenar '+' '+str(listapartesdelcuerpo[int(eleccionpartedelcuerpo(y))])+' '+'y'+''+' '+str(listapartesdelcuerpo[int(eleccionpartedelcuerpo(z))]))

def salirAplicacion():
    valorsalir=messagebox.askquestion('salir','deseas salir de la aplicación?')
 
    if valorsalir=='yes':
        raiz.destroy()
      


entrenamientoMenu=Menu(barraMenu, tearoff=0)
#sub____
entrenamientoMenu.add_command(label='cardiovascular',command=infocardio)
entrenamientoMenu.add_command(label='funcional',command=infoAdicional)
entrenamientoMenu.add_separator()

entrenamientoMenu.add_command(label='salir',command=salirAplicacion)

alimentacionMenu=Menu(barraMenu, tearoff= 0)
#sub__
alimentacionMenu.add_command(label='crear base de informacion',command=conexionBBDD)
alimentacionMenu.add_command(label='crear base de contador de calorias',command=conexionAli)
alimentacionMenu.add_command(label='borrar campos', command=limpiarCampos)



progresoMenu=Menu(barraMenu, tearoff=0)
progresoMenu.add_command(label='gluteos',command=infoglu)
progresoMenu.add_command(label='brazos',command=infobrazos)
progresoMenu.add_command(label='piernas',command=infopierna)
progresoMenu.add_command(label='lumbares',command=infolum)
progresoMenu.add_command(label='addomen',command=infoabd)
#lo que quiero que apareza 
barraMenu.add_cascade(label='Entrenamiento', menu=entrenamientoMenu)
barraMenu.add_cascade(label='Alimentacion', menu=alimentacionMenu)

barraMenu.add_cascade(label='ejercicios', menu=progresoMenu)








#____________________________________________
raiz.mainloop()
