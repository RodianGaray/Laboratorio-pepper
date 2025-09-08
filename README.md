# Laboratorio con Pepper, Chatbot y Dashboard

Este repositorio contiene:
- Código de Pepper para la exposición.
- Chatbot educativo.
- Dashboard en Streamlit.
- Documento en Overleaf.
---

## Primer Punto: Interactuando con Pepper
### Paso a paso
### 1. Configuración
1. Conectar Pepper a la red y obtener su **IP**.  
2. Instalar Python con el SDK de NAOqi.  
3. Subir las diapositivas a la carpeta multimedia del robot o un servidor.  

### 2. Ejecutar
1. Guardar el script como `pepper_expo.py`.  
2. Cambiar la IP en el código:  
   ```python
   connection_url = "tcp://<IP_PEPPER>:9559"
Ejecutar:
```
python pepper_expo.py
```
### Imágenes de las diapositivas
Coloca tus imágenes en la carpeta images/ y cámbialas en el código:

```
tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva1.png")
```
### Ejemplo de estructura:
images/
 ├─ diapositiva1.png
 ├─ diapositiva2.png
 ├─ diapositiva3.png
 ├─ diapositiva4.png
 ├─ diapositiva5.png
### Código usado
```
import qi
import time
import sys

def main(session):
    tts = session.service("ALTextToSpeech")
    motion = session.service("ALMotion")
    posture = session.service("ALRobotPosture")
    tablet = session.service("ALTabletService")

    posture.goToPosture("StandInit", 0.5)
    tts.setLanguage("Spanish")
    tts.setVolume(0.9)

    # INTRODUCCIÓN
    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva1.png")
    tts.say("Hola a todos. Hoy quiero presentarles tres innovaciones que están transformando los sistemas digitales.")
    motion.setAngles("RShoulderPitch", -0.5, 0.2)
    motion.setAngles("RElbowYaw", 1.5, 0.2)
    motion.setAngles("RElbowRoll", 0.5, 0.2)
    time.sleep(3)
    motion.setAngles("RShoulderPitch", 1.5, 0.2)

    # --- PRIMER TEMA: INTELIGENCIA ARTIFICIAL GENERATIVA ---
    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva2.png")
    tts.say("En primer lugar, hablemos de la inteligencia artificial generativa multimodal. ")
    tts.say("La inteligencia artificial generativa multimodal combina múltiples tipos de datos como texto, imágenes y audio, para crear contenido innovador y transformador.")
    time.sleep(6)

    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva2b.png")
    tts.say("Estos modelos combinan texto, imagen y voz, generando experiencias enriquecidas e innovadoras que amplían las fronteras de la creatividad y la interacción humana tecnológica.")
    tts.say("Su importancia radica en que impulsan la inteligencia artificial actual, revolucionando aplicaciones en educación, arte e investigación.")
    motion.setAngles("HeadYaw", 0.3, 0.2)
    time.sleep(2)
    motion.setAngles("HeadYaw", -0.3, 0.2)
    motion.setAngles("HeadYaw", 0.0, 0.2)

    # --- SEGUNDO TEMA: METAVERSO Y GAMIFICACIÓN ---
    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva3.png")
    tts.say("En segundo lugar, exploremos el metaverso y la gamificación.")
    tts.say("El metaverso es un universo digital inmersivo donde convergen la realidad virtual y aumentada, transformando experiencias y potenciando nuevas formas de interacción y creatividad sin límites.")
    time.sleep(7)

    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva3b.png")
    tts.say("El metaverso potencia la gamificación al ofrecer experiencias inmersivas que aumentan la motivación y el aprendizaje, transformando la forma en que vivimos y trabajamos.")
    tts.say("Sus componentes clave integran realidad aumentada, realidad virtual, inteligencia artificial y conectividad avanzada, creando entornos digitales innovadores.")
    motion.setAngles("LShoulderPitch", -0.3, 0.2)
    motion.setAngles("RShoulderPitch", -0.3, 0.2)
    time.sleep(3)
    motion.setAngles("LShoulderPitch", 1.2, 0.2)
    motion.setAngles("RShoulderPitch", 1.2, 0.2)

    # --- TERCER TEMA: BLOCKCHAIN Y CONTRATOS INTELIGENTES ---
    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva4.png")
    tts.say("Finalmente, hablemos de blockchain y contratos inteligentes.")
    tts.say("Blockchain es una tecnología descentralizada que garantiza transparencia, seguridad y confianza mediante registros inmutables y colaboración sin intermediarios.")
    time.sleep(7)

    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva4b.png")
    tts.say("El registro descentralizado funciona con nodos distribuidos que validan y almacenan datos de forma segura, promoviendo transparencia y autonomía en cada transacción digital.")
    tts.say("La combinación de blockchain con contratos inteligentes asegura procesos confiables, transparentes y eficientes, transformando sectores como finanzas, cadenas de suministro y administración pública.")
    motion.setAngles("HeadPitch", 0.3, 0.2)
    time.sleep(2)
    motion.setAngles("HeadPitch", 0.0, 0.2)

    # CIERRE
    tablet.showImage("http://198.18.0.1/apps/multimedia/diapositiva5.png")
    tts.say("Estas innovaciones marcan el futuro de la tecnología digital. Muchas gracias por su atención.")
    tablet.hideImage()

if __name__ == "__main__":
    try:
        connection_url = "tcp://198.18.0.1:9559"
        app = qi.Application(["PepperTalk", "--qi-url=" + connection_url])
        app.start()
        session = app.session
        main(session)
    except RuntimeError:
        print("No se pudo conectar con Pepper.")


```
### Diapositivas mostradas:
![Diapositivas](Expo1.jpg) 
![Diapositivas](Expo2.jpg) 
![Diapositivas](Expo3.jpg) 
![Diapositivas](Expo4.jpg) 
![Diapositivas](Expo5.jpg) 
![Diapositivas](Expo6.jpg) 
 

## Segundo Punto: Chatbot
Paso a paso
Instalar dependencias:
```
pip install chatterbot chatterbot_corpus pyttsx3
```
Ejecutar el chatbot:
```
python scripts/chatbot.py
```
Para salir de la conversación:
```
salir
o
exit
```
Código usado (chatbot.py)
```
import qi
import sys
import time

# Base de conocimiento simple
respuestas = {
    "inteligencia artificial": "La inteligencia artificial generativa multimodal combina texto, imágenes y audio para crear contenido innovador.",
    "ejemplo ia": "Un ejemplo es un modelo que puede describir imágenes y luego generar texto y voz coherente.",
    "metaverso": "El metaverso es un universo digital inmersivo que une realidad virtual, aumentada e inteligencia artificial.",
    "gamificacion": "La gamificación aplica dinámicas de juego en contextos educativos o laborales para aumentar la motivación.",
    "blockchain": "Blockchain es una base de datos descentralizada y segura que registra transacciones de forma transparente.",
    "contratos inteligentes": "Los contratos inteligentes son programas autoejecutables que garantizan procesos seguros y transparentes."
}

def responder(session, pregunta):
    tts = session.service("ALTextToSpeech")
    motion = session.service("ALMotion")

    pregunta = pregunta.lower()
    for clave, respuesta in respuestas.items():
        if clave in pregunta:
            tts.say(respuesta)
            motion.setAngles("HeadYaw", 0.3, 0.2)
            time.sleep(1)
            motion.setAngles("HeadYaw", -0.3, 0.2)
            motion.setAngles("HeadYaw", 0.0, 0.2)
            return
    tts.say("Lo siento, solo puedo responder sobre inteligencia artificial generativa, metaverso y blockchain.")

def main(session):
    tts = session.service("ALTextToSpeech")
    tts.setLanguage("Spanish")
    tts.setVolume(0.9)

    tts.say("Hola. Soy Pepper y responderé tus preguntas sobre inteligencia artificial generativa, metaverso y blockchain.")
    while True:
        pregunta = raw_input("Escribe tu pregunta: ")  # Para Python 2.7 en NAOqi
        if pregunta.lower() in ["salir", "exit"]:
            tts.say("Gracias por conversar conmigo. Hasta pronto.")
            break
        responder(session, pregunta)

if __name__ == "__main__":
    try:
        connection_url = "tcp://198.18.0.1:9559"
        app = qi.Application(["PepperChatbot", "--qi-url=" + connection_url])
        app.start()
        session = app.session
        main(session)
    except RuntimeError:
        print("No se pudo conectar con Pepper.")
```
## Tercer Punto: Dashboard
Paso a paso
Instalar Streamlit:
```
pip install streamlit
```
Ejecutar el dashboard:
```
streamlit run scripts/dashboard.py
```
Código usado (dashboard.py)
```
import streamlit as st
import requests

st.set_page_config(page_title="Dashboard Pepper", layout="centered")

st.title("Dashboard Integrado con Pepper")
st.write("Este dashboard conecta el chatbot y las presentaciones de Pepper.")

# Sección chatbot
st.header("Chatbot")
pregunta = st.text_input("Escribe tu pregunta sobre IA, Metaverso o Blockchain:")

if st.button("Enviar"):
    if pregunta.strip():
        # Aquí se conectaría con el chatbot corriendo en Pepper
        # Para prueba local simulamos una respuesta
        st.success("Respuesta de Pepper: " + "Contenido generado según la pregunta.")
    else:
        st.warning("Por favor escribe una pregunta válida.")

# Sección multimedia
st.header("Material Multimedia")
opcion = st.selectbox("Selecciona un tema:", [
    "Tema1 - IA Generativa Multimodal",
    "Tema2 - Metaverso y Gamificacion",
    "Tema3 - Blockchain y Contratos Inteligentes"
])

if opcion == "Tema1 - IA Generativa Multimodal":
    st.image("images/expo2.png", caption="Pepper explicando IA Generativa")
elif opcion == "Tema2 - Metaverso y Gamificacion":
    st.image("images/expo4.png", caption="Pepper explicando Metaverso")
elif opcion == "Tema3 - Blockchain y Contratos Inteligentes":
    st.image("images/expo6.png", caption="Pepper explicando Blockchain")
```
## Instrucciones de ejecución

### 1. Ejecución de Pepper
```bash
python scripts/pepper_expo.py
```
### Chatbot
```bash
python scripts/chatbot.py
````
### Dashboard
```bash
streamlit run scripts/dashboard.py
````
Cuarto Punto: Documento en Overleaf
Este documento está en la carpeta /doc/ y contiene todos los pasos y evidencias.

Evidencia:
[Ver documento](Laboratorio_pepper.pdf)



## Autores
- **Rodian Daniel Garay Peralta**  
- **Mariana Lombana Rojas**

Docente: *Diego Alejandro Barragán Vargas*  
Universidad Santo Tomás  
5 de septiembre de 2025



