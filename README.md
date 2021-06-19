# Attendance_Assistant
Python script to list how much time each student attended the class using the data provided in the csv file provided. Details such as Full Name, Action(joined/left), timestamp are provided in the csv file




csv_attendance.csv


"Full Name,User Action,Timestamp,"
"Samvasan P,Joined,4/23/2021, 6:44:22 PM"
"Keerthivaasan K V R,Joined,4/23/2021, 6:44:31 PM"
"Keerthivaasan K V R,Left,4/23/2021, 6:45:32 PM"
"Keerthivaasan K V R,Joined,4/23/2021, 6:51:56 PM"
"Keerthivaasan K V R,Left,4/23/2021, 6:53:35 PM"
"Keerthivaasan K V R,Joined,4/23/2021, 6:55:09 PM"
"Keerthivaasan K V R,Left,4/23/2021, 6:56:10 PM"
"Keerthivaasan K V R,Joined,4/23/2021, 7:01:06 PM"
"Pradeep S,Joined,4/23/2021, 6:48:38 PM"
"Pradeep S,Left,4/23/2021, 6:50:06 PM"
"Hariharan J,Joined,4/23/2021, 6:54:26 PM"
"Hariharan J,Left,4/23/2021, 7:13:54 PM"
"Hariharan J,Joined,4/23/2021, 7:13:57 PM"
"Samritha S,Joined,4/23/2021, 6:56:57 PM"
"Samritha S,Left,4/23/2021, 7:37:23 PM"
"Samritha S,Joined,4/23/2021, 7:37:34 PM"



# ATTENDANCE ASSISTANT
'''
TASK GIVEN :
Python script to list how much time each student attended the class
using the data provided in the csv file provided. Details such as Full Name,
Action(joined/left), timestamp are provided in the csv file
'''
start=int(input("Enter time approximately start time (6:30 means enter 630):"))
print()
end=int(input("Enter time approximately end time (7:00 means enter 700:"))
print()
m=input("Enter AM or PM:")
lst=[]
import csv
with open('D:\College\csv_attendance.csv','r')as csv_file:
    csv_reader = csv.reader(csv_file)
    next(csv_reader)   #Used to eliminate the first row
    for line in csv_reader:
        lst.append(line)
csv_file.close()
print("\nOriginal list : ")
print(lst)
l=[]
for i in range(len(lst)):
    l.append(lst[i][0].split(','))
print("\nOriginal list after splitting : ")
print(l)
y=[]
for i in range(len(l)):
    y.append(l[i][0])
print("\nList with only Names : ")
names=y    #Duplicate this list..
print(y)
ls=[]
for i in range(len(l)):
    for j in range(len(l[i])):
        if m in l[i][j]:   #Here m represents AM OR PM
            ls.append(l[i][j])
print("\nList with only times in ",m,": ")
print(ls)
new=[]
for i in ls:
    x=i.replace(m,'')
    new.append(x)
print("\nList with only times without",m,": ")
print(new)
w=[]
for i in new:
    x=i.replace(':','')
    w.append(x)
print("\nReplace the colon with empty space in the above list : ")
print(w)
time_int=[]
for i in w:
    time_int.append(i[1:len(i)-3])     #len(i)=7 ;len(i)-3=4 ..So index from 1 to 3(4-1)
print("\nTaking only necessary characters for calculation : ")
print(time_int)
dic_index={}
for j in names:
    dupl=[i for i in range(len(names)) if names[i]==j]
    dic_index[j]=dupl
print("\nThe dictionary with key as name and value of list as index of time : ")
print(dic_index)
times=[]
dic_times={}
k=1
for i in dic_index.values():
   times=[time_int[j] for j in i]
   dic_times[k]=times
   k+=1
#print(dic_times)
for i in dic_times.values():
    if (len(i)%2 != 0):
        i.append(str(end))
print("\nThe dictionary with key as number and value as list of joined and left time : ")
print(dic_times)
main=dic_times
for i,j in main.items():  #.items() is used to access both key and values..
    res=0
    while(len(j)!=0):
        if(j[1][0]==j[0][0]):
            res+=int(j[1])-int(j[0])
        else:
            tot = int(str(j[1])[0:len(j[1])-2]) - int(str(j[0])[0:len(j[0])-2])
            # Here [0:len(j[1])-2]) it represents only hour to be mentioned
            res+=int(j[1]) - int(j[0])-(tot*40)
        del j[0:2]
    main[i]=res
print("\nThe dictionary with key as number and value as total time the student attended : ")
print(main)
print()
print("------------------------------------------------------------\n")
print("CLASS ATTENDANCE WITH DURATION OF HOURS : \n")
for i in range(len(list(dic_index.keys()))):
    hrs=list(main.values())[i]/60   #Minutes to Hour conversion
    print(list(dic_index.keys())[i],"attend class for",list(main.values())[i],"minutes","(",round(hrs,2),")hrs")
    print()
print("------------------------------------------------------------")
