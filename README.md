# PerhitunganHari
 Tugas 4 - Irfazi - 2210010277

# 1. Deskripsi Program
Aplikasi ini menghitung jumlah hari dalam bulan tertentu pada tahun tertentu yang dipilih oleh pengguna.

- Input: Pengguna memilih bulan dari JComboBox dan memasukkan tahun menggunakan JSpinner.
- Penggunaan JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun.
- Output: Setelah tombol ditekan, aplikasi menampilkan jumlah hari dalam bulan yang dipilih.
  
# 2. Komponen GUI: 
JFrame, JPanel, JLabel, JComboBox, JSpinner, JButton, JCalendar
- JPanel: Untuk menampung komponen lain.
- JLabel: Berfungsi sebagai label untuk elemen input dan output.
- JComboBox: Untuk memilih bulan.
- JSpinner: Untuk memasukkan tahun.
- JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun secara visual.
- JButton: Tombol untuk menghitung jumlah hari, menghitung selisih hari, hapus dan keluar

- Button Hitung

private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
       btnHitung.addActionListener((ActionEvent e) -> {
        MenghitungHari();
    });
    }    

- Button Hitung Selisih Hari

 private void btnSelisihActionPerformed(java.awt.event.ActionEvent evt) {                                           
       btnSelisih.addActionListener((ActionEvent e) -> {
            SelisihHari();
        });
    }      

- Button Hapus

private void btnHapusSelisihActionPerformed(java.awt.event.ActionEvent evt) {                                                
       btnHapusSelisih.addActionListener((ActionEvent e) -> {
            HapusPerselisihan();
        });
       
    }      

Metode hapusinput() di panggil
/ private void Hapus() {
        cbxBulan.setSelectedIndex(0);
        spTahun.setValue(2023);
        jCalendar.setCalendar(Calendar.getInstance());
        filedHasil.setText("Jumlah hari: ");
    }
- Button Keluar

    private void btnKeluarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        System.exit(0);
    }

# 3. Logika Program: 
Penggunaan API tanggal (LocalDate), Perhitungan hari dalam bulan, Perhitungan tahun kabisat

# 4. Events:
* ActionListener untuk tombol Hitung

 private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    btnHitung.addActionListener((ActionEvent e) -> {
        kalkulatorhari();
    });
    

Penjelasan Kode :
ActionListener pada buttonHitung Saat tombol ditekan, metode kalkulatorhari() akan dipanggil.

 private void MenghitungHari() {
        int month = cbxBulan.getSelectedIndex() + 1;
        int year = (int) spTahun.getValue();
        Calendar selectedDate = jCalendar.getCalendar();
        selectedDate.set(Calendar.MONTH, month - 1);
        selectedDate.set(Calendar.YEAR, year);
        jCalendar.setCalendar(selectedDate);
        YearMonth yearMonth = YearMonth.of(year, month);
        int daysInMonth = yearMonth.lengthOfMonth();
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();
        filedHasil.setText(String.format(
                "Jumlah hari: %d, Hari pertama: %s, Hari terakhir: %s",
                daysInMonth, firstDay.getDayOfWeek(), lastDay.getDayOfWeek()
        ));
     
    }
    
Metode hitungHari():
- cbxBulan.getSelectedIndex() mendapatkan indeks bulan yang dipilih (dengan Januari sebagai indeks 0), lalu menambahkan 1 agar sesuai dengan bulan kalender (Januari = 1).
- spinnerTahun.getValue() mengambil nilai tahun yang dipilih.
- Menghitung jumlah hari: YearMonth.of(tahun, bulan) membuat objek YearMonth untuk bulan dan tahun yang dipilih. Metode lengthOfMonth() kemudian digunakan untuk mendapatkan jumlah hari pada bulan tersebut.
- Hasil jumlah hari ditampilkan di labelHasil.
  
* ChangeListener pada JSpinner untuk input tahun

private void spTahunStateChanged(javax.swing.event.ChangeEvent evt) {                                     
        spTahun.addChangeListener((ChangeEvent e) -> {
        BulanTahun();
    });
    }     

Listener untuk mengubah bulan dan tahun pada JCalendar saat ComboBox atau Spinner berubah

 private void cbxBulanItemStateChanged(java.awt.event.ItemEvent evt) {                                          
        cbxBulan.addItemListener((ItemEvent e) -> {
            BulanTahun();
        });
    }   

Metode pembaruankalender() akan di panggil

/private void BulanTahun() {
        int month = cbxBulan.getSelectedIndex(); 
        int year = (int) spTahun.getValue();

        Calendar selectedDate = Calendar.getInstance();
        selectedDate.set(Calendar.YEAR, year);
        selectedDate.set(Calendar.MONTH, month); 
        selectedDate.set(Calendar.DAY_OF_MONTH, 1);
        jCalendar.setCalendar(selectedDate); 
    }

# 5. Variasi:
* Tampilkan informasi tambahan seperti hari pertama dan terakhir dalam bulan tersebut

LocalDate startDate = startCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
        
LocalDate endDate = endCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();

* Integrasikan fitur untuk menghitung selisih hari antara dua tanggal

 private void btnSelisihActionPerformed(java.awt.event.ActionEvent evt) {                                           
       btnSelisih.addActionListener((ActionEvent e) -> {
            SelisihHari();
        });
    }

Metode selisihHari() akan di panggil

private void SelisihHari() {
        Calendar startCal = jCalendarAwal.getCalendar();
        
        Calendar endCal = jCalendarAkhir.getCalendar();
        
        LocalDate startDate = startCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
        
        LocalDate endDate = endCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
        
        long day = ChronoUnit.DAYS.between(startDate, endDate);
        
        filedHasilSelisih.setText("Selisih hari : " + day + " hari");
    }
    

# Hasil Gambar Project Ketika di Run
![]().
## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    10    |
|  2  | Logika Program   |    20    |
|  3  | Event            |    20    |
|  4  | Kesesuaian UI    |    20    |
|  5  | Memenuhi Variasi |    40    |
|     | TOTAL        | 100 |
