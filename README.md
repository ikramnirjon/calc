from tkinter import*

root = Tk()
root.title("Calculator")
root.minsize(width=350, height=500)
root.maxsize(width=1280, height=800)

def ScitechzCalc(source, side):
    storeObj = Frame (source, borderwidth=3, bd=3, bg="white")
    storeObj.pack(side=side, expand=YES, fill=BOTH)
    return storeObj

def button(source, side, text, command=None):
    storeObj = Button(source, bg="white", fg="black", text=text, command=command)
    storeObj.pack(side=side, expand=YES, fill=BOTH)
    return storeObj

class app(Frame):
    def __init__(self):
        Frame. __init__(self)
        self.option_add('*Font', 'Helvetica 24 italic', )
        self.pack(expand=YES, fill=BOTH)


        display = StringVar()
        Entry(self, relief=RIDGE,
                textvariable=display,justify='right',bd=26,fg="black",bg="white").pack(side=TOP, expand=YES,
                        fill=BOTH)

        for clearBut in(["CLEAR"],):
            erase = ScitechzCalc(self, TOP)
            for ichar in clearBut:
                button(erase, LEFT, ichar,
                       lambda storeObj=display, q=ichar: storeObj.set(''))

        for NumBut in ("789/", "456*", "123-", "0.+"):
            FunctionNum = ScitechzCalc(self, TOP)
            for char in NumBut:
                button(FunctionNum, LEFT, char,
                       lambda storeObj=display, q=char: storeObj.set(storeObj.get() + q))

        EqualsButton = ScitechzCalc(self, TOP)
        for iEquals in "=":
            if iEquals == '=':
                btniEquals = button(EqualsButton, LEFT, iEquals)
                btniEquals.bind('<ButtonRelease-1>',
                         lambda e, s=self, storeObj=display: s.calc(storeObj), '+')
            else:
                btniEquals = button(EqualsButton, LEFT, iEquals,
                   lambda storeObj=display, s=' %s '%iEquals: storeObj.set(storeObj.get()+s))
       

    def calc(self, display):
        try:
            display.set(eval(display.get()))
        except:
            display.set("Error")

if __name__ == '__main__':
    app().mainloop()
