# Face Recognition Integrated with SQLite

Used modules:
face_recognition --> pip install face-recognition

File 1: loadfacedb.py
Run this file to load images in a sqlite file separated as Person name(File name), Person_Img, Face_Encoding.
The code takes input as a folder location which then scans for image files .jpg/.jpeg/.png, then it will continue with the process of parsing the name and adding data in their respective rows

** NOTE **
Give a folder location and not single image
Add image which has single face
Images are converted to binary and sql takes it as BLOB.
Name the known images properly because that will be read as persons name 
(ex. If name of image is "Roni Thomas.jpg" then the persons name will be Roni Thomas as well)

SQL command:
    CREATE TABLE IF NOT EXISTS ImageDB(
        Person TEXT,
        Person_Img BLOB,
        Face_Encoding TEXT);

File 2: facerecog.py
Run this after the above file as this files read data from the created DB.
Give the image location as "C:\...\filename.jpg"
The give image is compared with the face encodings already available in the DB and if a match is found the name is printed in this case "Match found >>> Roni Thomas"

SQL Command to fetch encoding & name from DB:
    cur.execute("SELECT Face_Encoding FROM ImageDB")
    rows = cur.fetchall()

    cur.execute("SELECT Person FROM ImageDB")
    names = cur.fetchall()

** NOTE **
The encoing are stored as binary in SQL so this has to be converted back to numpy array in order to compare the encondings the below code does the needful

row = b''.join(row)
db_enc = np.frombuffer(row)

File 3: compare_img.py
For Comapring two images, just enter the image loacations and the results will be displayed as TRUE/FALSE

To know more about the face recognition module please check
https://pypi.org/project/face-recognition

For Installing in Windows it must be hassle but for linux users its easy-peasy

Thank You for Reading hope this was helpful.

Regards
Roni Thomas
dev.ronithomas@gmail.com