## addblock.py (Main)
[[./Pyautogui Doc|Pyautogui Doc]]
``` Python
import cv2

import pyautogui

import numpy as np

import subprocess

import time

  

# Fungsi untuk menghentikan perulangan dengan menekan tombol tertentu

def check_for_exit_key():

    if pyautogui.hotkey('ctrl', 'c'):

        exit()  # Tekan Ctrl+C untuk keluar dari perulangan

  

# Lokasi awal mouse (X = 801, Y = 205)

start_x, start_y = 801, 205

  

# Lokasi tujuan mouse (X = 663, Y = 201)

end_x, end_y = 663, 201

  

# Jumlah iterasi (misalnya 100 kali)

iterations = 100

  

while iterations > 0:

    # Countdown 3 detik sebelum mencetak lokasi mouse

    #for i in range(3, 0, -1):

    #    print(f"Countdown: {i} detik")

    #    time.sleep(1)  # Jeda selama 1 detik

  

    # Jalankan skrip 'block.py'

    subprocess.run(['python', 'block.py'])

  

    # Melakukan klik dan drag dari lokasi awal ke lokasi tujuan

    pyautogui.mouseDown(start_x, start_y)  # Klik mouse di lokasi awal

    pyautogui.dragTo(end_x, end_y, duration=1)  # Tarik mouse ke lokasi tujuan dengan kecepatan drag selama 1 detik

    pyautogui.mouseUp(end_x, end_y)  # Lepaskan mouse di lokasi tujuan

  

    # Jalankan skrip 'hand.py'

    subprocess.run(['python', 'hand.py'])

  

    # HIT BLOCK 1 (7 kali klik dengan jeda yang lebih cepat)

    for _ in range(7):

        pyautogui.click(826, 211)

        time.sleep(0.2)  # Jeda 0.2 detik antara setiap klik

  

    # HIT BLOCK 2 (7 kali klik dengan jeda yang lebih cepat)

    for _ in range(7):

        pyautogui.click(758, 200)

        time.sleep(0.2)  # Jeda 0.2 detik antara setiap klik

  

    # HIT BLOCK 3 (7 kali klik dengan jeda yang lebih cepat)

    for _ in range(7):

        pyautogui.click(692, 203)

        time.sleep(0.2)  # Jeda 0.2 detik antara setiap klik

    # Jalankan skrip 'enter.py'

    subprocess.run(['python', 'enter.py'])

  

    # Jalankan skrip 'jalan.py'

    subprocess.run(['python', 'jalan.py'])

  
  

    iterations -= 1  # Kurangi jumlah iterasi

    check_for_exit_key()  # Periksa apakah Anda ingin keluar

  

    # Cek apakah sudah mencapai 50 iterasi

    if iterations % 20 == 0:

        print("Menjalankan seedfull.py")

        subprocess.run(['python', 'seedfull.py'])

  

print("Perulangan selesai.")
```

## block.py
``` Python
import cv2

import pyautogui

import numpy as np

  

# Nama file gambar yang akan dicari (ganti dengan nama gambar Anda)

image_file = 'block.png'

  

# Baca gambar yang akan dicari

template = cv2.imread(image_file, cv2.IMREAD_COLOR)

  

# Ambil tangkapan layar seluruh layar

screenshot = pyautogui.screenshot()

  

# Ubah tangkapan layar ke format yang dapat diolah oleh OpenCV

screenshot = np.array(screenshot)  # Konversi ke NumPy array

screenshot = cv2.cvtColor(screenshot, cv2.COLOR_RGB2BGR)

  

# Lakukan pencarian gambar "block.png" menggunakan OpenCV

result = cv2.matchTemplate(screenshot, template, cv2.TM_CCOEFF_NORMED)

min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(result)

  

# Dapatkan koordinat lokasi yang cocok

top_left = max_loc

h, w, _ = template.shape

bottom_right = (top_left[0] + w, top_left[1] + h)

  

# Temukan tengah gambar "block.png" yang cocok

center_x = top_left[0] + (w // 2)

center_y = top_left[1] + (h // 2)

  

# Klik pada tengah gambar "block.png" yang cocok menggunakan PyAutoGUI

pyautogui.click(center_x, center_y)
```

## hand.py
```Python
import cv2

import pyautogui

import numpy as np

  

# Nama file gambar "hand.png"

hand_image_file = 'hand.png'

  

# Baca gambar "hand.png"

hand_template = cv2.imread(hand_image_file, cv2.IMREAD_COLOR)

  

# Ambil tangkapan layar seluruh layar

screenshot = pyautogui.screenshot()

  

# Ubah tangkapan layar ke format yang dapat diolah oleh OpenCV

screenshot = np.array(screenshot)  # Konversi ke NumPy array

screenshot = cv2.cvtColor(screenshot, cv2.COLOR_RGB2BGR)

  

# Lakukan pencarian gambar "hand.png" menggunakan OpenCV

result = cv2.matchTemplate(screenshot, hand_template, cv2.TM_CCOEFF_NORMED)

min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(result)

  

# Pastikan cocokan dengan gambar "hand.png" memiliki tingkat kecocokan yang memadai (sesuaikan dengan kebutuhan Anda)

if max_val > 0.8:  # Sesuaikan nilai kecocokan (0.8) sesuai dengan gambar Anda

    top_left = max_loc

    h, w, _ = hand_template.shape

    bottom_right = (top_left[0] + w, top_left[1] + h)

  

    # Temukan tengah gambar "hand.png" yang cocok

    center_x = top_left[0] + (w // 2)

    center_y = top_left[1] + (h // 2)

  

    # Klik pada tengah gambar "hand.png" yang cocok menggunakan PyAutoGUI

    pyautogui.click(center_x, center_y)
```

## enter.py
```Python
import pyautogui

import cv2

  

# Lokasi file gambar "enter.png" (ganti dengan lokasi file yang sesuai)

gambar_enter = "enter.png"

  

# Fungsi untuk mendeteksi apakah gambar "enter.png" terlihat di layar

def cek_gambar_enter():

    screenshot = pyautogui.screenshot()  # Ambil tangkapan layar

    screenshot.save("screenshot.png")  # Simpan tangkapan layar sementara

    tangkapan_layar = cv2.imread("screenshot.png")  # Baca tangkapan layar menggunakan OpenCV

    gambar = cv2.imread(gambar_enter)  # Baca gambar "enter.png" menggunakan OpenCV

    hasil = cv2.matchTemplate(tangkapan_layar, gambar, cv2.TM_CCOEFF_NORMED)  # Cocokkan gambar

    threshold = 0.8  # Ambang batas untuk hasil pencocokan (dapat disesuaikan)

    lokasi = cv2.minMaxLoc(hasil)[3]  # Temukan lokasi pencocokan terbaik

  

    if hasil[lokasi[1]][lokasi[0]] >= threshold:

        return True  # Jika gambar terdeteksi, kembalikan True

    return False  # Jika tidak, kembalikan False

  

# Fungsi untuk menjalankan skrip enter jika gambar "enter.png" terdeteksi

def jalankan_enter():

    print("Menjalankan skrip enter...")

    pyautogui.press('enter')  # Simulasikan tekanan tombol "Enter"

  

# Cek apakah gambar "enter.png" terdeteksi

if cek_gambar_enter():

    jalankan_enter()  # Jalankan skrip enter jika gambar terdeteksi

else:

    print("Tidak ada gambar enter yang terdeteksi.")
```

## jalan.py
```Python
import pyautogui

import time  

  

time.sleep(0.5)

  

# Tekan tanda panah ke kanan dan tahan selama 0,5 detik

pyautogui.keyDown('right')

time.sleep(0.5)

pyautogui.keyUp('right')

  

# Tekan tanda panah ke atas dua kali

pyautogui.keyUp('up')

pyautogui.keyDown('up')

  

# Diam selama 0,5 detik

time.sleep(0.5)

  

# Tekan tanda panah ke kiri dan tahan selama 0,5 detik

pyautogui.keyDown('left')

time.sleep(0.5)

pyautogui.keyUp('left')
```
## seedfull.py
```Python
import cv2

import pyautogui

import numpy as np

import subprocess

import time

  

# Nama file gambar yang akan dicari

seedfull_image = 'seedfull.png'

  

# Fungsi untuk memeriksa apakah gambar ada di layar

def check_for_image(image_path):

    template = cv2.imread(image_path, cv2.IMREAD_COLOR)

    screenshot = pyautogui.screenshot()

    screenshot = np.array(screenshot)

    screenshot = cv2.cvtColor(screenshot, cv2.COLOR_RGB2BGR)

  

    result = cv2.matchTemplate(screenshot, template, cv2.TM_CCOEFF_NORMED)

    min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(result)

  

    threshold = 0.9  # Sesuaikan dengan nilai ambang yang sesuai

    if max_val >= threshold:

        return True

    return False

  

# Pemeriksaan

if check_for_image(seedfull_image):

    print("Seed sudah penuh, menghentikan program")

else:

    print("Seed belum penuh, melanjutkan ke addblock.py")

    addblock_process = subprocess.Popen(['python', 'addblock.py'])  # Menjalankan addblock.py

  

while True:

    if check_for_image(seedfull_image):

        print("Seed telah menjadi penuh, menghentikan addblock.py dan menjalankan wa.py")

        addblock_process.terminate()  # Menghentikan proses addblock.py

        subprocess.run(['python', 'wa.py'])  # Menjalankan wa.py

        break

    time.sleep(1)  # Tunggu sebentar dan cek kembali 
```

#python 