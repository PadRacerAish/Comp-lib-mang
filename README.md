# Comp-lib-mang
It is school project of computer science for library management.
import mysql.connector as a
con=a.connect(host='localhost',user='root',passwd='aditya',database='library')


def addbook():
    bn=input("enter book name:")
    c=input("enter book code:")
    t=input("total books:")
    s=input("enter subject:")

    data=(bn,c,t,s)
    sql='insert into books values(%s,%s,%s,%s)'
    c=con.cursor()
    c.execute(sql,data)
    con.commit()
    print('>-----------------------------------------------------------')
    print(" DATA ENTERED SUCCESSFULLY")
    main()

def issueb():
    n=input("enter student name:")
    r=input("enter regno.:")
    co=input("enter book code:")
    d=input("enter date:")
    a='insert into issue values(%s,%s,%s,%s)'
    data=(n,r,co,d)
    c=con.cursor()
    c.execute(a,data)
    con.commit()
    print(">------------------------------------------------------------")
    print("BOOK SUCCESFULLY ISSUED TO :",n)
    bookup(co,-1)

def submitb():
    n=input("enter student name:")
    r=input("enter regno.:")
    co=input("enter book code:")
    d=input("enter date:")
    a='insert into issue values(%s,%s,%s,%s)'
    data=(n,r,co,d)
    c=con.cursor()
    c.execute(a,data)
    con.commit()
    print(">------------------------------------------------------------")
    print("BOOK SUCCESFULLY SUBMITTED BY :",n)
    bookup(co,1)

def bookup(co,u):
    a='select TOTAL from books where BCODE=%s'
    data=(co,)
    c=con.cursor()
    c.execute(a,data)
    myresult=c.fetchone()
    t=myresult[0]+u
    sql="update BOOKS set total=%s where BCODE=%s"
    d=(t,co)
    c.execute(sql,d)
    con.commit()
    main()

def dbook():
    ac=input("enter book code:")
    a=' delete from books where bcode=%s'
    data=(ac,)
    c=con.cursor()
    c.execute(a,data)
    con.commit()
    main()

def dispbook():
    
    a= ' select * from books'
    c=con.cursor()
    c.execute(a)
    myresult=c.fetchall()
    for i in myresult:
        print("BOOK NAME:",i[0])
        print("BOOK CODE :",i[1])
        print("TOTAL:",i[2])
        print(">======================<")
    main()

def main():
    print("""
                                LIBRARY MANAGER

        1.ADD BOOK
        2.ISSUE BOOK
        3.SUBMIT BOOK
        4.DELETE BOOK
        5.DISPLAY BOOK
        """)
    choice=int(input("enter task number:"))
    print(">======================================<")
    if choice==1:
        addbook()
    elif choice==2:
        issueb()
    elif choice==3:
        submitb()
    elif choice==4:
        dbook()
    elif choice==5:
        dispbook()
    else:
        print("wrong choice")
        main()

        
def pswd():
    ps=input("enter the password:")
    if ps=='kveme':
        main()
pswd()
