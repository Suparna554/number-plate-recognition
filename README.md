import cv2
import pytesseract
import numpy as np
import pyttsx3

pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\Tesseract.exe'

cascade=cv2.CascadeClassifier("haarcascade_russian_plate_number.xml")

states={"AN":"Andaman and Nicobar","AP":"Andhra Pradesh","AR":"Arunachal Pradesh","AS":"Assam","BR":"Bihar",
        "CG":"Chattisgarh","CH":"Chandigarh","DD":"Dadra and Nagar Haveli and Daman and Diu","DL":"Delhi",
        "GA":"Goa","GJ":"Gujarat","HP":"Himachal Pradesh","HR":"Haryana","JH":"Jharkhand",
         "JK":"Jammu and Kashmir","KA":"Karnataka","KL":"Kerala","KS":"Kyasamballi","LA":"Ladakh",
         "LD":"Lakshadweep","MH":"Maharashtra","ML":"Meghalaya","MN":"Manipur","MP":"Madhya Pradesh",
        "MZ":"Mizoram","NL":"Nagaland","OD":"Odisha","PB":"Punjab","PY":"Puducherry","RJ":"Rajasthan",
        "SK":"Sikkim","TN":"Tamil Nadu","TR":"Tripura","TS":"Telangana","UK":"Uttarakhand",
        "UP":"Uttar Pradesh","WB":"West Bengal"}
audio = pyttsx3.init()

def extract_num(img_name):
        global read
        read = pytesseract.image_to_string(plate)
        read = ' '.join(e for e in read if e.isalnum)
        stat = read[0:2]
        stat = read[:3]
        numstate = []
        numstate.append(read[0])
        numstate.append(read[2])
        str1 = ""
        for ele in numstate:
            str1 += ele
        print(str1)
        print(read)
        try:
            print('Car belongs to', states[stat])
            print('Car belongs to', states[str1])
            audio.say('The State is ')
            audio.say(states[str1])
            audio.runAndWait()
        except:
            print('State not recognized!')
        print(read)
        audio.say('State not recognized!', str1)
        audio.runAndWait()


cv2.rectangle(img, (x, y), (x + w, y + h), (51, 51, 255), 2)
cv2.rectangle(img, (x, y - 40), (x + w, y), (51, 51, 255), -1)
cv2.putText(img, read, (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 3.0, (125, 246, 55), 3)
cv2.waitKey(0)
cv2.destroyAllWindows()

extract_num ("C:/Users/HP/PycharmProjects/Numberplate/test1.jpeg")
extract_num ("C:/Users/user/PycharmProjects/Numberplate/test3.jpeg")
