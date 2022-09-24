#### Train with specified GPUs
python train.py --weights 'runs/train/exp75/weights/best.pt' --data 'data/dotav15_poly.yaml' --hyp 'data/hyps/obb/hyp.finetune_dota.yaml' --epochs 300 --batch-size -1 --device 0

#### Test yolov5-obb with single GPU. Get the HBB metrics
python val.py --data 'data/dotav15_poly.yaml' --weights 'runs/train/exp75/weights/best.pt' --batch-size -1 --img 2048 --task 'val' --device 0 --save-json --name 'obb_76'

#### Parse the results. Get the poly format results.
python tools/TestJson2VocClassTxt.py --json_path 'runs/val/obb_823/best_obb_predictions.json' --save_path 'runs/val/obb_823/obb_predictions_Txt'

#### Get the OBB metrics
python DOTA_devkit/dota_evaluation_task1.py --detpath 'runs/val/obb_762/obb_predictions_Txt/Task1_{:s}.txt' --annopath '/media/vasya/cf028678-d9b6-4839-81c7-4bc43f361caa/DOTA/DOTAv1.5/val/labelTxt/{:s}.txt' --imagesetfile '/media/vasya/cf028678-d9b6-4839-81c7-4bc43f361caa/DOTA/DOTAv1.5/val/imgnamefile.txt'  
It is nessesary check true labels for DOTA 1,1.5 or 2.0 in code the program
#### Detect objects on user's pictures
python detect.py --weights 'runs/train/exp75/weights/best.pt' --source 'dataset/dataset_demo/images/' --img 2048 --device 0 --conf-thres 0.25 --iou-thres 0.2 --hide-labels --hide-conf

python detect.py --weights 'runs/train/exp76/weights/best.pt' --source '/media/vasya/cf028678-d9b6-4839-81c7-4bc43f361caa/DOTA/DOTAv1.5/val/images' --device 0



#### Program's parameters
##### 1 TestJson2VocClassTxt.py [-h] [--json_path JSON_PATH] [--save_path SAVE_PATH]
optional arguments:  

>  -h, --help         -   show this help message and exit  
> --json_path JSON_PATH   - path to file   'best_obb_predictions.json'  
> --save_path SAVE_PATH   - specify where to save the output dir of labels
