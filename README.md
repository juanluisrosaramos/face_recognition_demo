# Face recognition demo
Creado sobre el proyecto [face_recognition](https://github.com/ageitgey/face_recognition) y usando la librería Dlib

## Install

    $ virtualenv -p /usr/bin/python3.7 env
    $ source env/bin/activate
    $ pip install -r requirements.txt

Si es posible, compilar DLIB con cuda (sino descomentarlo de requirements.txt). Sobre todo para los ejemplos que crean dataset. [Compilar dlib con CUDA](https://gist.github.com/flavindias/0d1f8a1e1692572493d7437335705a33) en mi caso, tengo que compilar con gcc7 por lo que añado "cmake .. -DCUDA_HOST_COMPILER=/usr/bin/gcc-7" en el paso 3.1 y "python setup.py install --set CUDA_HOST_COMPILER=/usr/bin/gcc-7" después NO hago el pip install dlib.


### Trabajar con una sola imagen
Creado con [ejemplos de la libreria](https://github.com/ageitgey/face_recognition/tree/master/examples) la ventaja de este proyecto es que usa una sola imagen de la cara para reconocerla

#### Crear imagen desde la webcam. 
Abre la webcam y salva la imagen cuando presionemos la tecla "s". Añadir nombre de la persona como parámetro y será lo que mostrará en el sgte paso. Guarda laimagen en la carpeta known_people

    $ python webcam-capture.py nombre de la persona

#### Reconocer desde webcam
En el código está como añadir imagenes de personas y crear los encodings luego se llama a la webcam y compara los frames    
    $python facerec_from_webcam_faster.py

### Trabajar con dataset
Según el proyecto del uncle Adrian https://www.pyimagesearch.com/2018/06/18/face-recognition-with-opencv-python-and-deep-learning/
Siempre que se trabaje con CPU añadir -d hog a todos los comandos (no usará CNN)

#### Crear dataset
Añadir carpetas con nombres de personas a mostrar y unas cuantas fotos. en este caso podríamos hacer los de capturar varios frames de la persona. El dataset se creará con el nombre de encodings.pickle y ya lleva imagenes y nobres de las personas.

    $ python encode_faces.py --dataset known_people/ --encodings encodings.pickle

#### Ejecutar sobre imagen de test
       $ python recognize_faces_image.py --encodings encodings.pickle --image test_people/2.jpg 
#### Ejecutar la webcam contra el dataset

    $ python recognize_faces_video.py --encodings encodings.pickle --output output/webcam.avi --display 1 
(añadir -d hog si trabajamos con CPU)