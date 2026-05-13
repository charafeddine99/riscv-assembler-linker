# RV32I Tabanlı Assembler ve Linker Sistemi

## Proje Hakkında

Bu proje, PicoRV32 işlemcisi için geliştirilmiş RV32I tabanlı özel bir assembler ve linker sistemidir. Sistem, assembly kaynak dosyalarını object dosyalarına dönüştürmekte ve birden fazla object modülünü linkleyerek FPGA üzerinde çalıştırılabilir executable çıktılar üretmektedir.

Proje Sistem Programlama dersi kapsamında geliştirilmiştir.

---

# Proje Özellikleri

## Assembler Özellikleri

- RV32I instruction desteği
- Two-pass assembler mimarisi
- Opcode table yönetimi
- Symbol table yönetimi
- Object dosya üretimi
- EXTDEF ve EXTREF desteği
- Relocation kaydı üretimi
- Syntax ve semantic hata kontrolü
- GUI tabanlı assembler arayüzü

## Linker Özellikleri

- Çoklu object dosyası linkleme
- ESTAB (External Symbol Table) oluşturma
- External symbol resolution işlemleri
- Relocation işlemleri
- HEX çıktı üretimi
- FPGA memory dosyası oluşturma

## FPGA Özellikleri

- PicoRV32 entegrasyonu
- BRAM memory initialization desteği
- Verilog simülasyon uyumluluğu
- GTKWave waveform analizi

---

# Kullanılan Teknolojiler

- Python
- PyQt5
- RISC-V RV32I ISA
- PicoRV32
- Verilog HDL
- GTKWave
- FPGA Simülasyon Ortamı

---

# Proje Dizini Yapısı

```bash id="8z5dbe"
project/
│
├── assembler/
│   ├── lexer.py
│   ├── parser.py
│   ├── opcode_table.py
│   ├── symbol_table.py
│   ├── object_generator.py
│   └── assembler_gui.py
│
├── linker/
│   ├── estab.py
│   ├── relocation.py
│   ├── linker.py
│   └── hex_generator.py
│
├── fpga/
│   ├── picorv32.v
│   ├── memory.v
│   ├── testbench.v
│   └── pico_bram.mem
│
├── build/
│   ├── MAIN.obj
│   ├── LOGIC.obj
│   └── IODRV.obj
│
├── screenshots/
│
├── report/
│
└── README.txt



Desteklenen Direktifler

Assembler sistemi aşağıdaki direktifleri desteklemektedir:

START
END
EXTDEF
EXTREF
CSECT



Object Dosya Formatı

Üretilen object dosyaları aşağıdaki kayıt türlerini içermektedir:

| Kayıt | Açıklama                     |
| ----- | ---------------------------- |
| OBJ   | Object modül başlığı         |
| DEF   | Export edilen semboller      |
| REF   | External symbol referansları |
| DAT   | Machine code verileri        |
| RLC   | Relocation kayıtları         |



Hata Yönetimi Özellikleri

Assembler sistemi aşağıdaki hata kontrol mekanizmalarını içermektedir:

Tanımsız etiket kontrolü

Duplicate label kontrolü

Geçersiz EXTREF/EXTDEF kontrolü

Adres taşma kontrolü

Syntax hata kontrolü

Geçersiz instruction kontrolü



Test Senaryoları

Projede aşağıdaki testler gerçekleştirilmiştir:

Instruction encoding testleri

Relocation testleri

Symbol resolution testleri

FPGA execution testleri

Hata yönetimi testleri

Sınır durum testleri



Takım Bilgisi

Bu proje Sistem Programlama dersi kapsamında dört kişilik ekip tarafından geliştirilmiştir.


Akademik Amaç

Bu proje eğitim ve akademik amaçlarla geliştirilmiştir.




Kaynaklar

RISC-V ISA Documentation

PicoRV32 GitHub Repository

Linkers and Loaders – John R. Levine

Computer Organization and Design RISC-V Edition


