import tkinter
from tkinter import *
from tkinter.font import Font
from tkinter import ttk
import  tkinter.messagebox as Messagebox
from tkinter import Button

import mysql.connector
def Insert():
   a=e1.get()
   b=e2.get()
   c=e3.get()
   d=combo.get()
   e=combo2.get()
   f=e6.get()
   g=e7.get()
   h=combo1.get()
   i=e9.get()
   mydb=mysql.connector.connect(
      host="localhost",
      user="root",
      password="4446",
      database="sports2"
      )
   mycursor=mydb.cursor()
   try:
      sql="INSERT INTO SPORTS3(Player_First_Name,Player_Middle_Name,Player_Last_Name,Sports_Discipline,Birth_Date,Mail_id,Phone_Number,Gender,Address)VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s)"
      val=(a,b,c,d,e,f,g,h,i)
      mycursor.execute(sql,val)
      mydb.commit()
      Messagebox.showinfo("Form","Registration success")
      a=e1.delete(0,END)
      b=e2.delete(0,END)
      c=e3.delete(0,END)
      d=combo.delete(0,END)
      e=combo2.delete(0,END)
      f=e6.delete(0,END)
      g=e7.delete(0,END)
      h=combo1.delete(0,END)
      i=e9.delete(0,END)
      e1.focus_set()
   except Exception as e:
      print(e)
      mydb.rollback()
      mydb.close()
def show(width):
   mydb2=mysql.connector.connect(host="localhost",user="root",password="4446",database="sports2")
   mycursor=mydb2.cursor()
   mycursor.execute('select Player_First_Name,Player_Middle_Name,Player_Last_Name,Sports_Discipline,Birth_Date,Mail_id,Phone_Number,Gender, Address from sports3')
   records=mycursor.fetchall()
   print(records)
   for i,(Player_First_Name,Player_Middle_Name,Player_Last_Name,Sports_Discipline,Birth_Date,Mail_id,Phone_Number,Gender, Address) in enumerate(records,start=1):
      Listbox.insert("","end",values=(Player_First_Name,Player_Middle_Name,Player_Last_Name,Sports_Discipline,Birth_Date,Mail_id,Phone_Number,Gender, Address))
      mydb2.close()
unique_identifier_column = 'Player_First_Name'

def Update():
   
    a = e1.get()
    b = e2.get()
    c = e3.get()
    d = combo.get()
    e = combo2.get()
    f = e6.get()
    g = e7.get()
    h = combo1.get()
    i = e9.get()
    
    selected_row = Listbox.selection()
    if not selected_row:
        Messagebox.showwarning("Update", "Please select a record to update.")
        return

    

    selected_id = Listbox.item(selected_row, 'values')[0]
    
    mydb = mysql.connector.connect(
        host="localhost",
        user="root",
        password="4446",
        database="sports2"
    )
    mycursor = mydb.cursor()
    try:
        sql = f"UPDATE SPORTS3 SET Player_First_Name = %s, Player_Middle_Name = %s, Player_Last_Name = %s, " \
              "Sports_Discipline = %s, Birth_Date = %s, Mail_id = %s, Phone_Number = %s, Gender = %s, Address = %s " \
              f"WHERE {unique_identifier_column} = %s"
        val = (a, b, c, d, e, f, g, h, i, selected_id)
        mycursor.execute(sql, val)
        mydb.commit()
        Messagebox.showinfo("Update", "Record updated successfully.")
        
        
    except Exception as e:
        print(e)
        mydb.rollback()
   
def Getvalue(event):
   e1.delete(0,END)
   e2.delete(0,END)
   e3.delete(0,END)
   combo.delete(0,END)
   combo2.delete(0,END)
   e6.delete(0,END)
   e7.delete(0,END)
   combo.delete(0,END)  
   selected_row=Listbox.selection()[0]
   values=Listbox.item(selected_row,'values')
   e9.delete(0,END)
   e1.insert(0,values[0])
   e2.insert(0,values[1])
   e3.insert(0,values[2])
   combo.insert(0,values[3])
   combo2.insert(0,values[4])
   e6.insert(0,values[5])
   e7.insert(0,values[6])
   combo1.insert(0,values[7])
   e9.insert(0,values[8])

root=tkinter.Tk()
root.geometry("100x30")
root.title("sports form")
fon=Font(family="Times New Roman",size=20,weight="bold")
fon1=Font(family="Times new roman",size=12,weight="bold")
l1=Label(root,text="SDAT REGISTRATION FORM",font=fon,fg="red")
l1.place(x="500",y="20")
l2=Label(root,text="Player First Name  *",font=fon1,fg="green")
l2.place(x="40",y="100")
e1=Entry(root,width=24)
e1.place(x="180",y="100")
l3=Label(root,text="Player Middle Name  ",font=fon1,fg="green")
l3.place(x="500",y="100")
e2=Entry(root,width=24)
e2.place(x="670",y="100")
l4=Label(root,text="Player Last Name  *",font=fon1,fg="green")
l4.place(x="1000",y="100")
e3=Entry(root,width=24)
e3.place(x="1150",y="100")
l5=Label(root,text="Sports Discipline  *",font=fon1,fg="green")
l5.place(x="40",y="200")
e4=Entry(root,width=24)
combo=ttk.Combobox(root, values=["Hockey", "Kabbadi", "Volley ball", "Foot ball","Cricket","Handball","Athlete"])
combo.place(x="180",y="200")
l6=Label(root,text="Birth Date  *",font=fon1,fg="green")
l6.place(x="500",y="200")
e5=Entry(root,width=24)
combo2 = ttk.Combobox(root, values=["2001", "2002", "2003", "2004","2005","2007"])
combo2.place(x="670",y="200")
l7=Label(root,text="Mail id  *",font=fon1,fg="green")
l7.place(x="1000",y="200")
e6=Entry(root,width=24)
e6.place(x="1150",y="200")
l8=Label(root,text="Phone Number  *",font=fon1,fg="green")
l8.place(x="40",y="300")
e7=Entry(root,width=24)
e7.insert(END,"+91")
e7.place(x="180",y="300")
l9=Label(root,text="Gender  *",font=fon1,fg="green")
l9.place(x="500",y="300")
e8=Entry(root)
combo1 = ttk.Combobox(root, values=["Male","Female"])
combo1.place(x="670",y="300")
l7=Label(root,text="Address  *",font=fon1,fg="green")
l7.place(x="1000",y="300")
e9=Entry(root,width=24)
e9.place(x="1150",y="300")

def clear():
    e1.delete(0,END)
    e2.delete(0,END)
    e3.delete(0,END)
    combo.delete(0,END)
    combo2.delete(0,END)
    e6.delete(0,END)
    e7.delete(0,END)
    combo1.delete(0,END)
    e9.delete(0,END)

def delete_record():
    selected_row = Listbox.selection()
    if not selected_row:
        Messagebox.showwarning("Delete", "Please select a record to delete.")
        return

    selected_id = Listbox.item(selected_row, 'values')[0]

    mydb = mysql.connector.connect(
        host="localhost",
        user="root",
        password="4446",
        database="sports2"
    )
    mycursor = mydb.cursor()
    try:
        sql = f"DELETE FROM  sports3 WHERE {unique_identifier_column} = %s"
        val = (selected_id,)
        mycursor.execute(sql, val)
        mydb.commit()
        Listbox.delete(selected_row)
        
        Messagebox.showinfo("Delete", "Record deleted successfully.")
    except Exception as e:
        print(e)
        mydb.rollback()
    finally:
        mydb.close()
b=Button(root,text="delete",font=fon1,command=delete_record,activebackground="red",bg="White")
b.place(x="500",y="400")

b1=Button(root,text="insert",font=fon1,command=Insert,activebackground="yellow",bg="white")
b1.place(x="300",y="400")

b2=Button(root,text="Update",font=fon1,command=Update,activebackground="violet",bg="white")
b2.place(x="700",y="400")

b3=Button(root,text="Clear",font=fon1,command=clear,activebackground="pink",bg="white")
b3.place(x="900",y="400")

cols=('Player_First_Name','Player_Middle_Name','Player_Last_Name','Sports_Discipline','Birth_Date','Mail_id','Phone_Number','Gender','Address')
Listbox=ttk.Treeview(root,columns=cols,show="headings")
for col in cols:
   Listbox.heading(col,text=col)
   Listbox.place(y="500")
   Listbox.grid(padx="0",pady="500")
show(20)
Listbox.bind('<Double-Button-1>',Getvalue)
root.mainloop()
