import json
import math

def main():
    stok_bengkel = {
        "FLTR-01": {"nama": "Filter Oli", "harga": 50000, "stok": 15},
        "BRK-22": {"nama": "Kampas Rem Depan", "harga": 250000, "stok": 8}
    }
    
    print("=== Sistem Manajemen Part Bengkel ===")
    
    while True:
        print("\nMenu:")
        print("1. Lihat Stok")
        print("2. Tambah Part Baru")
        print("3. Keluar")
        
        pilihan = input("Pilih menu (1/2/3): ")
        
        if pilihan == "1":
            print("\n--- Daftar Suku Cadang ---")
            for kode, info in stok_bengkel.items():
                print(f"[{kode}] {info['nama']} | Stok: {info['stok']} | Harga: Rp{info['harga']:,}")
        
        elif pilihan == "2":
            kode_baru = input("Masukkan kode part baru: ").upper()
            nama_baru = input("Masukkan nama part: ")
            try:
                harga_baru = float(input("Masukkan harga satuan: "))
                jumlah_stok = int(input("Masukkan jumlah stok awal: "))
                
                stok_bengkel[kode_baru] = {
                    "nama": nama_baru, 
                    "harga": harga_baru, 
                    "stok": jumlah_stok
                }
                print(f"Sukses: {nama_baru} telah ditambahkan ke sistem.")
            except ValueError:
                print("Input gagal: Harga dan Stok harus berupa angka!")

        elif pilihan == "3":
            total_nilai = sum(item['harga'] * item['stok'] for item in stok_bengkel.values())
            pajak = total_nilai * 0.11 
            
            total_akhir = math.ceil(total_nilai + pajak)
            
            data_json = json.dumps(stok_bengkel, indent=2)
            
            print("\n--- Laporan Penutup ---")
            print(f"Total Nilai Aset (inc. PPN): Rp{total_akhir:,}")
            print("Data berhasil diringkas ke format JSON.")
            break
        
        else:
            print("Pilihan tidak valid!")

if __name__ == "__main__":
    main()
