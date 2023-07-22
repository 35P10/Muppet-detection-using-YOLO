
# Detección de Muppets usando YOLOv7


### Data

* Se extrajeron fotogramas de videos y, de manera manual, se procedió a etiquetar cada personaje presente en cada fotograma usando LabelImg. 

| Version       | Descripcion | Labels | Images | Train images | Val images | Link
|--------------|------|------|------|------|------|------|
| v1         | Primer episodio de la serie The Muppets 2015 | **24:** 'Kermit', 'Miss Piggy', 'Fozzie Bear', 'Sam the Eagle', 'Rizzo the Rat', 'Yolanda Rat', 'The Great Gonzo', 'Scooter', 'Zoot', 'Pepe the King Prawn', 'Dr. Bunsen Honeydew', 'Beaker', 'Floyd Pepper', 'Animal', 'Dr. Teeth', 'Janice', 'Lips', 'Bobo the Bear', 'Waldorf', 'Statler','Sweetums', 'The Swedish Chef', 'Uncle Deadly', 'Big Mean Carl' |  459 |392 | 67 |


## 🧩 Requerimientos

* Python
* [Anaconda](https://www.anaconda.com/download/)

## ⚙️ Configuración de entorno


1. Clone el repositorio original de [YOLOv7](https://github.com/WongKinYiu/yolov7)

```
git clone https://github.com/WongKinYiu/yolov7.git
```

2. Agrege contenido desde este reposotorio en YOLOv7.
    * ```cfg\training\yolov7-muppets.yaml``` (opcional, si desea entrenar el modelo)
    * ```muppet_prediction_weights\v*\v*-best.pt```
    * ```requirements_CUDA.txt```
    * Reemplaze el contenido de ```requirements.txt```


    Los directorios deberian verse similar a:

3. Abra el directorio ```your/path/YOLOv7``` en el terminal Anaconda:

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

> NOTA: Para las instrucciones a continuación asegúrese de encontrarse en el entorno "yolov7" (Anaconda).

## 🏷️ Realizar predicciones

```
python detect.py --weights "path/of/weights" --conf 0.5 --img-size 640 --source "path/to/imageOrVideo" --view-img --no-trace
```

La salida debe encontrarse en ```.\runs\detect```

### Pesos

| Version       | path |
|--------------|------|
| v1         | muppet_prediction_weights\v1\v1-best.pt   |

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

| Version       | path |
|--------------|------|
| v1         | muppet_prediction_weights\v1\v1-best.pt| 


El archivo descargado muévalo a la carpeta ```.\data```

### Etiquetar imagenes

Descarge LabelImg:
```
pip install labelImg
```
Ejecute el programa con:
```
labelImg
```