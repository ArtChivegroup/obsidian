Berikut adalah Cheat Sheet (Panduan Cepat) untuk menggunakan PyAutoGUI:
#python

**Fungsi Umum**

- Mendapatkan posisi mouse saat ini: `pyautogui.position()`
- Mendapatkan resolusi layar saat ini: `pyautogui.size()`
- Memeriksa apakah koordinat X dan Y berada dalam layar: `pyautogui.onScreen(x, y)`

**Fail-Safes**

- Mengatur jeda 2,5 detik setelah setiap panggilan PyAutoGUI: `pyautogui.PAUSE = 2.5`
- Mengaktifkan fitur fail-safe yang menghentikan program jika mouse bergerak ke sudut kiri atas layar: `pyautogui.FAILSAFE = True`

**Fungsi Mouse**

- Menggerakkan mouse ke koordinat XY dalam beberapa detik tertentu: `pyautogui.moveTo(x, y, duration=num_seconds)`
- Menggerakkan mouse relatif terhadap posisi saat ini: `pyautogui.moveRel(xOffset, yOffset, duration=num_seconds)`
- Mengklik mouse (bisa disesuaikan dengan tombol dan jumlah klik): `pyautogui.click(x=moveToX, y=moveToY, clicks=num_of_clicks, interval=secs_between_clicks, button='left')`
- Klik kanan mouse: `pyautogui.rightClick(x=moveToX, y=moveToY)`
- Klik tengah mouse: `pyautogui.middleClick(x=moveToX, y=moveToY)`
- Klik ganda mouse: `pyautogui.doubleClick(x=moveToX, y=moveToY)`
- Klik tiga kali mouse: `pyautogui.tripleClick(x=moveToX, y=moveToY)`
- Menggulir halaman dengan mouse: `pyautogui.scroll(amount_to_scroll, x=moveToX, y=moveToY)`
- Menekan tombol mouse (down) dan melepaskan tombol mouse (up) secara terpisah: `pyautogui.mouseDown(x=moveToX, y=moveToY, button='left')`, `pyautogui.mouseUp(x=moveToX, y=moveToY, button='left')`

**Fungsi Keyboard**

- Mengetikkan teks atau karakter ke tempat kursor keyboard berada: `pyautogui.typewrite('Hello world!\\\\n', interval=secs_between_keys)`
- Mengetikkan daftar nama tombol keyboard: `pyautogui.typewrite(['a', 'b', 'c', 'left', 'backspace', 'enter', 'f1'], interval=secs_between_keys)`
- Menjalankan hotkey keyboard (contoh: Ctrl-C atau Ctrl-V): `pyautogui.hotkey('ctrl', 'c')`
- Menekan tombol keyboard secara terpisah (down dan up): `pyautogui.keyDown(key_name)`, `pyautogui.keyUp(key_name)`

**Fungsi Kotak Pesan**

- Menampilkan kotak pesan informasi: `pyautogui.alert('This displays some text with an OK button.')`
- Menampilkan kotak pesan konfirmasi: `pyautogui.confirm('This displays text and has an OK and Cancel button.')`
- Menampilkan kotak pesan prompt: `pyautogui.prompt('This lets the user type in a string and press OK.')`

**Fungsi Tangkapan Layar**

- Mengambil tangkapan layar: `pyautogui.screenshot()`
- Mengambil tangkapan layar dan menyimpannya ke file: `pyautogui.screenshot('foo.png')`
- Mencari gambar pada layar: `pyautogui.locateOnScreen('looksLikeThis.png')`
- Mencari semua lokasi gambar yang cocok pada layar: `list(pyautogui.locateAllOnScreen('looksLikeThis.png'))`
- Mencari pusat lokasi gambar pada layar: `pyautogui.locateCenterOnScreen('looksLikeThis.png')`

Pastikan Anda telah menginstal modul Pillow/PIL jika ingin menggunakan fitur tangkapan layar.

Demikianlah Panduan Cepat Penggunaan PyAutoGUI. Anda dapat menggunakannya untuk mengotomatisasi tugas di komputer Anda.