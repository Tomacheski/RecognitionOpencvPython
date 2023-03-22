# RecognitionOpencvPython
#Recognition wood diameter with python OpenCv

import cv2
import numpy as np

# Carregue a imagem
img = cv2.imread('imagem.jpg')

# Converter imagem para escala de cinza
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Aplicar filtro Gaussiano para reduzir ruído
gray = cv2.GaussianBlur(gray, (5, 5), 0)

# Detectar bordas com Canny
edges = cv2.Canny(gray, 50, 100)

# Encontrar contornos na imagem
contours, hierarchy = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

# Selecionar o maior contorno
contour = max(contours, key=cv2.contourArea)

# Encontrar o círculo que melhor se ajusta ao contorno
(x, y), radius = cv2.minEnclosingCircle(contour)

# Converter o raio de pixels para milímetros
mm_per_pixel = 0.5 # Especificar aqui o tamanho em milímetros de cada pixel
diameter_mm = radius * 2 * mm_per_pixel

# Desenhar o círculo na imagem
cv2.circle(img, (int(x), int(y)), int(radius), (0, 255, 0), 2)

# Mostrar o resultado
cv2.imshow('imagem', img)
cv2.imshow('imagem2', gray)
print(f'Diâmetro: {diameter_mm:.2f} mm')

# Esperar até que uma tecla seja pressionada
cv2.waitKey(0)
cv2.destroyAllWindows()
