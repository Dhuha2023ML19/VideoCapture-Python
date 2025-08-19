# VideoCapture-Python
import numpy as np
import cv2 as cv


cap = cv.VideoCapture(0) #Capture the webcam on the computer, 0 specifies that you want to only use 1 camera and not multiple.

while True:
    ret, frame = cap.read()  #ret is boolean value that is True if the webcam is captured successfuly.
    width = int(cap.get(3))  # 3 defines the property "width", typecasted it into integer because it is by default a floating number, but when do slicing we need to use integers not boolean.
    height = int(cap.get(4)) # 4 defines the property "height", typecasted it into integer because it is by default a floating number, but when do slicing we need to use integers not boolean.

    image = np.zeros(frame.shape,np.uint8) #Fills the webcam with all zeros (black image)
    smaller_frame = cv.resize(frame, (0,0), fx=0.5, fy=0.5)
    image[:height//2, :width//2] = smaller_frame # frame placed in the UP Left corner
    image[height//2:, :width//2] = smaller_frame # frame placed in the Bottom Left corner
    image[:height//2, width//2:] = smaller_frame # frame placed in the UP Right corner
    image[height//2:, width//2:] = smaller_frame # frame placed in the Bottom Right corner
    
    cv.imshow("WebCam",image) 

    if cv.waitKey(1) == ord("q"): #Waits for 1 milliseconds for the key to pressed, if no key is pressed the loop will keep on going giving a smooth video, but if we increase the number then the video will be slowed, and if we put 0 then the video will stay stop as it is(because the progrm will be freezed).
        break

cap.release() #Releases the webcam, if not released, other apps might not be able to properly use the webcam.
cv.destroyAllWindows() #Closes all windows
