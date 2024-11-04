
# Project Perhitungan Umur

Program Java ini merupakan `plikasi GUI` (Graphical User Interface) yang dibuat menggunakan `javax.swing`, berfungsi untuk mengonversi suhu antar berbagai satuan: Celsius, Fahrenheit, Reamur, dan Kelvin. Pengguna dapat memilih satuan suhu yang diinginkan melalui radio button dan melakukan konversi sesuai pilihan.



# Deskripsi

Aplikasi ini memanfaatkan komponen `JFrame` untuk membangun antarmuka pengguna yang interaktif. Pengguna dapat memilih tanggal lahir melalui `dateChooser`, dan aplikasi akan menghitung serta menampilkan usia dalam format tahun, bulan, dan hari. Di samping itu, aplikasi ini terintegrasi dengan API eksternal untuk menampilkan peristiwa-peristiwa sejarah yang terjadi pada tanggal ulang tahun pengguna, memberikan pengalaman yang informatif dan menarik.

# Features

**Fitur Utama**

Input Suhu: Pengguna dapat memasukkan nilai suhu yang ingin dikonversi di `JTextField`.
Pilihan Satuan Suhu: Pengguna memilih satuan asal dan tujuan konversi, menggunakan `ComboBox` untuk satuan asal dan `RadioButton` untuk satuan tujuan.
Arah Konversi: Terdapat logika yang mengatur konversi antara Celsius, Fahrenheit, Kelvin, dan Reamur.
Listener Otomatis: Program memantau perubahan input suhu secara otomatis dan langsung menghitung ulang hasilnya.
Pesan Kesalahan: Jika input yang dimasukkan tidak valid, program akan menampilkan pesan kesalahan.
Dari file Suhu.form, terlihat bahwa aplikasi ini menggunakan NetBeans untuk pengaturan layout, memanfaatkan GridBagLayout dan beberapa komponen swing untuk mendukung desain antarmuka. ​
        import java.awt.event.ActionListener;
        import java.awt.event.ActionEvent;
        import javax.swing.event.DocumentEvent;
        import javax.swing.event.DocumentListener;


        public class Suhu extends javax.swing.JFrame {

        private String arahKonversi = "CtoF"; // Default arah konversi
        private double suhuInput; // Untuk menyimpan nilai input suhu
        private double hasilKonversi; // Untuk menyimpan hasil konversi

        public Suhu() {
            initComponents();
            setupListeners(); // Mengatur listener
        }
        
        private void setupListeners() {
        // Listener untuk tombol konversi
        tombolKonversi.addActionListener(e -> lakukanKonversi());
        
        // Listener untuk JTextField agar mendeteksi perubahan input suhu
        textFieldSuhu.getDocument().addDocumentListener(new DocumentListener() {
            @Override
            public void insertUpdate(DocumentEvent e) {
                lakukanKonversi(); // Panggil metode konversi saat ada perubahan
            }

            @Override
            public void removeUpdate(DocumentEvent e) {
                lakukanKonversi(); // Panggil metode konversi saat ada perubahan
            }

            @Override
            public void changedUpdate(DocumentEvent e) {
                lakukanKonversi(); // Panggil metode konversi saat ada perubahan
            }
        });

        // Listener untuk RadioButton Fahrenheit
        radioButtonFahrenheit.addActionListener(e -> {
            arahKonversi = "toF"; // Konversi ke Fahrenheit
            lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
        });

        // Listener untuk RadioButton Reamur
        radioButtonReamur.addActionListener(e -> {
            arahKonversi = "toR"; // Konversi ke Reamur
            lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
        });

        // Listener untuk RadioButton Kelvin
        radioButtonKelvin.addActionListener(e -> {
            arahKonversi = "toK"; // Konversi ke Kelvin
            lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
        });
        
        // Listener untuk RadioButton Kelvin
        radioButtonCelcius.addActionListener(e -> {
            arahKonversi = "toC"; // Konversi ke Celcius
            lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
        });

        // Listener untuk ComboBox Konversi Dari
        comboBoxKonversiDari.addActionListener(e -> {
            lakukanKonversi(); // Panggil metode konversi saat pilihan diubah
        });
    }

        
        private void lakukanKonversi() {
        try {
            // Mengambil nilai dari JTextField
            suhuInput = Double.parseDouble(textFieldSuhu.getText());

            // Mendapatkan pilihan dari ComboBox
            String konversiDari = comboBoxKonversiDari.getSelectedItem().toString();

            // Melakukan konversi berdasarkan arah konversi
            switch (konversiDari) {
                case "Celcius":
                    if (arahKonversi.equals("toF")) {
                        hasilKonversi = suhuInput * 9/5 + 32; // Celcius ke Fahrenheit
                    } else if (arahKonversi.equals("toR")) {
                        hasilKonversi = suhuInput * 4/5; // Celcius ke Reamur
                    } else if (arahKonversi.equals("toK")) {
                        hasilKonversi = suhuInput + 273.15; // Celcius ke Kelvin
                    }
                    break;
                case "Fahrenheit":
                    if (arahKonversi.equals("toC")) {
                        hasilKonversi = (suhuInput - 32) * 5/9; // Fahrenheit ke Celcius
                    } else if (arahKonversi.equals("toR")) {
                        hasilKonversi = (suhuInput - 32) * 4/9; // Fahrenheit ke Reamur
                    } else if (arahKonversi.equals("toK")) {
                        hasilKonversi = (suhuInput - 32) * 5/9 + 273.15; // Fahrenheit ke Kelvin
                    }
                    break;
                case "Reamur":
                    if (arahKonversi.equals("toC")) {
                        hasilKonversi = suhuInput * 5/4; // Reamur ke Celcius
                    } else if (arahKonversi.equals("toF")) {
                        hasilKonversi = suhuInput * 9/4 + 32; // Reamur ke Fahrenheit
                    } else if (arahKonversi.equals("toK")) {
                        hasilKonversi = suhuInput * 5/4 + 273.15; // Reamur ke Kelvin
                    }
                    break;
                case "Kelvin":
                    if (arahKonversi.equals("toC")) {
                        hasilKonversi = suhuInput - 273.15; // Kelvin ke Celcius
                    } else if (arahKonversi.equals("toF")) {
                        hasilKonversi = (suhuInput - 273.15) * 9/5 + 32; // Kelvin ke Fahrenheit
                    } else if (arahKonversi.equals("toR")) {
                        hasilKonversi = (suhuInput - 273.15) * 4/5; // Kelvin ke Reamur
                    }
                    break:
                default:
                    hasilKonversi = suhuInput; // Jika tidak ada konversi
                    break;
            }

            // Menampilkan hasil konversi di label output
            labelHasil.setText(String.format("%.2f", hasilKonversi));
        } catch (NumberFormatException ex) {
            // Tampilkan pesan kesalahan jika input tidak valid
            labelHasil.setText("Masukkan angka yang valid.");
        }
    }

        /**
        * This method is called from within the constructor to initialize the form.
        * WARNING: Do NOT modify this code. The content of this method is always
        * regenerated by the Form Editor.
        */
        @SuppressWarnings("unchecked")
        // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
        private void initComponents() {
            java.awt.GridBagConstraints gridBagConstraints;

            buttonGroup1 = new javax.swing.ButtonGroup();
            jPanel1 = new javax.swing.JPanel();
            jLabel1 = new javax.swing.JLabel();
            jLabel2 = new javax.swing.JLabel();
            labelHasil = new javax.swing.JLabel();
            textFieldSuhu = new javax.swing.JTextField();
            comboBoxKonversiDari = new javax.swing.JComboBox<>();
            jLabel4 = new javax.swing.JLabel();
            jLabel5 = new javax.swing.JLabel();
            radioButtonFahrenheit = new javax.swing.JRadioButton();
            radioButtonReamur = new javax.swing.JRadioButton();
            radioButtonKelvin = new javax.swing.JRadioButton();
            tombolKonversi = new javax.swing.JButton();
            radioButtonCelcius = new javax.swing.JRadioButton();
            jLabel6 = new javax.swing.JLabel();

            setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
            getContentPane().setLayout(new java.awt.GridBagLayout());

            jLabel1.setBackground(new java.awt.Color(153, 255, 0));
            jLabel1.setFont(new java.awt.Font("Tahoma", 1, 24)); // NOI18N
            jLabel1.setForeground(new java.awt.Color(0, 204, 204));
            jLabel1.setText("Aplikasi Konversi Suhu");

            jLabel2.setText("Masukan Suhu                :");

            textFieldSuhu.addActionListener(new java.awt.event.ActionListener() {
                public void actionPerformed(java.awt.event.ActionEvent evt) {
                    textFieldSuhuActionPerformed(evt);
                }
            });

            comboBoxKonversiDari.setModel(new javax.swing.DefaultComboBoxModel<>(new String[] { "Celcius", "Fahrenheit", "Kelvin", "Reamur" }));

            jLabel4.setText("Konversi Dari                   :");

            jLabel5.setText("Konversi ke                      :");

            buttonGroup1.add(radioButtonFahrenheit);
            radioButtonFahrenheit.setText("Fahrenheit");

            buttonGroup1.add(radioButtonReamur);
            radioButtonReamur.setText("Reamur");

            buttonGroup1.add(radioButtonKelvin);
            radioButtonKelvin.setText("Kelvin");
            radioButtonKelvin.addActionListener(new java.awt.event.ActionListener() {
                public void actionPerformed(java.awt.event.ActionEvent evt) {
                    radioButtonKelvinActionPerformed(evt);
                }
            });

            tombolKonversi.setText("Konversi");
            tombolKonversi.addActionListener(new java.awt.event.ActionListener() {
                public void actionPerformed(java.awt.event.ActionEvent evt) {
                    tombolKonversiActionPerformed(evt);
                }
            });

            buttonGroup1.add(radioButtonCelcius);
            radioButtonCelcius.setText("Celcius");

            jLabel6.setText("Hasil                                 :");

            javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
            jPanel1.setLayout(jPanel1Layout);
            jPanel1Layout.setHorizontalGroup(
                jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                .addGroup(jPanel1Layout.createSequentialGroup()
                    .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(183, 183, 183)
                            .addComponent(jLabel1))
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(36, 36, 36)
                            .addComponent(jLabel2)
                            .addGap(55, 55, 55)
                            .addComponent(textFieldSuhu, javax.swing.GroupLayout.PREFERRED_SIZE, 179, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addGap(46, 46, 46)
                            .addComponent(tombolKonversi))
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(36, 36, 36)
                            .addComponent(jLabel4)
                            .addGap(55, 55, 55)
                            .addComponent(comboBoxKonversiDari, javax.swing.GroupLayout.PREFERRED_SIZE, 179, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(36, 36, 36)
                            .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                .addComponent(jLabel5)
                                .addComponent(jLabel6))
                            .addGap(55, 55, 55)
                            .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                .addGroup(jPanel1Layout.createSequentialGroup()
                                    .addComponent(radioButtonFahrenheit)
                                    .addGap(12, 12, 12)
                                    .addComponent(radioButtonReamur)
                                    .addGap(6, 6, 6)
                                    .addComponent(radioButtonKelvin)
                                    .addGap(49, 49, 49)
                                    .addComponent(radioButtonCelcius))
                                .addComponent(labelHasil))))
                    .addGap(60, 60, 60))
            );
            jPanel1Layout.setVerticalGroup(
                jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                .addGroup(jPanel1Layout.createSequentialGroup()
                    .addGap(54, 54, 54)
                    .addComponent(jLabel1)
                    .addGap(55, 55, 55)
                    .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(5, 5, 5)
                            .addComponent(jLabel2))
                        .addComponent(textFieldSuhu, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addComponent(tombolKonversi))
                    .addGap(6, 6, 6)
                    .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(5, 5, 5)
                            .addComponent(jLabel4))
                        .addComponent(comboBoxKonversiDari, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addGap(12, 12, 12)
                    .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                        .addGroup(jPanel1Layout.createSequentialGroup()
                            .addGap(2, 2, 2)
                            .addComponent(jLabel5))
                        .addComponent(radioButtonFahrenheit)
                        .addComponent(radioButtonReamur)
                        .addComponent(radioButtonKelvin)
                        .addComponent(radioButtonCelcius))
                    .addGap(36, 36, 36)
                    .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                        .addComponent(labelHasil)
                        .addComponent(jLabel6)))
            );

            gridBagConstraints = new java.awt.GridBagConstraints();
            gridBagConstraints.gridx = 0;
            gridBagConstraints.gridy = 0;
            gridBagConstraints.ipadx = 60;
            gridBagConstraints.ipady = 108;
            gridBagConstraints.anchor = java.awt.GridBagConstraints.NORTHWEST;
            gridBagConstraints.insets = new java.awt.Insets(6, 6, 6, 6);
            getContentPane().add(jPanel1, gridBagConstraints);

            pack();
        }// </editor-fold>                        

        private void tombolKonversiActionPerformed(java.awt.event.ActionEvent evt) {                                               
            // TODO add your handling code here:
        }                                              

        private void radioButtonKelvinActionPerformed(java.awt.event.ActionEvent evt) {                                                  
            // TODO add your handling code here:
        }                                                 

        private void textFieldSuhuActionPerformed(java.awt.event.ActionEvent evt) {                                              
            // TODO add your handling code here:
        }                                             

        /**
        * @param args the command line arguments
        */
        public static void main(String args[]) {
            /* Set the Nimbus look and feel */
            //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
            /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
            * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
            */
            try {
                for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                    if ("Nimbus".equals(info.getName())) {
                        javax.swing.UIManager.setLookAndFeel(info.getClassName());
                        break;
                    }
                }
            } catch (ClassNotFoundException ex) {
                java.util.logging.Logger.getLogger(Suhu.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
            } catch (InstantiationException ex) {
                java.util.logging.Logger.getLogger(Suhu.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
            } catch (IllegalAccessException ex) {
                java.util.logging.Logger.getLogger(Suhu.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
            } catch (javax.swing.UnsupportedLookAndFeelException ex) {
                java.util.logging.Logger.getLogger(Suhu.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
            }
            //</editor-fold>
            //</editor-fold>

            /* Create and display the form */
            java.awt.EventQueue.invokeLater(new Runnable() {
                public void run() {
                    new Suhu().setVisible(true);
                }
            });
        }

        // Variables declaration - do not modify                     
        private javax.swing.ButtonGroup buttonGroup1;
        private javax.swing.JComboBox<String> comboBoxKonversiDari;
        private javax.swing.JLabel jLabel1;
        private javax.swing.JLabel jLabel2;
        private javax.swing.JLabel jLabel4;
        private javax.swing.JLabel jLabel5;
        private javax.swing.JLabel jLabel6;
        private javax.swing.JPanel jPanel1;
        private javax.swing.JLabel labelHasil;
        private javax.swing.JRadioButton radioButtonCelcius;
        private javax.swing.JRadioButton radioButtonFahrenheit;
        private javax.swing.JRadioButton radioButtonKelvin;
        private javax.swing.JRadioButton radioButtonReamur;
        private javax.swing.JTextField textFieldSuhu;
        private javax.swing.JButton tombolKonversi;
        // End of variables declaration                   

        
    }

## Authors

- [@AhmadShawity](https://github.com/Kryuuu)

