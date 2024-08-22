# Calculator-creation-with-tkinter

from tkinter import *
import random
window=Tk()
window.title("Calculator")
window.geometry("200x200")
icon=PhotoImage(file="C:\\Users\\sree\\Pictures\\calculator-icon-4.png")
window.iconphoto(True,icon)
l=["orange","pink","blue","yellow","brown","gray","violet"]
window.config(background="gray")
global equation_text,equation_label,eq,label,label2
equation_text=""    
equation_label=StringVar()
eq=StringVar()
label1=Label(window,bg="white",text="CALCULATOR",font=("consolas",20),height=2,width=24)
label1.pack()
label=Label(window,bg="white",textvariable=equation_label,font=("consolas",20),height=2,width=24)
label.pack()
label2=Label(window,bg="white",textvariable=eq,font=("consolas",20),height=2,width=24)
label2.pack()
def button_pressed(val): 
    global equation_text
    global flag1,flag,evalflag
    if len(str(equation_label.get()))==1 and str(equation_label.get())[0]=="0":
        equation_text=str(val)
        equation_label.set(equation_text)
        flag1=1
    else:
        if flag==0:
            equation_text=equation_label.get()+str(val)
            equation_label.set(equation_text)
            flag1=1
            if evalflag==1:
                eq.set(eval(equation_text))
    if flag==1:
            try:
                equation_text=equation_label.get()+str(val)
                total=str(eval(equation_text))
                equation_label.set(equation_text)
                eq.set(total)
                flag=0
                evalflag=1
                flag1=1
            except ZeroDivisionError:
                equation_label.set(equation_text)
                eq.set("can't divide by zero")
                flag=-1
                flag1=0
                deciflag=-1
                equation_text=""
def clear_pressed():
    global equation_text,flag,deciflag
    equation_label.set(0)
    eq.set(0)
    equation_text=""
    flag=0
    deciflag=0
def clear_by_one(val):
    global flag1
    global flag
    global equation_text,deciflag
    try:
        if len(val)<1:
            equation_label.set("0")
            eq.set("")
            flag=0
            deciflag=0
        else:
            equation_label.set(val)
            equation_text=""
            flag1=1
            if val[-1] in ["/","*","+","-"]:
                eq.set(eval(val[0:len(val)-1]))
                flag=1
                flag1=0
            else:
                eq.set(eval(val[0:len(val)]))
                flag=1
    except SyntaxError:
        equation_label.set("")
        flag=0
        flag1=0
    except ZeroDivisionError:
        equation_label.set("")
        flag=0
        flag1=0
def evaluate(val):
    global flag1
    global flag,deciflag
    if len(val)<=2 and val[0]=="0":
        equation_label.set("0")
    elif len(val)>=17:
        equation_label.set(val[:len(val)-1])
    elif flag1==1:
        equation_label.set(val)
        flag1=0
        flag=1
        deciflag=0
    else:
        flag1=0
def decimal(val):
    global deciflag,equation_text
    if deciflag==0:
        equation_text=equation_label.get()+str(val)
        equation_label.set(equation_text)
        equation_text=""
        deciflag=1
def equals():
    global flag1
    if len(str(equation_label.get()))==0:
        equation_label.set("")
        eq.set("")
    elif len(str(eq.get()))!=0:
             equation_label.set(eq.get())
             eq.set("")
    elif len(str(eq.get()))==0:
            if str(equation_label.get())[-1] in ["/","*","+","-"]:
                equation_label.set(str(equation_label.get())[:len(equation_label.get())-1])
                flag1=1
            else:
                if len(str(equation_label.get()))==0:
                    equation_label.set("")
                    eq.set("")
                else:
                     equation_label.set(equation_label.get())
                     eq.set("")
    flag1=1
def fun():
        global new,frame,flag,flag1,evalflag,deciflag,clear,x,division,button1,button2,button3,button4,button5,button6,button7,button8,button9
        global mul,add,sub,extra,zero,deci,equal
        flag=0
        flag1=0
        evalflag=0
        deciflag=0
        frame=Frame(window)
        frame.pack()
        clear=Button(frame,text="clear",height=4,width=9,command=lambda : clear_pressed(),bg=random.choices(l),activebackground=random.choices(l))
        clear.grid(row=0,column=0)
        x=Button(frame,text="X",height=4,width=9,command=lambda : clear_by_one((str(equation_label.get())[:len(equation_label.get())-1])),bg=random.choices(l),activebackground=random.choices(l))
        x.grid(row=0,column=1)
        division=Button(frame,text="/",height=4,width=9,command=lambda : evaluate(str(equation_label.get())+"/"),bg=random.choices(l),activebackground=random.choices(l))
        division.grid(row=0,column=3)
        button7=Button(frame,text="7",height=4,width=9,command=lambda : button_pressed("7"),bg=random.choices(l),activebackground=random.choices(l))
        button7.grid(row=1,column=0)
        button8=Button(frame,text="8",height=4,width=9,command=lambda : button_pressed("8"),bg=random.choices(l),activebackground=random.choices(l))
        button8.grid(row=1,column=1)
        button9=Button(frame,text="9",height=4,width=9,command=lambda : button_pressed("9"),bg=random.choices(l),activebackground=random.choices(l))
        button9.grid(row=1,column=2)
        mul=Button(frame,text="x",height=4,width=9,command=lambda : evaluate(str(equation_label.get())+"*"),bg=random.choices(l),activebackground=random.choices(l))
        mul.grid(row=1,column=3)
        button4=Button(frame,text="4",height=4,width=9,command=lambda : button_pressed("4"),bg=random.choices(l),activebackground=random.choices(l))
        button4.grid(row=2,column=0)
        button5=Button(frame,text="5",height=4,width=9,command=lambda : button_pressed("5"),bg=random.choices(l),activebackground=random.choices(l))
        button5.grid(row=2,column=1)
        button6=Button(frame,text="6",height=4,width=9,command=lambda : button_pressed("6"),bg=random.choices(l),activebackground=random.choices(l))
        button6.grid(row=2,column=2)
        sub=Button(frame,text="-",height=4,width=9,command=lambda:evaluate(str(equation_label.get())+"-"),bg=random.choices(l),activebackground=random.choices(l))
        sub.grid(row=2,column=3)
        button1=Button(frame,text="1",height=4,width=9,command=lambda : button_pressed("1"),bg=random.choices(l),activebackground=random.choices(l))
        button1.grid(row=3,column=0)
        button2=Button(frame,text="2",height=4,width=9,command=lambda : button_pressed("2"),bg=random.choices(l),activebackground=random.choices(l))
        button2.grid(row=3,column=1)
        button3=Button(frame,text="3",height=4,width=9,command=lambda : button_pressed("3"),bg=random.choices(l),activebackground=random.choices(l))
        button3.grid(row=3,column=2)
        add=Button(frame,text="+",height=4,width=9,command=lambda:evaluate(str(equation_label.get())+"+"),bg=random.choices(l),activebackground=random.choices(l))
        add.grid(row=3,column=3)
        zero=Button(frame,text="0",height=4,width=9,command=lambda : button_pressed("0"),bg=random.choices(l),activebackground=random.choices(l))
        zero.grid(row=4,column=1)
        deci=Button(frame,text=".",height=4,width=9,command=lambda :decimal("."),bg=random.choices(l),activebackground=random.choices(l))
        deci.grid(row=0,column=2)
        equal=Button(frame,text="=",height=4,width=9,command=lambda:equals(),bg=random.choices(l),activebackground=random.choices(l))
        equal.grid(row=4,column=2)
fun()
window.mainloop()
