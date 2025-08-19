import numpy as np
import cv2 as cv

cap = cv.VideoCapture(0) 

while True:
   ret, frame = cap.read() 
   width = int(cap.get(3)) 
   height = int(cap.get(4))
  
   image = np.zeros(frame.shape,np.uint8) 
   smaller_frame = cv.resize(frame, (0,0), fx=0.5, fy=0.5)
   image[:height//2, :width//2] = smaller_frame 
   image[height//2:, :width//2] = cv.rotate(smaller_frame,cv.ROTATE_180) 
   image[:height//2, width//2:] =  smaller_frame
   image[height//2:, width//2:] = cv.rotate(smaller_frame,cv.ROTATE_180) 
        
   cv.imshow("WebCam", image) 

   if cv.waitKey(1) == ord("q"): 
      break


cap.release() 
cv.destroyAllWindows() 
