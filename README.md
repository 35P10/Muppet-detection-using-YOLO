
# Detección de Muppets usando YOLOv7

¿Por qué sería relevante identificar Muppets? No lo sé, ¡pero aquí está!

<div align="center">
<img width="500" src= "https://github.com/35P10/Muppet-detection-using-YOLO/blob/main/muppet_prediction_weights/v1/test_batch1_pred.jpg">
<img width="500" src= "https://github.com/35P10/Muppet-detection-using-YOLO/blob/main/images/test_output.jpg">
</div>
   
### Data

* Se extrajeron fotogramas de videos y, de manera manual, se procedió a etiquetar cada personaje presente en cada fotograma usando LabelImg. 

<div align="center">
<img width="500" src="https://github.com/35P10/Muppet-detection-using-YOLO/blob/main/images/labeling.png">
</div>



| Version       | Source | Labels | Images | Train images | Val images | Link
|--------------|------|------|------|------|------|------|
| v1         | Primer episodio de la serie The Muppets 2015 | **24:** 'Kermit', 'Miss Piggy', 'Fozzie Bear', 'Sam the Eagle', 'Rizzo the Rat', 'Yolanda Rat', 'The Great Gonzo', 'Scooter', 'Zoot', 'Pepe the King Prawn', 'Dr. Bunsen Honeydew', 'Beaker', 'Floyd Pepper', 'Animal', 'Dr. Teeth', 'Janice', 'Lips', 'Bobo the Bear', 'Waldorf', 'Statler','Sweetums', 'The Swedish Chef', 'Uncle Deadly', 'Big Mean Carl'. | 459 | 392 | 67 | [Click me](https://1drv.ms/u/s!AtXTi8WrC_84i_osfo3TLA4CdzaAMQ?e=wP2db5)|
| v2         | v1, Segundo episodio de la serie The Muppets 2015 | v1 |  802 | 672 | 130 | [Click me](https://1drv.ms/u/s!AtXTi8WrC_84i_o4sra8FkaBQrWlug?e=qGWEaO)|

## 🧩 Requerimientos

* Python
* [Anaconda](https://www.anaconda.com/download/)

## ⚙️ Configuración de entorno


1. Clone el repositorio original de [YOLOv7](https://github.com/WongKinYiu/yolov7)

```
git clone https://github.com/WongKinYiu/yolov7.git
```

2. Agregue contenido desde este repositorio a YOLOv7.
    * ```cfg\training\yolov7-muppets.yaml``` (opcional, si desea entrenar el modelo)
    * ```muppet_prediction_weights\v*\v*-best.pt```
    * ```requirements_CUDA.txt```
    * Reemplaze el contenido de ```requirements.txt```


    El directorio root ***YOLOv7*** deberia verse similar a:

<div align="center">
<img width="200" src="https://github.com/35P10/Muppet-detection-using-YOLO/blob/main/images/dir02.png">
</div>

4. Abra el directorio ```your/path/YOLOv7``` en el terminal Anaconda:

```
cd /d your/path/YOLOv7
```

4. Ejecute:

```
conda create -n yolov7 python=3.9
```

```
conda activate yolov7
```

```
pip install -r requirements.txt
```

```
pip install -r requirements_CUDA.txt
```

> NOTA: Para las instrucciones a continuación asegúrese de encontrarse en el entorno "yolov7" de Anaconda.

## 🏷️ Realizar predicciones

```
python detect.py --weights "path/of/weights" --conf 0.5 --img-size 640 --source "path/to/imageOrVideo" --view-img --no-trace
```

La salida debe encontrarse en ```.\runs\detect```

### Pesos

| Version       | path |
|--------------|------|
| v1         | muppet_prediction_weights\v1\v1-best.pt   |
| v2         | muppet_prediction_weights\v2\v2-best.pt   |

**Ejemplo:**

```
python detect.py --weights muppet_prediction_weights\v1\v1-best.pt --conf 0.5 --img-size 640 --source test.jpg --view-img --no-trace
```

## 🚀 Entrenar modelo

```
python train.py --workers 1 --device 0 --batch-size 8 --epochs 100 --img 640 640 --data data/muppets_data.yaml --hyp data/hyp.scratch.custom.yaml --cfg cfg/training/yolov7-muppets.yaml --name yolov7-muppets --weights yolov7.pt
```

> NOTA: Si tiene problemas de VRAM, reduzca el valor del parámetro batch-size.

### Data

Descargue el dataset y muévalo a la carpeta ```.\data```

### Etiquetar imagenes

Descargue LabelImg:
```
pip install labelImg
```
Ejecute el programa con:
```
labelImg
```
