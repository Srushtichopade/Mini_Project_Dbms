import mysql.connector as c
con=c.connect(host="localhost",
              user="root",
              password="Srush@028",
              database="HelthTRack_Project")
if con.is_connected():
    print("Successfully connected....!!!!!")
print("*"*184)
print(" "*99 , end = '')
print("HelthTrack")
print("*"*184)

cursor=con.cursor()
while True:
  a=int(input("Patient ID"))
  b=input("Patient name ")
  c=int(input("Age "))
  d=input("Gender")
  e=int(input("Contact_no"))
  f=int(input("Admit Month"))
  g=int(input("Discharge Month"))
  h=input("Attending Phycisian")
  i=input("Old Record")
  query="insert into HelthTRack_Project(Patient_id,Patient_name,Age,Gender,Contact_no,Admit_Month,Discharge_Month,Attending_physician,Old_Record)values({},'{}',{},'{}',{},{},{},'{}','{}')".format(a,b,c,d,e,f,g,h,i)

  cursor.execute(query)
  con.commit()
  print("Process Done!!!!!!\n\n")
  choice=int(input("1->Enter more Record\n 2->Update \n 3->Delate  \n 4->Exit  Enter the choice :"))

  if choice ==2:
      query="Update helthTrack set Old_Record = Yes where Patient_id=17"
      
  if choice ==3:
      query="delete from helthTrackk where Patient_id=70"
      
  if choice ==4:
      break
  
  
  
      
   
