import re
from datetime import datetime

def proses_tanggal(teks):
    """
    Mencari tanggal dalam format YYYY-MM-DD, mengubahnya ke DD-MM-YYYY,
    dan menghitung selisih hari dengan tanggal sekarang.

    Args:
        teks (str): Teks yang akan dianalisis.

    Returns:
        list: List berisi string hasil pemrosesan setiap tanggal yang ditemukan.
    """
    tanggal_regex = r'\d{4}-\d{2}-\d{2}'
    tanggal_ditemukan = re.findall(tanggal_regex, teks)
    hasil = []
    tanggal_sekarang = datetime.now()

    for tanggal_str in tanggal_ditemukan:
        try:
            tanggal_obj = datetime.strptime(tanggal_str, '%Y-%m-%d')
            tanggal_format_baru = tanggal_obj.strftime('%d-%m-%Y')
            selisih = tanggal_sekarang - tanggal_obj
            hasil.append(f"{tanggal_format_baru} 00:00:00 selisih {selisih.days} hari")
        except ValueError:
            hasil.append(f"Format tanggal tidak valid: {tanggal_str}")
    return hasil

# Contoh penggunaan
teks_input = "Pada tanggal 1945-08-17 Indonesia merdeka. Indonesia memiliki beberapa pahlawan nasional, seperti Pangeran Diponegoro (TL: 1785-11-11), Pattimura (TL: 1783-06-08) dan Ki Hajar Dewantara (1889-05-02)."
hasil_proses = proses_tanggal(teks_input)
for item in hasil_proses:
    print(item)

teks_lain = input("Masukkan teks yang mengandung tanggal (YYYY-MM-DD): ")
hasil_proses_lain = proses_tanggal(teks_lain)
for item in hasil_proses_lain:
    print(item)
