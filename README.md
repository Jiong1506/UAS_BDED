# UAS_BDED
Belajari Di Era Digital
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UAS Digital Literacy Quiz</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f0ff;
            color: #333;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            background-color: #fff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            text-align: center;
            color: #6a5acd;
            margin-bottom: 30px;
            font-size: 2.2em;
        }
        
        .quiz-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            padding: 10px;
            background-color: #e6e6fa;
            border-radius: 8px;
            font-weight: bold;
        }
        
        .question {
            background-color: #f8f4ff;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 10px;
            border-left: 5px solid #9370db;
        }
        
        .question-number {
            font-weight: bold;
            color: #6a5acd;
            margin-bottom: 10px;
            font-size: 1.1em;
        }
        
        .question-text {
            margin-bottom: 15px;
            font-size: 1.05em;
        }
        
        .options {
            margin-left: 20px;
        }
        
        .option {
            margin-bottom: 10px;
            padding: 8px;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        
        .option:hover {
            background-color: #e6e6fa;
        }
        
        .option input {
            margin-right: 10px;
        }
        
        .correct {
            background-color: #e6ffe6;
            border-left: 3px solid #4caf50;
        }
        
        .incorrect {
            background-color: #ffebee;
            border-left: 3px solid #f44336;
        }
        
        .highlight {
            font-weight: bold;
            color: #6a5acd;
        }
        
        button {
            display: block;
            margin: 30px auto;
            padding: 12px 25px;
            background-color: #9370db;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1.1em;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: #7b68ee;
        }
        
        .results {
            display: none;
            margin-top: 30px;
            padding: 20px;
            background-color: #f0e6ff;
            border-radius: 10px;
            text-align: center;
        }
        
        .score {
            font-size: 1.5em;
            font-weight: bold;
            color: #6a5acd;
            margin-bottom: 20px;
        }
        
        .answers {
            text-align: left;
            margin-top: 20px;
        }
        
        .answer-item {
            margin-bottom: 15px;
            padding: 10px;
            background-color: #fff;
            border-radius: 5px;
        }
        
        .progress-bar {
            height: 10px;
            background-color: #e6e6fa;
            border-radius: 5px;
            margin-bottom: 20px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background-color: #9370db;
            width: 0%;
            transition: width 0.5s;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 1.8em;
            }
            
            .question {
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Digital Literacy Quiz</h1>
        <div class="quiz-info">
            <div>Total Questions: <span id="total-questions">50</span></div>
            <div>Answered: <span id="answered">0</span></div>
        </div>
        <div class="progress-bar">
            <div class="progress" id="progress"></div>
        </div>
        <div id="quiz-container"></div>
        <button id="submit-btn">Submit Quiz</button>
        <div class="results" id="results">
            <div class="score">Your Score: <span id="score">0</span>/50</div>
            <div class="answers" id="answers"></div>
            <button id="retry-btn">Try Again</button>
        </div>
    </div>

    <script>
        // Data soal dari file BIED.txt
        const allQuestions = [
            {
                question: "1) Di era digital, keunggulan kompetitif hanya dimiliki oleh perusahaan yang dapat memanfaatkan ....",
                options: [
                    "A. sumberdaya alam",
                    "B. sumberdaya manusia",
                    "C. sains dan teknologi",
                    "D. pengetahuan"
                ],
                correctAnswer: 2
            },
            {
                question: "2) Dampak kebutuhan akan pekerja-pengetahuan (knowledge workers) yang meningkat di dunia industri akan memicu perguruan tinggi menghasilkan lulusan dalam jumlah yang ....",
                options: [
                    "A. lebih sedikit",
                    "B. sama saja",
                    "C. lebih besar",
                    "D. sesuai kebutuhan"
                ],
                correctAnswer: 2
            },
            {
                question: "3) Ciri-ciri SDM berbasis pengetahuan adalah sebagai berikut kecuali ....",
                options: [
                    "A. bekerja di perusahaan besar",
                    "B. mampu menciptakan pekerjaan sendiri",
                    "C. sifat pekerjaannya cenderung berubah",
                    "D. bergantung pada jaringan sosial"
                ],
                correctAnswer: 0
            },
            {
                question: "4) Dalam masyarakat pengetahuan (knowledge society), membuat video singkat YouTube untuk menyampaikan gagasan untuk menjangkau audiens merupakan keterampilan ....",
                options: [
                    "A. digital",
                    "B. manual",
                    "C. komunikasi",
                    "D. belajar mandiri"
                ],
                correctAnswer: 0
            },
            {
                question: "5) Di era pembelajaran digital, beberapa nilai esensial/inti (core values) dari perguruan tinggi perlu ....",
                options: [
                    "A. berubah",
                    "B. dipertahankan",
                    "C. di-eliminasi",
                    "D. digunakan bila perlu"
                ],
                correctAnswer: 0
            },
            {
                question: "6) Salah satu respon perguruan tinggi terhadap kebutuhan akan lulusan pendidikan tinggi yang semakin meningkat adalah dengan menciptakan kelas-kelas ....",
                options: [
                    "A. kecil",
                    "B. sedang",
                    "C. besar",
                    "D. sesuai kebutuhan"
                ],
                correctAnswer: 0
            },
            {
                question: "7) Strategi perguruan tinggi dalam mengelola kelas besar pada umumnya memberikan dampak yang cenderung ....",
                options: [
                    "A. positif",
                    "B. negatif",
                    "C. netral",
                    "D. tidak diketahui"
                ],
                correctAnswer: 0
            },
            {
                question: "8) Sifat keberadaan teknologi pembelajaran di era digital terhadap kemunculan kelas besar adalah ....",
                options: [
                    "A. mempercepat",
                    "B. memperlambat",
                    "C. menganggu",
                    "D. tidak diketahui"
                ],
                correctAnswer: 0
            },
            {
                question: "9) Di era pembelajaran digital, perguruan tinggi perlu fokus pada metode pembelajaran yang membantu keberhasilan mahasiswa yang mengarah pada pendekatan ...",
                options: [
                    "A. belajar dengan pendampingan mentor",
                    "B. belajar berkelompok",
                    "C. belajar sendiri",
                    "D. individualisasi belajar"
                ],
                correctAnswer: 3
            },
            {
                question: "10) Salah satu alasan untuk kembali kuliah di era pembelajaran digital meskipun sudah bekerja pada umumnya adalah untuk ....",
                options: [
                    "A. mendukung karir",
                    "B. mencari pengalaman belajar baru",
                    "C. memutakhirkan wawasan",
                    "D. mengukur kemampuan belajar di era digital"
                ],
                correctAnswer: 0
            },
            {
                question: "11) Elemen-elemen ini adalah komponen dari konsep literasi digital dalam arti luas kecuali ....",
                options: [
                    "A. literasi media",
                    "B. keterampilan belajar mandiri",
                    "C. literasi informasi",
                    "D. komunikasi dan kolaborasi"
                ],
                correctAnswer: 1
            },
            {
                question: "12) Literasi digital adalah seperangkat pengetahuan yang diperoleh dari praktik-praktik situasional di lingkungan yang penuh dengan perubahan-perubahan teknologi dan pengetahuan tersebut bersifat ....",
                options: [
                    "A. personal",
                    "B. akademis",
                    "C. komersial",
                    "D. profesional"
                ],
                correctAnswer: 0
            },
            {
                question: "13) Literasi digital tidak hanya tentang penguasaan kemahiran teknis namun juga tentang pemahaman aspek-aspek di seputar penggunaan teknologi seperti ....",
                options: [
                    "A. norma-norma penggunaan teknologi digital",
                    "B. dokumentasi digital",
                    "C. SOP (standard operation procedure)",
                    "D. otomatisasi prosedur"
                ],
                correctAnswer: 0
            },
            {
                question: "14) Salah satu contoh keterampilan digital adalah ....",
                options: [
                    "A. mengetahui bahwa setting Facebook selalu dimutakhirkan",
                    "B. cara men-tweet di Twitter",
                    "C. menyadari pentingnya mengubah password secara periodik",
                    "D. mengetahui risiko menggunakan password yang mudah ditebak"
                ],
                correctAnswer: 3
            },
            {
                question: "15) Dalam proses dan perkembangan pembelajaran di era digital mahasiswa sebagai agen perubahan dapat mengambil peran sebagai ....",
                options: [
                    "A. peneliti",
                    "B. pengguna",
                    "C. pedukung",
                    "D. pengendali"
                ],
                correctAnswer: 0
            },
            {
                question: "16) Munculnya pembelajaran digital pada umumnya disebabkan terutama oleh perkembangan ....",
                options: [
                    "A. ilmu pengetahuan",
                    "B. proses bisnis perguruan tinggi",
                    "C. teknologi informasi dan komunikasi",
                    "D. kebudayaan manusia"
                ],
                correctAnswer: 2
            },
            {
                question: "17) Pembelajaran digital sangat relevan dengan kondisi pendidikan tinggi yang saat ini antara lain ....",
                options: [
                    "A. biaya pendidikan yang semakin tinggi",
                    "B. masih menjadi impian lulusan SLTA",
                    "C. banyak yang tutup",
                    "D. kesulitan mendapatkan mahasiswa"
                ],
                correctAnswer: 0
            },
            {
                question: "18) Munculnya massive open online courses (MOOCs) antara lain didorong oleh berkembangnya infrastruktur digital dan telah berkembang menjadi ....",
                options: [
                    "A. full course",
                    "B. micro course",
                    "C. degree program",
                    "D. certificate program"
                ],
                correctAnswer: 2
            },
            {
                question: "19) Berkembangnya pembelajaran online alternatif telah melahirkan berbagai inovasi khususnya berkaitan dengan kredensial alternatif seperti ....",
                options: [
                    "A. certificate",
                    "B. nano degree",
                    "C. diploma",
                    "D. degree"
                ],
                correctAnswer: 0
            },
            {
                question: "20) Kredensial alternatif memiliki berbagai keunggulan untuk memenuhi dunia kerja yang cepat berubah dikarenakan ....",
                options: [
                    "A. flexible",
                    "B. universal",
                    "C. global",
                    "D. special"
                ],
                correctAnswer: 0
            },
            {
                question: "21) Pencarian sumber pembelajaran yang bertujuan untuk memperluas hasil pencarian menggunakan metode ....",
                options: [
                    "A. Pemotongan",
                    "B. Pembatasan",
                    "C. Pencarian lanjutan",
                    "D. Operator Boolean"
                ],
                correctAnswer: 2
            },
            {
                question: "22) Penggunaan Operator Boolean dengan operator OR akan menghasilkan data pencarian yang ....",
                options: [
                    "A. Lebih luas",
                    "B. Lebih sempit",
                    "C. Lebih akurat",
                    "D. Lebih berkualitas"
                ],
                correctAnswer: 0
            },
            {
                question: "23) Pencarian dengan menggunakan mesin pencari dapat menghasilkan data yang sangat luas, umum dan tidak spesifik. Untuk menghasilkan hasil pencarian data yang lebih spesifik dapat menggunakan ....",
                options: [
                    "A. AND",
                    "B. OR",
                    "C. FRASA",
                    "D. NOT"
                ],
                correctAnswer: 0
            },
            {
                question: "24) Penggunaan operator Boolean NOT untuk pencarian database sumber pembelajaran dipergunakan untuk ....",
                options: [
                    "A. Memfokuskan",
                    "B. Mengecualikan",
                    "C. Memperluas",
                    "D. Mempersempit"
                ],
                correctAnswer: 1
            },
            {
                question: "25) Pada pencarian sumber pembelajaran dengan menggunakan operator Boolean perlu diperhatikan urutan operator tersebut, mesin pencari pada umumnya menggunakan urutan sebagai berikut ....",
                options: [
                    "A. OR, AND, NOT",
                    "B. AND, OR, NOT",
                    "C. NOT, AND, OR",
                    "D. AND, NOT, OR"
                ],
                correctAnswer: 1
            },
            {
                question: "26) Membaca merupakan aktivitas utama di perguruan tinggi. Sebelum Anda membaca materi pelajaran sebaiknya Anda memulainya dengan mengetahui ....",
                options: [
                    "A. tujuannya",
                    "B. penulisnya",
                    "C. penerbitnya",
                    "D. reviewnya"
                ],
                correctAnswer: 0
            },
            {
                question: "27) Memilih atau menyeleksi bacaan atau materi pembelajaran dapat menentukan keberhasilan Anda membaca secara efektif. Menyeleksi bacaan dapat dilakukan melalui antara lain kecuali ....",
                options: [
                    "A. mengidentifikasi kata-kata kunci",
                    "B. mengetahui tujuan membaca",
                    "C. menelusuri daftar isi dan indeks buku untuk halaman yang relevan",
                    "D. membuat rangkuman setiap materi."
                ],
                correctAnswer: 3
            },
            {
                question: "28) Pada perkuliahan atau tutorial sering dilakukan dengan presentasi oral maupun video. Mencatat materi selama perkuliahan/tutorial sangat penting, dikarenakan ....",
                options: [
                    "A. membantu Anda mengidentifikasi topik utama",
                    "B. mengetahui materi kuliah",
                    "C. mengetahui materi yang diujikan",
                    "D. meninjau materi kuliah/tutorial dengan materi pada buku."
                ],
                correctAnswer: 0
            },
            {
                question: "29) Catatan perkuliahan/tutorial sangat penting untuk mahasiswa dikarenakan catatan berisikan, kecuali ....",
                options: [
                    "A. ringkasan",
                    "B. informasi utama",
                    "C. informasi yang tidak ada di buku atau bacaan",
                    "D. informasi kinestesis"
                ],
                correctAnswer: 3
            },
            {
                question: "30) Metode membaca secara efektif pada umumnya menggunakan metode SOW3R. Huruf O pada metode SAW3R berfungsi untuk ....",
                options: [
                    "A. memfokuskan pada materi yang ingin diketahui",
                    "B. menyiapkan catatan untuk lebih konsentrasi",
                    "C. membuat overview materi",
                    "D. mengingat kembali materi."
                ],
                correctAnswer: 2
            },
            {
                question: "31) Tulisan reflektif memungkinkan berisikan berbagai unsur antara lain tulisan yang bersifat ....",
                options: [
                    "A. Argumentatif",
                    "B. Deskriptif",
                    "C. Konklusif",
                    "D. Hipotetis"
                ],
                correctAnswer: 0
            },
            {
                question: "32) Mencatat perkuliahan atau video presentasi menggunakan komputer akan lebih mudah, hal ini disebabkan oleh beberapa faktor kecuali ....",
                options: [
                    "A. Lebih cepat",
                    "B. Mudah untuk diubah",
                    "C. Fleksibel",
                    "D. Mudah disimpan"
                ],
                correctAnswer: 0
            },
            {
                question: "33) Mencatat atau note taking merupakan kegiatan perkuliahan yang sangat penting, karena mencatat ....",
                options: [
                    "A. membantu konsentrasi",
                    "B. membantu mengingat",
                    "C. membantu merangkum",
                    "D. membantu meringkas"
                ],
                correctAnswer: 3
            },
            {
                question: "34) Teknologi digital telah mempengaruhi di pembelajaran pendidikan tinggi yang memungkinkan semakin membuka akses dan perannya ke depan, salah satu pembelajaran digital alternatif yang muncul saat ini adalah ....",
                options: [
                    "A. TED Talk",
                    "B. MOOCs",
                    "C. Kredensial Alternatif",
                    "D. Digital Badges"
                ],
                correctAnswer: 1
            },
            {
                question: "35) Catatan yang berisikan interaksi dan komunikasi Anda pada saat mengikuti pembelajaran dengan teman Anda disebut sebagai ....",
                options: [
                    "A. Jurnal",
                    "B. Buku harian pembelajaran",
                    "C. Buku log",
                    "D. Catatan reflektif"
                ],
                correctAnswer: 3
            },
            {
                question: "36) Jenis teknologi yang tercepat untuk mencapai angka seratus juta penggunaan adalah ....",
                options: [
                    "A. telepon",
                    "B. ponsel",
                    "C. Facebook",
                    "D. Internet (WWW)"
                ],
                correctAnswer: 1
            },
            {
                question: "37) Media dapat bertindak sebagai batu loncatan untuk imaginasi kita dan sumber fantasi sehingga media dikatakan mempunyai fungsi sebagai ....",
                options: [
                    "A. hiburan",
                    "B. informasi",
                    "C. forum",
                    "D. pengawas bagi pemerintah"
                ],
                correctAnswer: 3
            },
            {
                question: "38) Salah satu keunggulan televisi selain membuat cerita lebih hidup adalah sebagai media yang mampu menyajikan informasi dalam waktu yang cepat, hal ini berarti cerita yang dibahas di televisi ....",
                options: [
                    "A. komprehensif",
                    "B. parsial",
                    "C. utuh",
                    "D. kurang mendalam"
                ],
                correctAnswer: 2
            },
            {
                question: "39) Teknologi yang terkait dengan media yang dianggap mengantar pergerakan budaya besar-besaran seperti Renaisans Eropa adalah teknologi ....",
                options: [
                    "A. radio",
                    "B. telepon",
                    "C. telegraf",
                    "D. mesin cetak"
                ],
                correctAnswer: 3
            },
            {
                question: "40) Terjadinya tingkat meledaknya konsumerisme besar-besaran seiring dengan meledaknya popularitas media ....",
                options: [
                    "A. mesin cetak",
                    "B. telepon",
                    "C. radio",
                    "D. telegraf"
                ],
                correctAnswer: 0
            },
            {
                question: "41) Yang manakah di antara istilah berikut ini digunakan untuk mengategorikan tindakan komunikasi satu-ke-banyak dan banyak-ke-banyak ....",
                options: [
                    "A. komunikasi massa",
                    "B. komunikasi organisasional",
                    "C. komunikasi interpersonal",
                    "D. komunikasi antar budaya"
                ],
                correctAnswer: 0
            },
            {
                question: "42) Aspen mendefinisikan literasi media sebagai 'kemampuan untuk mengakses, menganalisa, mengevaluasi dan menciptakan media dalam berbagai bentuk'. Definisi ini pertama kali diterbitkan tahun ....",
                options: [
                    "A. 1982",
                    "B. 1992",
                    "C. 2012",
                    "D. 2002"
                ],
                correctAnswer: 1
            },
            {
                question: "43) Satu pernyataan yang benar di bawah ini tentang definisi literasi media yang diperluas untuk abad ke-21?",
                options: [
                    "A. literasi media menunjukkan keterampilan penting terutama sekali untuk ekspresi diri.",
                    "B. literasi media terutama berkenaan dengan mengevaluasi sumber berita, bukan beritanya itu sendiri.",
                    "C. literasi media membangun pemahaman tentang peran media dalam masyarakat.",
                    "D. literasi media terutama berkenaan dengan mengetahui sumber berita."
                ],
                correctAnswer: 0
            },
            {
                question: "44) Salah satu pernyataan berikut sebagai indikasi bahwa siaran pers tersebut kurang kredibel adalah ....",
                options: [
                    "A. siaran pers harus menyertakan tanggal dan penulis lokasi di awal paragraf awal",
                    "B. siaran pers mirip dengan promosi produk atau sales pitch",
                    "C. siaran pers harus memberikan informasi kunci, memungkinkan seorang wartawan untuk menggunakannya untuk menghasilkan artikel atau laporan",
                    "D. sebuah siaran pers biasanya ditulis oleh seseorang yang bekerja di bagian Humas"
                ],
                correctAnswer: 1
            },
            {
                question: "45) Siaran pers defensif terkadang diperlukan hanya untuk menangani informasi yang ....",
                options: [
                    "A. positif",
                    "B. negatif",
                    "C. kritis",
                    "D. netral"
                ],
                correctAnswer: 1
            },
            {
                question: "46) Berikut ini yang merupakan perbedaan antara media lama dengan media baru adalah ....",
                options: [
                    "A. media baru memungkinkan pemirsanya untuk berpartisipasi aktif",
                    "B. media lama memuat berita lama",
                    "C. media baru lebih dapat dipercaya",
                    "D. media lama menyuguhkan berita faktual"
                ],
                correctAnswer: 0
            },
            {
                question: "47) Salah satu alasan mengapa media cenderung memberitakan kekerasan adalah ....",
                options: [
                    "A. tidak ada bahan berita lain",
                    "B. kasus kekerasan biasanya tidak memiliki analisis lanjut, yang penting diberitakan begitu saja asal pembaca tertarik",
                    "C. berita kekerasan paling ditunggu oleh masyarakat",
                    "D. kekerasan merupakan hal yang paling sering terjadi di masyarakat"
                ],
                correctAnswer: 1
            },
            {
                question: "48) Salah satu jenis pembaca dalam menyikapi sebuah pemberitaan media adalah oppositional reader, yaitu ....",
                options: [
                    "A. masyarakat yang begitu mudah hanyut dalam pemberitaan media",
                    "B. pembaca yang tidak kritis dan cenderung mengikuti apa yang diberitakan oleh media",
                    "C. pembaca yang selalu menolak segala pemberitaan media terutama nilai-nilai yang ditransmisikan oleh media",
                    "D. pembaca yang ideal dan patut dicontoh oleh masyarakat"
                ],
                correctAnswer: 2
            },
            {
                question: "49) Tokoh yang menyatakan bahwa semua revolusi komunikasi telah menciptakan pergolakan dan telah mengubah standar literasi dan komunikasi adalah ....",
                options: [
                    "A. Henry Jenkins",
                    "B. Timpane",
                    "C. Baron",
                    "D. Stanley McChrystal"
                ],
                correctAnswer: 3
            },
            {
                question: "50) Istilah yang digunakan untuk menggambarkan cara konsumen media di negara Eropa Timur dalam menyaring informasi setelah Perang Dunia I adalah ....",
                options: [
                    "A. cyberbalkanization",
                    "B. delayed feedback",
                    "C. onion article",
                    "D. convergence"
                ],
                correctAnswer: 0
            },
            {
                question: "51) Penerima informasi dalam komunikasi massa bersifat heterogen. Ciri-ciri masyarakat heterogen tersebut adalah di bawah ini, kecuali ....",
                options: [
                    "A. tidak membedakan suku, ras, agama, maupun strata sosial yang berbeda",
                    "B. memiliki beragam karakter psikologi, usia, jenis kelamin, tempat tinggal, serta adat budaya",
                    "C. memiliki strata sosial yang berbeda-beda",
                    "D. berasal dari latar belakang pendidikan yang sama"
                ],
                correctAnswer: 3
            },
            {
                question: "52) Dalam proses komunikasi massa pesan-pesan yang disampaikan oleh komunikator ditujukan kepada khalayak luas atau semua orang bukan hanya sekelompok orang. Dengan demikian, dapat diartikan bahwa pesan yang disampaikan tersebut bersifat ....",
                options: [
                    "A. khusus",
                    "B. umum",
                    "C. luas",
                    "D. tersebar"
                ],
                correctAnswer: 1
            },
            {
                question: "53) Copycats merupakan salah satu dampak dari berita tentang kekerasan. Maksud dari copycats tersebut yaitu ....",
                options: [
                    "A. peniruan kekerasan oleh pembaca sebagai hasil apa yang dia lihat dalam pemberitaan media",
                    "B. masyarakat akan merasa terbiasa dengan adanya kekerasan akibat media terlalu sering memberitakan kekerasan",
                    "C. perasaan khawatir pembaca bila terjadi kekerasan pada dirinya setelah melihat adegan kekerasan",
                    "D. perasaan takut pembaca jika terjadi kejahatan kepada dirinya"
                ],
                correctAnswer: 0
            },
            {
                question: "54) Salah satu dampak berita kekerasan yang dimuat oleh media adalah masyarakat akan merasa terbiasa dengan adanya kekerasan akibat media terlalu sering memberitakan kekerasan. Hal ini merupakan dampak berita kekerasan, yaitu ....",
                options: [
                    "A. copycats",
                    "B. desensitization effects",
                    "C. moral panic",
                    "D. fear of crime"
                ],
                correctAnswer: 1
            },
            {
                question: "55) Komunikasi massa merupakan salah satu komunikasi yang memiliki perbedaan signifikan dengan bentuk komunikasi yang lain. Hal ini merupakan pengertian komunikasi massa yang dikemukakan oleh ....",
                options: [
                    "A. Effendy",
                    "B. Elvinaro",
                    "C. William R. Rivers",
                    "D. Hafied Cangara"
                ],
                correctAnswer: 0
            },
            {
                question: "56) Aplikasi media sosial berikut ini yang memfasilitasi masyarakat untuk berkomunikasi melalui pesan singkat secara gratis adalah ....",
                options: [
                    "A. Short Message Service (SMS)",
                    "B. Multimedia Messaging Services (MMS)",
                    "C. WhatsApp",
                    "D. jurnal elektronik"
                ],
                correctAnswer: 2
            },
            {
                question: "57) Aplikasi media sosial yang berisi konten berupa video adalah ....",
                options: [
                    "A. Facebook",
                    "B. Youtube",
                    "C. Twitter",
                    "D. Instagram"
                ],
                correctAnswer: 1
            },
            {
                question: "58) Dampak positif yang muncul akibat berkembangnya media sosial, yaitu ....",
                options: [
                    "A. waktu untuk menyampaikan informasi menjadi lebih cepat",
                    "B. biaya yang digunakan relatif lebih mahal",
                    "C. masyarakat dapat membedakan berita yang fiktif dengan realita",
                    "D. masyarakat menjadi lebih sering membaca"
                ],
                correctAnswer: 0
            },
            {
                question: "59) Selain memberikan dampak positif, media sosial juga memiliki berbagai dampak negatif. Salah satunya adalah ....",
                options: [
                    "A. informasi menyebar terlalu cepat",
                    "B. berkurangnya interaksi interpersonal atau tatap muka",
                    "C. privasi masyarakat menjadi lebih terjamin",
                    "D. terjadi perbedaan pendapat di antara masyarakat pengguna media sosial"
                ],
                correctAnswer: 1
            },
            {
                question: "60) Desy, seorang guru TK, ingin berbagi tips tentang bagaimana mengenalkan konsep jumlah kepada para guru yang ada di sekolah lain melalui tayangan video. Agar penyampaian tips ini dapat menyebar secara cepat dan tidak menggunakan banyak biaya, sebaiknya Ibu Desy menggunakan aplikasi media sosial ....",
                options: [
                    "A. Youtube",
                    "B. koran elektronik",
                    "C. Multimedia Messaging Services (MMS)",
                    "D. Short Message Service (SMS)"
                ],
                correctAnswer: 0
            },
            {
                question: "61) Aspek penting yang perlu diperhatikan ketika menggunakan media sosial adalah ....",
                options: [
                    "A. lokasi penggunaan media sosial",
                    "B. kondisi fisik dan psikis ketika menggunakan aplikasi media sosial",
                    "C. strata sosial pengguna media sosial yang berbeda-beda",
                    "D. kerahasiaan informasi pribadi"
                ],
                correctAnswer: 3
            },
            {
                question: "62) Salah satu contoh kolaborasi positif yang dapat dilakukan melalui media sosial adalah ....",
                options: [
                    "A. bekerja sama pada saat ujian",
                    "B. mempromosikan budaya setempat",
                    "C. janjian menghadiri acara tertentu",
                    "D. mengumpulkan massa untuk berunjuk rasa"
                ],
                correctAnswer: 1
            },
            {
                question: "63) Salah satu manfaat media sosial adalah mempertemukan orang dengan ketertarikan yang sama. Maksud dari pernyataan ini dapat dilihat dari contoh nyata dalam kehidupan sehari-hari, yaitu ....",
                options: [
                    "A. ayah menginformasikan jadwalnya kepada anggota keluarga yang lain melalui aplikasi pesan singkat pada handphone",
                    "B. seorang guru membuat grup komunikasi dengan siswanya",
                    "C. seorang mahasiswa bergabung dalam komunitas pecinta buku",
                    "D. ketua kelas mengumumkan petugas piket setiap minggu"
                ],
                correctAnswer: 2
            },
            {
                question: "64) Setiap platform sosial media menawarkan berbagai tools atau fitur yang memungkinkan bagi sebuah bisnis untuk menyampaikan konten tertentu pada sasaran mereka. Hal ini merupakan salah satu manfaat media, yaitu ....",
                options: [
                    "A. menjangkau target pasar",
                    "B. mempertemukan orang dengan ketertarikan yang sama",
                    "C. peningkatan sirkulasi informasi",
                    "D. memperluas koneksi ke seluruh dunia"
                ],
                correctAnswer: 0
            },
            {
                question: "65) Berikut ini merupakan manfaat media sosial, kecuali ....",
                options: [
                    "A. mempertemukan orang dengan ketertarikan yang sama",
                    "B. berbagi informasi secara real-time",
                    "C. menjangkau target pasar",
                    "D. penurunan sirkulasi informasi"
                ],
                correctAnswer: 3
            },
            {
                question: "66) Pengguna internet yang biasanya hanya ingin menelusuri informasi disebut digital ....",
                options: [
                    "A. citizen",
                    "B. journalism",
                    "C. people",
                    "D. era"
                ],
                correctAnswer: 0
            },
            {
                question: "67) Di bawah ini yang merupakan salah satu perbedaan antara digital citizen dengan digital journalism adalah digital citizen ....",
                options: [
                    "A. menyebarkan informasi",
                    "B. menelusuri informasi",
                    "C. memperluas informasi",
                    "D. membuat informasi"
                ],
                correctAnswer: 1
            },
            {
                question: "68) Pengguna internet harus menunjukkan rasa hormat pada orang lain: bersikap sopan, dan melindungi hak semua orang termasuk hak mereka sendiri, merupakan penjelasan salah satu pilar digital citizenship, yaitu ....",
                options: [
                    "A. digital civility",
                    "B. information literacy",
                    "C. early literacy",
                    "D. digital literacy"
                ],
                correctAnswer: 0
            },
            {
                question: "69) Information literacy merupakan salah satu pilar digital citizenship. Pengertian information literacy tersebut adalah ....",
                options: [
                    "A. kemampuan untuk menghasilkan informasi",
                    "B. pengguna internet harus menunjukkan rasa hormat pada orang lain, bersikap sopan, dan melindungi hak semua orang",
                    "C. kemampuan untuk mengidentifikasi, menemukan, mengevaluasi, dan menggunakan informasi secara efektif dari internet untuk menyelesaikan suatu tugas, menjawab pertanyaan, atau meneliti suatu topik",
                    "D. pengguna internet sebaiknya saling bertukar informasi"
                ],
                correctAnswer: 2
            },
            {
                question: "70) JD. Lasica mengategorikan media citizen journalism ke dalam 5 tipe, yaitu ....",
                options: [
                    "A. audience participation",
                    "B. media participation",
                    "C. situs hobby masyarakat",
                    "D. laporan kegiatan sehari-hari"
                ],
                correctAnswer: 0
            },
            {
                question: "71) Dunia maya (cyberspace) merupakan realita yang terselubung secara global, didukung komputer, berakses komputer, multidimensi, artifisial, atau virtual. Pernyataan ini dikemukakan oleh ....",
                options: [
                    "A. Cision",
                    "B. Lasica",
                    "C. Gibson",
                    "D. Shayne Bowman"
                ],
                correctAnswer: 2
            },
            {
                question: "72) Kolaborasi antara jurnalis profesional dengan nonjurnalis yang memiliki kemampuan dalam materi yang dibahas merupakan salah satu klasifikasi bentuk citizen journalism yang dikemukakan oleh ....",
                options: [
                    "A. Shayne Bowman",
                    "B. Gibson",
                    "C. Chris Willis",
                    "D. Steve Outing"
                ],
                correctAnswer: 0
            },
            {
                question: "73) Citizen journalism dapat memanfaatkan media-media yang ada baik mainstream media ataupun social media. Apabila jurnalis warga ingin berbagi informasi berupa tulisan, baik tulisan ilmiah maupun tulisan populer, warga tersebut dapat menggunakan situs social media ....",
                options: [
                    "A. blog (wordpress, blogspot)",
                    "B. twitpic",
                    "C. friendster",
                    "D. flickr"
                ],
                correctAnswer: 0
            },
            {
                question: "74) Situs social media flickr biasanya digunakan oleh masyarakat dengan tujuan ....",
                options: [
                    "A. mengunggah berita",
                    "B. berbagi foto",
                    "C. pertemanan",
                    "D. berbagi video"
                ],
                correctAnswer: 1
            },
            {
                question: "75) Citizen journalism didasarkan pada warga negara yang memainkan peran aktif dalam proses pengumpulan, pelaporan, analisis, dan menyebarkan berita serta informasi. Dengan demikian, citizen journalism dikenal juga dengan istilah di bawah ini, kecuali jurnalisme ....",
                options: [
                    "A. publik",
                    "B. partisipatif",
                    "C. subjektif",
                    "D. demokratis"
                ],
                correctAnswer: 2
            },
            {
                question: "76) Literasi informasi pertama kali dikemukakan oleh ....",
                options: [
                    "A. Paul Zurkowski",
                    "B. Alexandria",
                    "C. Michael B. Eisenberg",
                    "D. Robert E. Berkowitz"
                ],
                correctAnswer: 0
            },
            {
                question: "77) Orang yang memiliki keterampilan literasi informasi akan mampu melakukan hal berikut ini, kecuali ....",
                options: [
                    "A. menentukan informasi apa yang dibutuhkan",
                    "B. menelusuri informasi yang dibutuhkan secara efisien",
                    "C. mengevaluasi informasi dan sumber-sumbernya",
                    "D. membuat dan menyebarkan informasi untuk mempengaruhi orang lain"
                ],
                correctAnswer: 3
            },
            {
                question: "78) Kegiatan membandingkan, mengelola, menyusun dan menggabungkan informasi yang diperoleh untuk dapat membangun suatu produk informasi yang diperoleh dari sumber informasi yang berhak cipta merupakan salah satu tahapan pemecahan masalah Big6, yaitu ....",
                options: [
                    "A. task definition",
                    "B. information seeking strategies",
                    "C. synthesis",
                    "D. evaluation"
                ],
                correctAnswer: 2
            },
            {
                question: "79) The Society of College, National and University Libraries (Sconul) di Inggris pada tahun 2011 menerbitkan the Seven Pillars of Information Literacy Model. Berikut ini yang termasuk ke dalam seven pillars of information literacy model tersebut adalah ....",
                options: [
                    "A. the information technology conception",
                    "B. construct strategies for locating",
                    "C. the knowledge control",
                    "D. the knowledge extension conception"
                ],
                correctAnswer: 1
            },
            {
                question: "80) Kemampuan untuk melakukan organisasi, evaluasi, dan menyusun informasi menurut susunan yang logis, membedakan antara fakta dan pendapat, serta menggunakan alat bantu visual untuk membandingkan dan mengkontraskan informasi, merupakan salah satu kemampuan yang dimiliki oleh seseorang menurut model ....",
                options: [
                    "A. Empowering Eight (E8)",
                    "B. Big6",
                    "C. Bruce's Seven Faces of Information Literacy",
                    "D. Seven Pillars of Information Literacy"
                ],
                correctAnswer: 1
            },
            {
                question: "81) Tahap pertama dalam 7 tahapan literasi informasi yang diusulkan oleh Christine Bruce adalah the information ....",
                options: [
                    "A. process conception",
                    "B. source conception",
                    "C. technology conception",
                    "D. control conception"
                ],
                correctAnswer: 3
            },
            {
                question: "82) The wisdom conception merupakan salah satu tahapan literasi informasi yang diusulkan oleh Bruce, yaitu tahapan ke- ....",
                options: [
                    "A. 2",
                    "B. 5",
                    "C. 6",
                    "D. 7"
                ],
                correctAnswer: 3
            },
            {
                question: "83) Salah satu jenis elemen literasi adalah literasi media, yaitu kemampuan ....",
                options: [
                    "A. individu untuk menghasilkan informasi melalui database komputer atau literasi ini sering disebut literasi elektronik atau literasi teknologi informasi",
                    "B. untuk memahami dan menggunakan media dalam memperoleh informasi, misalnya melalui televisi, radio, rekaman musik, koran, dan sebagainya",
                    "C. individu dalam memperoleh informasi melalui pustaka digital",
                    "D. untuk menggunakan internet sebagai sarana mengakses informasi dalam lingkungan jaringan website"
                ],
                correctAnswer: 1
            },
            {
                question: "84) Kemampuan untuk memahami dan menggunakan segala bentuk gambar, foto, ilustrasi atau image dalam komputer merupakan kemampuan yang termasuk dalam salah satu jenis elemen literasi, yaitu literasi ....",
                options: [
                    "A. digital",
                    "B. media",
                    "C. komputer",
                    "D. visual"
                ],
                correctAnswer: 3
            },
            {
                question: "85) Berikut ini merupakan keterampilan yang diperlukan untuk menguasai pesan dari media tertentu berdasarkan jenis elemen literasi media, kecuali ....",
                options: [
                    "A. kemampuan diri kita untuk berpikir secara kritis terhadap suatu hal (critical thinking skills)",
                    "B. mengalokasikan sumber secara intelektual dan fisik, dan menemukan informasi dari berbagai sumber (location and access)",
                    "C. pemahaman akan proses komunikasi massa (understanding of mass comm process)",
                    "D. kesadaran akan dampak media terhadap individu dan masyarakat (awareness of media impact)"
                ],
                correctAnswer: 3
            },
            {
                question: "86) Situs web Amerika yang dianggap oleh ilmuwan, pemerintah, serta dokter anak sebagai salah satu otoritas utama di bidang kesehatan dan kesejahteraan anak-anak adalah ....",
                options: [
                    "A. Pediatricians of America",
                    "B. American Academy of Pediatrics",
                    "C. American College of Pediatricians",
                    "D. Pedagogy in America"
                ],
                correctAnswer: 1
            },
            {
                question: "87) Kegiatan penelusuran sumber informasi sampai ke hulu sumber dengan cara mengakses tautan asli sumber berita dikenal dengan istilah ....",
                options: [
                    "A. Go Upstream",
                    "B. Fake news",
                    "C. searching",
                    "D. surfing"
                ],
                correctAnswer: 0
            },
            {
                question: "88) Salah satu jenis media sosial yang banyak digunakan oleh masyarakat adalah bookmarking. Media sosial bookmarking yang paling populer adalah ....",
                options: [
                    "A. Pinterest",
                    "B. Youtube",
                    "C. Facebook",
                    "D. Yahoo"
                ],
                correctAnswer: 0
            },
            {
                question: "89) Twitter, Scoop.It, Reddit merupakan contoh jenis media sosial ....",
                options: [
                    "A. Wiki",
                    "B. Content Sharing",
                    "C. Bookmarking",
                    "D. Social Network"
                ],
                correctAnswer: 2
            },
            {
                question: "90) Situs khusus milik Yahoo! yang mengkonsentrasikan diri pada image sharing dengan kontributor ahli di bidang fotografi di seluruh dunia adalah ....",
                options: [
                    "A. Flickr",
                    "B. Instagram",
                    "C. Youtube",
                    "D. Facebook"
                ],
                correctAnswer: 0
            },
            {
                question: "91) Situs media sosial dengan fitur tertentu yang digunakan oleh masyarakat dengan tujuan untuk menjalin sebuah hubungan dan interaksi dengan sesama adalah ....",
                options: [
                    "A. Instagram",
                    "B. Flickr",
                    "C. Pinterest",
                    "D. MySpace"
                ],
                correctAnswer: 0
            },
            {
                question: "92) Media sosial memiliki dampak positif sebagai berikut, kecuali ....",
                options: [
                    "A. menyediakan informasi yang tepat dan akurat",
                    "B. menambah wawasan dan pengetahuan",
                    "C. sarana penyebaran ideologi paling efektif dan efisien",
                    "D. cara cepat menjadi terkenal"
                ],
                correctAnswer: 3
            },
            {
                question: "93) Salah satu dampak negatif media sosial yang dirasakan oleh masyarakat yaitu ....",
                options: [
                    "A. berkurangnya interaksi langsung, lebih banyak di dunia maya",
                    "B. bertambahnya pengeluaran",
                    "C. hilang pekerjaan",
                    "D. hilangnya kepercayaan terhadap orang lain"
                ],
                correctAnswer: 0
            },
            {
                question: "94) Saat ini marak kasus penipuan melalui media sosial. Berikut ini yang merupakan salah satu ciri akun media sosial seseorang palsu adalah ....",
                options: [
                    "A. tidak ada foto pemilik akun",
                    "B. memiliki akun dengan nama yang sama di beberapa media sosial",
                    "C. menggunakan foto orang lain untuk nama akun yang berbeda di beberapa jenis media sosial",
                    "D. tidak mencantumkan nomor telepon di media sosial"
                ],
                correctAnswer: 2
            },
            {
                question: "95) Salah satu alasan mengapa berita palsu atau hoax biasanya langsung dipercaya oleh individu atau suatu kelompok adalah ....",
                options: [
                    "A. sesuai dengan pendapat atau sikap yang dimilikinya",
                    "B. berita hoax lebih meyakinkan",
                    "C. orang lebih tertarik untuk membaca berita hoax daripada fakta",
                    "D. saat ini tidak ada berita yang dapat dipercaya"
                ],
                correctAnswer: 0
            },
            {
                question: "96) Di bawah ini yang merupakan alasan mahasiswa harus berhati-hati dan lebih baik tidak menggunakan Wikipedia sebagai referensi tulisan saintifik adalah ....",
                options: [
                    "A. bias informasi karena konten dapat diedit oleh siapa pun dan kapan pun",
                    "B. tidak mencantumkan sumber yang jelas",
                    "C. ditulis oleh anak muda",
                    "D. informasi yang dimuat di Wikipedia tidak berhubungan dengan tulisan ilmiah"
                ],
                correctAnswer: 0
            },
            {
                question: "97) Faktor yang menjadi kekuatan, kelemahan, dan perbedaan terbesar Wikipedia adalah ....",
                options: [
                    "A. bersifat terbatas dan hanya diperuntukkan bagi orang atau kelompok tertentu",
                    "B. memiliki basis kontributor besar dan ditulis berdasarkan konsensus, sesuai dengan pedoman dan kebijakan editorial",
                    "C. artikel hanya boleh ditulis oleh ahli di bidangnya",
                    "D. kontributor memperoleh bayaran sesuai dengan jumlah artikel yang ditulisnya"
                ],
                correctAnswer: 1
            },
            {
                question: "98) Di bawah ini merupakan keuntungan penulisan artikel di Wikipedia oleh amatir adalah ....",
                options: [
                    "A. tidak perlu mengeluarkan biaya untuk penulisan",
                    "B. tulisan amatir lebih murni dibandingkan para ahli",
                    "C. tidak perlu mencantumkan referensi atau sumber",
                    "D. mereka memiliki lebih banyak waktu luang"
                ],
                correctAnswer: 0
            },
            {
                question: "99) Salah satu prinsip kolaborasi yang dianut dalam penulisan artikel Wikipedia adalah ....",
                options: [
                    "A. kolaborasi langsung dengan sumber referensi yang berbeda-beda",
                    "B. kolaborasi tidak langsung dengan satu sumber referensi",
                    "C. kolaborasi langsung dengan satu sumber referensi",
                    "D. kolaborasi tidak langsung dengan sumber referensi yang berbeda"
                ],
                correctAnswer: 0
            },
            {
                question: "100) Jenis tulisan yang biasanya dimuat di Wikipedia adalah ....",
                options: [
                    "A. cerita fiksi",
                    "B. cerita non fiksi",
                    "C. seluruh informasi yang memiliki sumber referensi",
                    "D. informasi tanpa perlu mencantumkan referensi atau sumber"
                ],
                correctAnswer: 2
            },
            {
                question: "101) Wikipedia membuka kesempatan bagi siapa pun yang ingin berkontribusi dalam penulisan konten atau materi. Jumlah referensi minimal yang harus dipenuhi oleh penulis adalah ....",
                options: [
                    "A. 2",
                    "B. 4",
                    "C. 5",
                    "D. tidak ada aturan pasti yang mengatur hal tersebut"
                ],
                correctAnswer: 3
            },
            {
                question: "102) Alasan mengapa penulis tidak perlu mencantumkan nama pada saat menjadi kontributor pada Wikipedia adalah ....",
                options: [
                    "A. artikel dikembangkan secara kolaboratif dan sukarela",
                    "B. reabilitas informasi yang ada masih dipertanyakan",
                    "C. menjaga kerahasiaan identitas penulis",
                    "D. penulis tidak dibayar"
                ],
                correctAnswer: 0
            },
            {
                question: "103) Wikipedia merupakan ensiklopedia yang ditulis oleh beberapa kolaborator tanpa menyebutkan nama, di mana penulisannya sesuai dengan lima pilar, di antaranya adalah ....",
                options: [
                    "A. berdasarkan sudut pandang penulis",
                    "B. memiliki aturan yang pasti",
                    "C. ditulis dari sudut pandang netral",
                    "D. tidak boleh didistribusikan secara gratis"
                ],
                correctAnswer: 2
            },
            {
                question: "104) Pada awalnya, Wikipedia merupakan proyek pelengkap untuk ....",
                options: [
                    "A. Wikimedia",
                    "B. Nupedia",
                    "C. Encyclopaedia Britannica",
                    "D. Jurnal Nature"
                ],
                correctAnswer: 1
            },
            {
                question: "105) Pengeditan artikel Wikipedia dibatasi untuk mencegah adanya gangguan atau vandalisme. Pengertian vandalisme tersebut adalah ....",
                options: [
                    "A. aktivitas mengganti isi artikel dengan opini pribadi",
                    "B. tidak sengaja menghapus artikel yang sudah ada",
                    "C. penambahan, penghapusan, atau pengubahan isi yang dengan sengaja dilakukan untuk mengurangi kualitas ensiklopedia",
                    "D. mengganti artikel orang lain dengan artikel baru dengan tujuan meningkatkan kualitas ensiklopedia"
                ],
                correctAnswer: 2
            },
            {
                question: "106) Media diartikan sebagai sarana berkomunikasi dan sumber informasi merupakan pendapat dari ....",
                options: [
                    "A. Smaldino dkk. (2018)",
                    "B. New Oxford American Dictionary",
                    "C. AECT",
                    "D. Maseri (2019)"
                ],
                correctAnswer: 0
            },
            {
                question: "107) Media dapat disebut sebagai 'media pembelajaran' (instructional media) ketika memuat ....",
                options: [
                    "A. informasi",
                    "B. pesan dengan tujuan pembelajaran",
                    "C. ide",
                    "D. saran"
                ],
                correctAnswer: 1
            },
            {
                question: "108) Media digital termasuk kontinu atau diskrit merupakan pembagian media digital berdasarkan ....",
                options: [
                    "A. asalnya",
                    "B. pemberi pesan",
                    "C. waktunya",
                    "D. penerima pesan"
                ],
                correctAnswer: 2
            },
            {
                question: "109) Pemilihan media pembelajaran hendaknya mempertimbangkan kesesuaian antara karakteristik siswa dan karakteristik media. Pemilihan media tersebut berdasarkan landasan ....",
                options: [
                    "A. filosofis",
                    "B. psikologis",
                    "C. teknologis",
                    "D. empiris"
                ],
                correctAnswer: 1
            },
            {
                question: "110) Adobe Premiere biasanya digunakan untuk pembuatan ....",
                options: [
                    "A. video instruksional",
                    "B. LMS",
                    "C. konten interaktif",
                    "D. screen casting"
                ],
                correctAnswer: 0
            },
            {
                question: "111) Sway merupakan aplikasi berbasis web dari perusahaan ....",
                options: [
                    "A. Microsoft",
                    "B. Google",
                    "C. Yahoo",
                    "D. Blackberry"
                ],
                correctAnswer: 0
            },
            {
                question: "112) Fungsi utama dari Sway adalah ....",
                options: [
                    "A. presentasi digital online",
                    "B. membuat website",
                    "C. mendesain gambar",
                    "D. membuat aplikasi"
                ],
                correctAnswer: 0
            },
            {
                question: "113) Langkah awal yang digunakan untuk membuat presentasi dengan Sway tanpa menggunakan template adalah memilih menu ....",
                options: [
                    "A. storyline",
                    "B. new blank Sway",
                    "C. end from a document",
                    "D. blank template"
                ],
                correctAnswer: 1
            },
            {
                question: "114) Jika Anda sudah memiliki dokumen yang berisi artikel, maka untuk membuat storyline, Anda harus memilih menu ....",
                options: [
                    "A. Start from a document",
                    "B. New blank Sway",
                    "C. open a new template",
                    "D. open recent"
                ],
                correctAnswer: 0
            },
            {
                question: "115) Menu design digunakan untuk ....",
                options: [
                    "A. menampilkan hasil pengembangan storyline",
                    "B. mengedit video",
                    "C. membuat hyperlink",
                    "D. menghapus storyline"
                ],
                correctAnswer: 0
            },
            {
                question: "116) Pergerakan komunitas global yang bertujuan untuk memberikan akses tak terbatas terhadap output/hasil penelitian ilmiah termasuk yang ada pada jurnal-jurnal, tesis, monograf ilmiah, dan bab buku merupakan dimensi dari ....",
                options: [
                    "A. open access",
                    "B. OER",
                    "C. open policy",
                    "D. open textbook"
                ],
                correctAnswer: 0
            },
            {
                question: "117) Gerakan global yang telah menghasilkan banyak perangkat lunak terbuka dan tanpa biaya adalah ....",
                options: [
                    "A. open access",
                    "B. OER",
                    "C. open educational practices",
                    "D. open source software"
                ],
                correctAnswer: 3
            },
            {
                question: "118) Eric Hoffer, seorang filsuf Amerika, mengatakan bahwa orang 'kaya' adalah orang yang ....",
                options: [
                    "A. memiliki harta melimpah",
                    "B. memiliki pengetahuan yang luas",
                    "C. mendistribusikan ilmu pengetahuan secara luas",
                    "D. memiliki kebebasan dan kepercayaan diri tanpa mengambil kebebasan dan kepercayaan diri orang lain"
                ],
                correctAnswer: 1
            },
            {
                question: "119) Ekspresi yang menyiratkan spirit/semangat untuk berkolaborasi yang difasilitasi teknologi internet yang bersifat terbuka disebut ....",
                options: [
                    "A. kebebasan berpendapat di internet",
                    "B. kebebasan berbagi materi digital",
                    "C. kebebasan digital",
                    "D. kemerdekaan berekspresi di internet"
                ],
                correctAnswer: 1
            },
            {
                question: "120) FOSS adalah perangkat lunak yang berlisensi terbuka untuk digunakan, disalin, ataupun didistribusikan/dibagi kembali. Prinsip kunci FOSS terletak pada ....",
                options: [
                    "A. biaya yang rendah",
                    "B. pendistribusian tanpa biaya",
                    "C. pemberian sumber kodifikasi (source code) program pada pengguna",
                    "D. izin penggunaan tanpa batas waktu"
                ],
                correctAnswer: 2
            },
            {
                question: "121) Kerangka 5R yang diperkenalkan David Wiley ini merupakan pengguna karya untuk ....",
                options: [
                    "A. memiliki, menggunakan, memodifikasi, menggabungkan, mendistribusi ulang karya",
                    "B. memiliki, menggunakan, memodifikasi, mengubah, menggabungkan",
                    "C. mendapatkan, menggunakan, mengubah, menggabungkan, menjual",
                    "D. mendapatkan, menggunakan, mendistribusikan, menggabungkan, mengkomersialkan"
                ],
                correctAnswer: 0
            },
            {
                question: "122) OER merupakan materi yang ....",
                options: [
                    "A. disebarkan dengan hak cipta penuh",
                    "B. dikemas dalam bentuk digital",
                    "C. disebarkan dengan lisensi terbuka",
                    "D. bersifat interaktif"
                ],
                correctAnswer: 2
            },
            {
                question: "123) Dimensi 'nilai pendidikan' suatu OER mengandung dua subdimensi, yaitu ....",
                options: [
                    "A. biaya dan penggunaan",
                    "B. format dan desain",
                    "C. digital dan non-digital",
                    "D. biaya dan penyebaran"
                ],
                correctAnswer: 0
            },
            {
                question: "124) Dimensi teknologi pada OER memastikan bahwa pengguna harus bisa ....",
                options: [
                    "A. mengoperasikan OER",
                    "B. menggunakan OER",
                    "C. mendistribusikan OER",
                    "D. mengedit OER"
                ],
                correctAnswer: 3
            },
            {
                question: "125) Praktik pembelajaran yang hanya mungkin dilakukan dengan memanfaatkan kerangka 5R disebut ....",
                options: [
                    "A. pedagogi merdeka",
                    "B. pedagogi berbasis OER",
                    "C. pedagogi 5R",
                    "D. pedagogi berlisensi"
                ],
                correctAnswer: 1
            },
            {
                question: "126) Tujuan asli suatu 'Hak Cipta' menurut Lawrence Lessig adalah untuk ....",
                options: [
                    "A. melindungi pencipta",
                    "B. mempromosikan kemajuan sains dan seni bermanfaat",
                    "C. melindungi praktik distribusi karya cipta",
                    "D. melindungi penerbit karya cipta"
                ],
                correctAnswer: 1
            },
            {
                question: "127) Hak Cipta adalah konsep hukum untuk memberikan hak kepemilikan dan perlindungan kepada ....",
                options: [
                    "A. pencipta",
                    "B. penerbit",
                    "C. masyarakat",
                    "D. pengguna"
                ],
                correctAnswer: 0
            },
            {
                question: "128) Suatu karya yang sama sekali tidak dilindungi oleh hak kekayaan intelektual dan tersedia untuk digunakan oleh semua anggota masyarakat disebut karya ....",
                options: [
                    "A. ber-hak cipta",
                    "B. OER",
                    "C. dalam domain publik",
                    "D. berlisensi terbuka"
                ],
                correctAnswer: 2
            },
            {
                question: "129) Hak eksklusif yang diberikan oleh produk hukum 'hak cipta' meliputi ....",
                options: [
                    "A. hak ekonomi, hak distribusi, hak penciptaan kembali, dan hak pendapatan",
                    "B. hak ekonomi, hak moral, hak terkait, dan pengalihan hak",
                    "C. hak ekonomi, hak penciptaan kembali, dan hak domain publik",
                    "D. hak kepemilikan, hak pendistribusian, dan pengalihan hak"
                ],
                correctAnswer: 1
            },
            {
                question: "130) Masa berlaku 'Hak Cipta' adalah ....",
                options: [
                    "A. sama di semua negara tanpa pengecualian",
                    "B. tanpa batas",
                    "C. terbatas untuk waktu tertentu",
                    "D. otomatis diperpanjang untuk masa tidak terbatas"
                ],
                correctAnswer: 2
            },
            {
                question: "131) Creative Commons merupakan perangkat hukum yang membantu pencipta untuk ....",
                options: [
                    "A. menginisiasi karya kreatif",
                    "B. mendaftarkan karya ciptanya",
                    "C. mendistribusikan/membagikan karya ciptanya",
                    "D. mendapatkan hak ekonominya"
                ],
                correctAnswer: 2
            },
            {
                question: "132) Creative Commons yang menyatakan pengguna boleh menggunakan suatu karya cipta untuk kepentingan komersial dari CC di bawah ini adalah ....",
                options: [
                    "A. CC BY",
                    "B. CC BY-NC",
                    "C. CC BY-NC-SA",
                    "D. CC BY-NC-ND"
                ],
                correctAnswer: 0
            },
            {
                question: "133) Memperhatikan definisi OER, maka unsur lisensi Creative Commons yang tidak bisa digunakan jika karya kita ingin dijadikan OER adalah unsur ....",
                options: [
                    "A. Atribusi (BY)",
                    "B. Non-komersial (NC)",
                    "C. Berbagi Serupa (SA)",
                    "D. Tanpa Turunan (ND)"
                ],
                correctAnswer: 3
            },
            {
                question: "134) Karya dengan lisensi CC yang sama sekali tidak dapat digabungkan dengan karya berlisensi CC lainnya adalah ....",
                options: [
                    "A. CC BY-ND dan CC BY-NC-ND",
                    "B. CC BY dan CC BY-SA",
                    "C. CC BY dan CC BY-NC",
                    "D. CC BY-SA dan CC BY-NC"
                ],
                correctAnswer: 0
            },
            {
                question: "135) Perbedaan prinsip pokok 'Hak Cipta' dengan CC adalah ....",
                options: [
                    "A. mengubah 'siapa' yang dilindungi",
                    "B. memberikan kebebasan kepada pencipta untuk skema berbagi hasil ciptaannya",
                    "C. mengubah dari 'seluruh hak dilindungi' menjadi 'sebagian hak dilindungi'",
                    "D. semua benar"
                ],
                correctAnswer: 2
            },
            {
                question: "136) Warga digital memerlukan literasi tertentu yang memungkinkan mereka dapat beradaptasi dengan dunia digital secara aman. Literasi apa saja yang diperlukan, kecuali ....",
                options: [
                    "A. literasi digital",
                    "B. literasi membaca",
                    "C. literasi informasi",
                    "D. literasi kemanusiaan"
                ],
                correctAnswer: 3
            },
            {
                question: "137) Warga digital harus memiliki sikap hormat terhadap orang lain dan menjadi pelindung hak semua orang bersama-sama berperilaku etis dan sesuai dengan norma sosial online, literasi ini termasuk sebagai ....",
                options: [
                    "A. literasi digital",
                    "B. literasi informasi",
                    "C. kesantunan digital",
                    "D. kecakapan digital"
                ],
                correctAnswer: 2
            },
            {
                question: "138) Pemahaman teknologi digital menjadi salah satu atribut yang harus ada pada warga digital sama halnya dengan pada saat kita menjadi warga masyarakat kita juga harus mengetahui atributnya. Pemahaman teknologi digital merupakan bagian dari literasi kecakapan digital yang meliputi antara lain ....",
                options: [
                    "A. mengetahui akibat dari keputusan online",
                    "B. akibat penggunaan akun digital secara online",
                    "C. memperhatikan hak-hak dari warga digital lainnya",
                    "D. membuat media digital secara re-mix"
                ],
                correctAnswer: 3
            },
            {
                question: "139) Warga digital pada umumnya menghabiskan waktunya dengan media digital, atribut warga digital yang berkaitan dengan bagaimana sebaiknya warga digital berinteraksi dengan media digital termasuk dalam atribut ....",
                options: [
                    "A. kecakapan digital",
                    "B. kesehatan dan kesejahteraan digital",
                    "C. hukum digital",
                    "D. hak dan tanggung jawab digital"
                ],
                correctAnswer: 0
            },
            {
                question: "140) Atribut warga digital yang berusaha untuk mencegah agar mereka tidak terjerumus dalam cyberbullying atau hoax termasuk dalam atribut ....",
                options: [
                    "A. hak dan tanggung jawab digital",
                    "B. keamanan digital dan privasi",
                    "C. hukum digital",
                    "D. kesopanan digital"
                ],
                correctAnswer: 1
            },
            {
                question: "141) Permasalahan psikologis yang muncul disebabkan karena Anda percaya terhadap penyakit yang Anda baca secara online disebut sebagai ....",
                options: [
                    "A. Cyberchondria",
                    "B. Cybersickness",
                    "C. Depression",
                    "D. Nomofobia"
                ],
                correctAnswer: 0
            },
            {
                question: "142) Manakah dari istilah berikut yang paling menggambarkan praktik online memposting komentar online dengan tujuan mengecewakan orang lain untuk membangkitkan respons emosional ....",
                options: [
                    "A. Pelecehan online",
                    "B. Sockpuppet",
                    "C. Troli Internet",
                    "D. Ketidakadilan akses"
                ],
                correctAnswer: 2
            },
            {
                question: "143) Praktik Troll dengan memposting panjang dan menulis banyak paragraf tentang apa pun yang mereka ketahui, apakah ada yang membacanya atau tidak, paling baik dijelaskan dengan istilah berikut ....",
                options: [
                    "A. Flaming",
                    "B. Blabbermouth",
                    "C. Fisking",
                    "D. Rebutta"
                ],
                correctAnswer: 0
            },
            {
                question: "144) Penghilangan hambatan sistemik yang ditimbulkan pada seseorang yang berkaitan dengan akses Internet sebagai salah bentuk dari prinsip ....",
                options: [
                    "A. Inclusion",
                    "B. Equality",
                    "C. Equity",
                    "D. Fairness"
                ],
                correctAnswer: 2
            },
            {
                question: "145) Mencuri foto daring seseorang dan kemudian membuat akun media sosial fiktif untuk keuntungan pribadi, paling baik dijelaskan oleh konsep berikut ....",
                options: [
                    "A. Doxxing",
                    "B. Impersonation",
                    "C. Catfishing",
                    "D. Swatting"
                ],
                correctAnswer: 2
            }
        ];

        // Fungsi untuk memilih 50 soal acak dari 145 soal
        function getRandomQuestions(questions, count) {
            const shuffled = [...questions].sort(() => 0.5 - Math.random());
            return shuffled.slice(0, count);
        }

        // Pilih 50 soal acak
        const selectedQuestions = getRandomQuestions(allQuestions, 50);
        let userAnswers = Array(50).fill(null);
        let answeredCount = 0;

        // Fungsi untuk menampilkan soal
        function displayQuestions() {
            const quizContainer = document.getElementById('quiz-container');
            quizContainer.innerHTML = '';
            
            selectedQuestions.forEach((question, index) => {
                const questionElement = document.createElement('div');
                questionElement.className = 'question';
                
                const questionNumber = document.createElement('div');
                questionNumber.className = 'question-number';
                questionNumber.textContent = `Question ${index + 1}`;
                
                const questionText = document.createElement('div');
                questionText.className = 'question-text';
                questionText.textContent = question.question.replace(/^\d+\)\s/, '');
                
                const optionsContainer = document.createElement('div');
                optionsContainer.className = 'options';
                
                question.options.forEach((option, optionIndex) => {
                    const optionElement = document.createElement('div');
                    optionElement.className = 'option';
                    
                    const radio = document.createElement('input');
                    radio.type = 'radio';
                    radio.name = `question-${index}`;
                    radio.id = `question-${index}-option-${optionIndex}`;
                    radio.value = optionIndex;
                    
                    if (userAnswers[index] === optionIndex) {
                        radio.checked = true;
                    }
                    
                    radio.addEventListener('change', () => {
                        userAnswers[index] = optionIndex;
                        updateAnsweredCount();
                    });
                    
                    const label = document.createElement('label');
                    label.htmlFor = `question-${index}-option-${optionIndex}`;
                    label.textContent = option;
                    
                    optionElement.appendChild(radio);
                    optionElement.appendChild(label);
                    optionsContainer.appendChild(optionElement);
                });
                
                questionElement.appendChild(questionNumber);
                questionElement.appendChild(questionText);
                questionElement.appendChild(optionsContainer);
                quizContainer.appendChild(questionElement);
            });
            
            updateAnsweredCount();
        }

        // Fungsi untuk memperbarui jumlah jawaban yang telah diisi
        function updateAnsweredCount() {
            answeredCount = userAnswers.filter(answer => answer !== null).length;
            document.getElementById('answered').textContent = answeredCount;
            
            // Update progress bar
            const progressPercentage = (answeredCount / 50) * 100;
            document.getElementById('progress').style.width = `${progressPercentage}%`;
        }

        // Fungsi untuk menampilkan hasil
        function showResults() {
            let score = 0;
            const resultsContainer = document.getElementById('results');
            const scoreElement = document.getElementById('score');
            const answersContainer = document.getElementById('answers');
            
            answersContainer.innerHTML = '';
            
            selectedQuestions.forEach((question, index) => {
                const answerItem = document.createElement('div');
                answerItem.className = 'answer-item';
                
                const questionText = document.createElement('div');
                questionText.textContent = `${index + 1}. ${question.question.replace(/^\d+\)\s/, '')}`;
                
                const userAnswer = document.createElement('div');
                if (userAnswers[index] !== null) {
                    userAnswer.textContent = `Your answer: ${question.options[userAnswers[index]]}`;
                } else {
                    userAnswer.textContent = 'You did not answer this question.';
                }
                
                const correctAnswer = document.createElement('div');
                correctAnswer.textContent = `Correct answer: ${question.options[question.correctAnswer]}`;
                
                if (userAnswers[index] === question.correctAnswer) {
                    score++;
                    answerItem.classList.add('correct');
                    correctAnswer.innerHTML = `<span class="highlight">${correctAnswer.textContent}</span>`;
                } else if (userAnswers[index] !== null) {
                    answerItem.classList.add('incorrect');
                }
                
                answerItem.appendChild(questionText);
                answerItem.appendChild(userAnswer);
                answerItem.appendChild(correctAnswer);
                answersContainer.appendChild(answerItem);
            });
            
            scoreElement.textContent = score;
            document.getElementById('quiz-container').style.display = 'none';
            document.getElementById('submit-btn').style.display = 'none';
            resultsContainer.style.display = 'block';
        }

        // Fungsi untuk mengulang quiz
        function retryQuiz() {
            userAnswers = Array(50).fill(null);
            answeredCount = 0;
            document.getElementById('quiz-container').style.display = 'block';
            document.getElementById('submit-btn').style.display = 'block';
            document.getElementById('results').style.display = 'none';
            displayQuestions();
        }

        // Event listeners
        document.getElementById('submit-btn').addEventListener('click', showResults);
        document.getElementById('retry-btn').addEventListener('click', retryQuiz);

        // Tampilkan soal saat halaman dimuat
        window.onload = displayQuestions;
    </script>
</body>
</html>
