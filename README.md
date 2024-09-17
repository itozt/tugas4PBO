#   Tugas 4 PBO - Clock Display

```
/* Kelas NumberDisplay merepresentasikan tampilan angka digital yang dapat menyimpan nilai dari nol hingga batas yang diberikan. Batas tersebut dapat 
 * ditentukan saat membuat tampilan. Nilai berkisar dari nol (inklusif) hingga batas-1. Jika digunakan, misalnya, untuk detik pada jam digital, batasnya 
 * adalah 60, sehingga menghasilkan nilai tampilan dari 0 hingga 59. Ketika ditambah, tampilan otomatis kembali ke nol saat mencapai batas.
 */
public class NumberDisplay{
    private int batas;
    private int nilai;
    /* Konstruktor untuk objek kelas NumberDisplay.
     * Menetapkan batas di mana tampilan akan kembali ke nol.
     */
    public NumberDisplay(int batasKembali){
        batas = batasKembali;
        nilai = 0;
    }

    /*Mengembalikan nilai saat ini*/
    public int getNilai(){
        return nilai;
    }

    /*Mengembalikan nilai tampilan (yaitu, nilai saat ini sebagai String dua digit. Jika nilainya kurang dari sepuluh, akan ditambahkan angka nol di depan).*/
    public String getNilaiTampilan(){
        if(nilai < 10){
            return "0" + nilai;
        } else {
            return "" + nilai;
        }
    }

    /* Menetapkan nilai tampilan ke nilai baru yang ditentukan. Jika nilai baru 
     * kurang dari nol atau melebihi batas, tidak melakukan apa-apa.*/
    public void setNilai(int nilaiBaru){
        if((nilaiBaru >= 0) && (nilaiBaru < batas)) {
            nilai = nilaiBaru;
        }
    }

    /* Menambah nilai tampilan sebanyak satu, kembali ke nol jika batas tercapai.*/
    public void tambahNilai(){
        nilai = (nilai + 1) % batas;
    }
}
```
