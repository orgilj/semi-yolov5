# self-yolov5
self learning on yolov5 experinmented on coco128


# build docker image
docker build -f Dockerfile .

docker run --gpus all --shm-size=8g -v /to_yolo_dir:/workspace -it created_image_name
# in container change directory /workspace/yolo directory 
cd /workspace/yolo_something_name
# download coco128 dataset
python train.py --img 640 --batch 16 --epochs 3 --data coco128.yaml --weights yolov5s.pt --cache
# will get error message and go datasets dir copy ../datasets/coco128/image/train2017 to ../datasets/coco128/image/unlabeled
# also in our experiment we copied coco validation dataset to unlabeled directory

# after copying dataset run train.py again
python train.py --img 640 --batch 16 --epochs 300 --data coco128.yaml --weights yolov5s.pt --cache

|         	| supervised learning 	| self learning       	|
|---------	|---------------------	|---------------------	|
|         	| m@p0.5  m@p0.5-0.95 	| m@p0.5  m@p0.5-0.95 	|
| yolov5s 	| 0.967   0.799       	| 0.968   0.824       	|
| yolov5m 	| 0.975   0.876       	| 0.977   0.878       	|
| yolov5l 	| 0.977   0.878       	| 0.979   0.914       	|
| yolov5x 	| 0.979   0.901       	| 0.978   0.918       	|

# if there is shape size error appears just ignore them (actualy requires label error)