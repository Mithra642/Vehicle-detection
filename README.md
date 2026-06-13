import cv2
import numpy as np
net=cv2.dnn.readNet("yolov3.weights", "yolov3.cfg")
with open("coco.names", "r") as f:
classes=[line.strip() for line in f.readlines()]
layer_names=net.getLayerNames()
output_layers=[layer_names[i - 1] for i in net.getUnconnectedOutLayers()]
image cv2.imread("traffic vechiles.jpg")
height, width, channels=image.shape
blob=cv2.dnn.blobFromImage(image, 1/255.0, (416, 416), swapRB=True, crop False)
net.setInput(blob)
outputs = net.forward(output_layers)
boxes = []
confidences = []
class_ids = []
for output in outputs: 
    for detection in output:
        scores = detection [5:]
        class_id= np.argmax(scores)
        confidence = scores [class_id]

if confidence > 0.5:
center_x = int (detection[0] * width)
center_y = int (detection[1] * height)
w = int(detection[2] * width)
h = int(detection[3] * height)
x = int (center_x - W/2)
y = int(center_y -  h/2)
boxes.append([x, y, w, h])
confidences.append(float(confidence))
class_ids.append(class_id)
Indexes = cv2.dnn.NMSBoxes(boxes, confidences, 0.5, 0.4)
vehicle_classes = ["car", "bus", "truck", "motorbike"]
vehicle_count = 0
if len(indexes) > 0:
for i in indexes.flatten():
    label = classes[class_ids[i]]
if label in vehicle_classes:
vehicle_count += 1
x, y, w, h = boxes[i]
cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2)
cv2.putText(image, label, (x, y-10), cv2.FONT HERSHEY SIMPLEX, 0.6, (0, 255, 0), 2)
cv2.putText(image, f"Total Vehicles: (vehicle_count)", (20, 40),cv2. FONT_HERSHEY_SIMPLEX,1, (0, 0, 255),3)
if len(indexes) > 0:
    for i in indexes.flatten():
        label = classes[class_ids[i]]
if label in vehicle_classes:
    vehicle_count += 1
    x, y, w, h boxes[i]
    cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2) cv2.putText(image, label,(x, y-10),
cv2.FONT HERSHEY SIMPLEX, 0.6,
(0, 255, 0), 2)
cv2.putText(image, f"Total Vehicles: (vehicle_count)",
(20, 40),
cv2. FONT HERSHEY SIMPLEX, 1, (0, 0, 255), 3)
print("Total Vehicles Detected:", vehicle_count)
cv2.imshow("Vehicle Detection", image)
cv2.waitKey(0)
cv2.destroyAllWindows()

Total Vehicles Detected: 26


