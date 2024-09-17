#   Tugas 4 PBO - Clock Display

## NumberDisplay.java
```
/* Kelas NumberDisplay merepresentasikan tampilan angka digital yang dapat menyimpan nilai dari nol hingga batas yang diberikan. Batas tersebut dapat 
 * ditentukan saat membuat tampilan. Nilai berkisar dari nol (inklusif) hingga batas-1. Jika digunakan, misalnya, untuk detik pada jam digital, batasnya 
 * adalah 60, sehingga menghasilkan nilai tampilan dari 0 hingga 59. Ketika ditambah, tampilan otomatis kembali ke nol saat mencapai batas.*/

public class NumberDisplay{
    private int batas;
    private int nilai;

    /* Konstruktor untuk menetapkan batas di mana tampilan akan kembali ke nol.*/
    public NumberDisplay(int batasKembali){
        batas = batasKembali;
        nilai = 0;
    }

    /* Mengembalikan nilai saat ini*/
    public int getNilai(){
        return nilai;
    }

    /* Mengembalikan nilai tampilan (yaitu, nilai saat ini sebagai String dua digit. Jika nilainya kurang dari sepuluh, akan ditambahkan angka nol di depan).*/
    public String getNilaiTampilan(){
        if(nilai < 10){
            return "0" + nilai;
        } else {
            return "" + nilai;
        }
    }

    /* Menetapkan nilai tampilan ke nilai baru yang ditentukan. Jika nilai baru kurang dari nol atau melebihi batas, tidak melakukan apa-apa.*/
    public void setNilai(int nilaiBaru){
        if((nilaiBaru >= 0) && (nilaiBaru < batas)){
            nilai = nilaiBaru;
        }
    }

    /* Menambah nilai tampilan sebanyak satu, kembali ke nol jika batas tercapai.*/
    public void increment(){
        nilai = (nilai + 1) % batas;
    }
}
```
### Penjelasan NumberDisplay.java
NumberDisplay adalah kelas yang menangani penghitungan dan penampilan angka, khususnya pada jam dan menit. Berikut adalah fungsi dari kelas ini:

Atribut:
- ```nilai```: Menyimpan nilai saat ini (seperti jam atau menit).
- ```batas``` : Menyimpan batas maksimum angka (24 untuk jam, 60 untuk menit).

Metode utama:
- ```increment()``` : Menambah nilai yang disimpan. Jika nilai mencapai batas, ia akan kembali ke 0. Ini berguna untuk jam (dari 23 ke 0) dan menit (dari 59 ke 0).
- ```getNilai()```: Mengembalikan nilai saat ini.
- ```setNilai(int nilaiBaru)``` : Mengatur nilai ke nilai baru.
- ```getNilaiTampilan()``` : Mengembalikan nilai dalam bentuk string, biasanya dalam format dua digit (misalnya, "08" bukan "8").

Cara Kerja:
Misalnya, untuk menampilkan menit :
Jika menit saat ini adalah 59, ketika metode increment() dipanggil, menit akan menjadi 0 dan juga menyebabkan jam bertambah satu.

## ClockDisplay.java
```
/* Jam ini menampilkan jam dan menit. Rentang waktunya adalah 00:00 (tengah malam) hingga 23:59 (satu menit sebelum tengah malam).
 * Tampilan jam menerima "tanda detik" (melalui metode timeTick) setiap menit
 * dan bereaksi dengan menambah tampilan. Ini dilakukan dengan cara jam biasa:
 * jam bertambah ketika menit kembali ke nol. */

public class ClockDisplay {
    private NumberDisplay jam;
    private NumberDisplay menit;
    private String stringTampilan;    // mensimulasikan tampilan yang sebenarnya
    
    /* Konstruktor ini membuat jam baru diatur pada 00:00.*/
    public ClockDisplay(){
        jam = new NumberDisplay(24);
        menit = new NumberDisplay(60);
        perbaruiTampilan();
    }

    /* Konstruktor ini membuat jam baru diatur pada waktu yang ditentukan oleh parameter.*/
    public ClockDisplay(int jam, int menit){
        this.jam = new NumberDisplay(24);
        this.menit = new NumberDisplay(60);
        aturWaktu(jam, menit);
    }

    /* Metode ini dipanggil setiap satu menit - ini membuat tampilan jam maju satu menit.*/
    public void detikWaktu(){
        menit.increment();
        if(menit.getNilai() == 0){  // baru saja kembali ke nol
            jam.increment();
        }
        perbaruiTampilan();
    }

    /* Mengatur waktu tampilan ke jam dan menit yang ditentukan. */
    public void aturWaktu(int jam, int menit){
        this.jam.setNilai(jam);
        this.menit.setNilai(menit);
        perbaruiTampilan();
    }

    /* Mengembalikan waktu saat ini dari tampilan ini dalam format HH:MM. */
    public String ambilWaktu(){
        return stringTampilan;
    }
    
    /*Memperbarui string internal yang mewakili tampilan.*/
    private void perbaruiTampilan(){
        stringTampilan = jam.getNilaiTampilan() + ":" + menit.getNilaiTampilan();
    }
}
```
### Penjelasan ClockDisplay.java
Kelas ClockDisplay merupakan kelas utama yang menggabungkan dua objek NumberDisplay untuk merepresentasikan jam dan menit pada sebuah jam digital.

Atribut:
- ```jam``` : Objek NumberDisplay yang menyimpan nilai jam (dari 0 hingga 23).
- ```menit``` : Objek NumberDisplay yang menyimpan nilai menit (dari 0 hingga 59).
- ```stringTampilan``` : Sebuah string yang menyimpan tampilan waktu dalam format "HH".

Konstruktor:
Konstruktor pertama membuat objek ClockDisplay dengan jam diatur ke 00:00.
Konstruktor kedua memungkinkan pengguna menentukan jam dan menit awal secara manual.

Metode Utama:
- ```detikWaktu()``` : Metode ini memajukan menit pada objek ClockDisplay. Ketika menit mencapai 60 (menjadi 0), metode ini juga akan memajukan jam. Jadi, metode ini seperti pengatur waktu yang menambah waktu setiap menit.
- ```aturWaktu(int jam, int menit)``` : Mengatur waktu pada objek ClockDisplay sesuai dengan parameter jam dan menit yang diberikan.
- ```ambilWaktu()``` : Mengembalikan waktu saat ini dalam format "HH" sebagai string, yang dapat digunakan untuk ditampilkan ke pengguna.
- ```perbaruiTampilan()``` : Metode ini menggabungkan nilai dari objek jam dan menit menjadi sebuah string dengan format "HH" yang diperbarui setiap kali waktu berubah.


Cara Kerja:
Saat objek ClockDisplay dibuat, ia akan memulai dengan nilai waktu default (00:00) atau waktu yang diatur oleh pengguna.
Setiap kali metode detikWaktu() dipanggil, menit akan bertambah satu. Jika menit mencapai 60, menit akan kembali ke 0 dan jam akan bertambah satu.
Waktu yang diperbarui akan disimpan sebagai string di stringTampilan dan bisa diakses menggunakan metode ambilWaktu().
Secara keseluruhan, objek NumberDisplay digunakan untuk menangani penambahan jam dan menit, sementara ClockDisplay mengelola tampilan dan pembaruan waktu pada jam digital.
