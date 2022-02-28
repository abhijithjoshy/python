from tkinter import *
root=Tk()
root.title("Registration Form")
root.geometry("500x500")
alphabets=["a","b","c","d","e","f","g","h","i","j",
           "k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z",]
Alphabets=["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P",
           "Q","R","S","T","U","V","W","X","Y","Z",]
symbols1='~!"@#$%^&*()_+}{:'
symbols2="|<>?|,./\;'\[]-="
label1=Label(text="First Name",font=("regular",15,"bold"))
label1.place(x=10,y=35)
entry1=Entry(root)
entry1.place(x=210,y=40)
label2=Label(text="Last Name",font=("regular",15,"bold"))
label2.place(x=10,y=70)
entry2=Entry(root)
entry2.place(x=210,y=75)
label3=Label(text="Age",font=("regular",15,"bold"))
label3.place(x=10,y=105)
entry3=Entry(root)
entry3.place(x=210,y=110,width=30,height=20)
label4=Label(text="Password",font=("regular",15,"bold"))
label4.place(x=10,y=140)
entry4=Entry(root)
entry4.place(x=210,y=145)
label5=Label(text="Confirm Password",font=("regular",15,"bold"))
label5.place(x=10,y=170)
entry5=Entry(root)
entry5.place(x=210,y=175)
label6=Label(text="* The size of name must be less than 50   "
                  "      \n\n*Age must be an integer    "
                  "                      "
                  "       \n\n* The size of password must  be less than 50")
label6.place(x=0,y=330)
label7=Label(text="Registration Form",font=("",12,"bold"),fg="red")
label7.place(x=160,y=0)
def funbutton1():
    x = pymysql.connect(host="localhost", user="root", password="psswd", db="college")
    funbuttonroot = Tk()
    funbuttonroot.geometry("500x500")
    funbuttonroot.title("login")
    cr = x.cursor()
    ab = entry1.get()
    ac = entry2.get()
    ageget = entry3.get()
    ad = entry4.get()
    ae=entry5.get()
    if ad == ae and len(ab) and len(ac) and len(ageget) and len(ad) and len(ae) > 0:
        if ageget in Alphabets or ageget in alphabets or ageget in symbols1 or ageget in symbols2:
            from tkinter import messagebox
            messagebox.showerror("Error","Age must be Integer")
            root.destroy()
            funbuttonroot.destroy()
        else:

             jj="insert into regform(firstname,lastname,age,password,confirmpassword)values(%s,%s,%s,%s,%s)"
             val=(ab,ac,ageget,ad,ae)
             cr.execute(jj,val)
             x.commit()
             x.close()
             root.destroy()
    elif len(ab) or len(ac) or len(ageget) or len(ad) or len(ae) == 0:
        funbuttonroot.destroy()
        from tkinter import messagebox
        messagebox.showerror("Empty Values or Password error", "Fill all blanks,make sure passwords are same and try again")
        root.destroy()
        funbuttonroot.destroy()
        funbuttonroot.mainloop()

    elif ageget in Alphabets or ageget in alphabets:
        root.destroy()
        funbuttonroot.destroy()
        from tkinter import messagebox
        messagebox.showerror("oops!","passwords Not Matches")

button1=Button(text="Submit",height=1,width=8,font=("",15,"bold"),bg="light grey",command=funbutton1)
button1.place(x=210,y=230)
root.mainloop()
