# Face Recognition Integrated with SQLite

# Used Library:
face_recognition --> pip install face-recognition

# File 1: loadfacedb.py
Run this file to load image data in a SQL file with columns Person name(Filename), Person_Img, Face_Encoding.
The code takes input as a folder location which then scans for image files .jpg/.jpeg/.png, then it will continue with the process of parsing the name and adding data in their respective rows.
Face encoding details are in NumPy array format

**NOTE**
Give a folder location and not a single image file
Add image which has a single face
Images are converted to binary and SQL takes it as a BLOB.
Name the known images properly because that will be read as a person name 
(ex. If the name of the image is "Roni Thomas.jpg" then the face found in the image will be labeled as "Roni Thomas")

SQL command:
    CREATE TABLE IF NOT EXISTS ImageDB(
        Person TEXT,
        Person_Img BLOB,
        Face_Encoding TEXT);

# File 2: facerecog.py
Run this after the above file as this code read data from the created DB.
Give the image location as "C:\...\filename.jpg"
The given image is compared with the face encodings already available in the DB and if a match is found the name is printed in this case "Match found >>> Roni Thomas"

SQL Command to fetch encoding & name from DB:
    cur.execute("SELECT Face_Encoding FROM ImageDB")
    rows = cur.fetchall()

    cur.execute("SELECT Person FROM ImageDB")
    names = cur.fetchall()

**NOTE**
The encoding is stored as binary in SQL so this has to be converted back to NumPy array in order to compare the encodings the below code does the needful

row = b''.join(row)
db_enc = np.frombuffer(row)

# File 3: compare_img.py
For Comparing two images, just enter the image locations as .jpg and the results will be displayed as TRUE/FALSE

# To know more about the face recognition library visit:
https://pypi.org/project/face-recognition

For Installing in Windows it must be a hassle but for Linux users it's easy-peasy

Thank You for Reading hope this was helpful.

Regards,
Roni Thomas
dev.ronithomas@gmail.com