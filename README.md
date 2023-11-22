# Inventoriorio - mobile

<details> 
<summary>Tugas 7</summary>

## Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?

Stateless widget dalam Flutter tidak menyimpan atau melacak perubahan status internal dan umumnya digunakan untuk tampilan statis. Sementara itu, stateful widget memiliki kemampuan untuk menyimpan dan melacak perubahan status internal, cocok untuk tampilan yang memerlukan pembaruan berdasarkan input atau interaksi pengguna. Stateful widget memerlukan lebih banyak sumber daya dan kompleksitas karena harus mengelola status internal.

| Stateless | Stateful |
| :-: | :-: | 
| Statis | Dinamis |
| Tidak bergantung pada perubahan data atau perilaku | Dapat berubah saat *runtime* tergantung data dan input user |
| Tidak memiliki state, di update hanya jika terdapat perubahan data | Memiliki state internal, di update jika ada perubahan input data atau state |
| Efisien dan sederhana | Lebih kompleks dan memerlukan lebih banyak sumber daya |

## Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.

- MyApp: Berfungsi sebagai widget root dari aplikasi.
- MaterialApp: Mengatur konfigurasi dasar aplikasi seperti judul, tema, dan halaman beranda.
- MyHomePage: Menampilkan antarmuka utama aplikasi.
- Item: Merepresentasikan model item dengan atribut seperti name, icon, dan color.
- ItemCard: Merender kartu untuk setiap item dalam GridView
- GridView: Menampilkan daftar item dalam tata letak grid.
- Scaffold: Menyediakan struktur dasar aplikasi dengan AppBar dan body.
- AppBar: Menampilkan judul aplikasi di bagian atas.
- SingleChildScrollView: Memungkinkan kontennya untuk discroll jika kontennya melebihi ukuran layar.
- Column: Mengatur widget-Widget secara vertikal di dalam SingleChildScrollView.
- Padding: Menambahkan padding pada kontennya.
- Text: Menampilkan teks dengan style tertentu.

## Step by step pengimplementasian

- Menginstal flutter, lalu menginstall ekstensi dart dan flutter dalam vscode.
- Membuat proyek flutter baru dengan nama Inventoriorio
- Dalam direktori `lib`, membuat berkas baru dengan nama `menu.dart`.
- Dalam direktori `lib`, mengisi berkas `main.dart` dengan :
```dart
import 'package:flutter/material.dart';
import 'package:inventoriorio/menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Inventoriorio Mobile',
        debugShowCheckedModeBanner: false,
        theme: ThemeData(
          // This is the theme of your application.
          //
          // TRY THIS: Try running your application with "flutter run". You'll see
          // the application has a blue toolbar. Then, without quitting the app,
          // try changing the seedColor in the colorScheme below to Colors.green
          // and then invoke "hot reload" (save your changes or press the "hot
          // reload" button in a Flutter-supported IDE, or press "r" if you used
          // the command line to start the app).
          //
          // Notice that the counter didn't reset back to zero; the application
          // state is not lost during the reload. To reset the state, use hot
          // restart instead.
          //
          // This works for code too, not just values: Most code changes can be
          // tested with just a hot reload.
          useMaterial3: true,
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
        ),
        home: MyHomePage());
  }
}
```
- Dalam direktori `lib`, mengisi berkas `menu.dart` dengan:
```dart
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);

  final List<Item> items = [
    Item("Lihat Item", Icons.checklist,
        const Color.fromARGB(255, 236, 191, 191)),
    Item("Tambah Item", Icons.add_shopping_cart,
        const Color.fromARGB(255, 177, 252, 206)),
    Item("Logout", Icons.logout, const Color.fromARGB(255, 206, 187, 250)),
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Inventoriorio',
        ),
      ),
      body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding dari halaman
          child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                  'Inventoriorio', // Text yang menandakan toko
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((Item item) {
                  // Iterasi untuk setiap item
                  return ItemCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

class Item {
  final String name;
  final IconData icon;
  final Color color;

  Item(this.name, this.icon, this.color);
}

class ItemCard extends StatelessWidget {
  final Item item;

  const ItemCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
        },
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.black,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.black),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

</details>

<details> 
<summary>Tugas 8</summary>

## Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!

Navigator.push():
- Digunakan untuk menambahkan layar baru ke dalam tumpukan navigasi.
- Memungkinkan pengguna kembali ke layar sebelumnya dengan menggunakan tombol kembali.
- Menambahkan layar baru di atas layar saat ini.
contoh penggunaan:
```dart
onTap: () {
  Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => const ItemFormPage(),
      ));
}
```

Navigator.pushReplacement():
- Digunakan untuk menggantikan layar saat ini dengan layar baru.
- Tidak memungkinkan pengguna untuk kembali ke layar sebelumnya.
- Berguna ketika ingin menggantikan layar login dengan layar utama setelah pengguna berhasil masuk.
contoh penggunaan:
```dart 
onTap: () {
  Navigator.pushReplacement(
      context,
      MaterialPageRoute(
        builder: (context) => MyHomePage(),
      ));
}
```

## Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!

1. Container: Widget dasar untuk mengatur properti seperti padding, margin, dan warna latar belakang. Digunakan sebagai wadah untuk elemen-elemen lainnya.
2. Row: Menyusun elemen-elemen secara horizontal.
3. Column: Menyusun elemen-elemen secara vertikal.
4. ListView: Menampilkan daftar elemen secara vertikal yang dapat di-scroll.
5. GridView: Menyusun elemen-elemen dalam bentuk grid, baik secara vertikal maupun horizontal.
6. Stack: Menumpuk elemen-elemen di atas satu sama lain. Digunakan untuk tata letak yang lebih kompleks, di mana elemen-elemen mungkin saling tumpang tindih.
7. Expanded: Digunakan di dalam Row atau Column untuk memberikan ruang yang setara untuk anak-anaknya, memanfaatkan sebanyak mungkin ruang yang tersedia.
8. Flexible: Memberikan fleksibilitas pada widget-child di dalam Row atau Column.
9. Wrap: Membungkus elemen-elemen ke baris baru jika melebihi lebar yang ditentukan.
10. SizedBox: Menentukan dimensi widget dengan lebar dan tinggi tertentu.

## Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!

Elemen input yang dipakai untuk form adalah `TextFormField`, digunakan untuk memasukkan input berupa teks

1. TextFormField untuk Nama Item:
   - Decoration: Digunakan untuk memberikan hint, label, dan gaya border pada input.
   - onChanged: Mengambil nilai yang diinputkan dan menyimpannya ke dalam variabel `_name`.
   - Validator: Memastikan bahwa input tidak boleh kosong.

2. TextFormField untuk Jumlah Item:
   - Decoration: Memberikan hint, label, dan gaya border pada input.
   - onChanged: Mengambil nilai yang diinputkan, mengonversinya ke dalam tipe data `int`, dan menyimpannya ke dalam variabel `_amount`.
   - Validator: Memastikan bahwa input tidak boleh kosong dan harus berupa angka.

3. TextFormField untuk Deskripsi:
   - Decoration: Memberikan hint, label, dan gaya border pada input.
   - onChanged: Mengambil nilai yang diinputkan dan menyimpannya ke dalam variabel `_description`.
   - Validator: Memastikan bahwa input tidak boleh kosong.

## Bagaimana penerapan clean architecture pada aplikasi Flutter?

Clean Architecture berfokus pada pemisahan tanggung jawab dan ketergantungan antara lapisan-lapisan dalam aplikasi. Pada aplikasi Flutter, implementasi Clean Architecture melibatkan tiga lapisan utama: Presentation Layer, Domain Layer, dan Data Layer.
- Presentation Layer: Menangani tampilan dan UI.
- Domain Layer: Berisi logika dan aturan aplikasi.
- Data Layer: Menangani akses data.

## Step by step pengimplementasian

- Membuat navigasi dengan membuat drawer dengan nama berkas `left_drawer.dart` yang diisi:
```dart
import 'package:flutter/material.dart';
import 'package:inventoriorio/screens/menu.dart';
import 'package:inventoriorio/screens/item_form.dart'; 

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'Item List',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text(
                  "Catat seluruh itemmu di sini!",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    fontWeight: FontWeight.normal,
                    color: Colors.white,
                  ),
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Item'),
            // Bagian redirection ke ItemFormPage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => const ItemFormPage(),
                  ));
            },
          ),
        ],
      ),
    );
  }
}
```
- Kemudian membuat form input untuk menambahkan item dengan membuat berkas `item_form.dart` dan diisi:
```dart
import 'package:flutter/material.dart';
import 'package:inventoriorio/widgets/left_drawer.dart';

class ItemFormPage extends StatefulWidget {
  const ItemFormPage({super.key});

  @override
  State<ItemFormPage> createState() => _ItemFormPageState();
}

class _ItemFormPageState extends State<ItemFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Center(
          child: Text(
            'Form Tambah Item',
          ),
        ),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Form(
        key: _formKey,
        child: SingleChildScrollView(
          child:
              Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Nama Item",
                  labelText: "Nama Item",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _name = value!;
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Nama tidak boleh kosong!";
                  }
                  return null;
                },
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Jumlah item",
                  labelText: "Jumlah item",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _amount = int.parse(value!);
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Jumlah item tidak boleh kosong!";
                  }
                  if (int.tryParse(value) == null) {
                    return "Jumlah item harus berupa angka!";
                  }
                  return null;
                },
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: TextFormField(
                decoration: InputDecoration(
                  hintText: "Deskripsi",
                  labelText: "Deskripsi",
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(5.0),
                  ),
                ),
                onChanged: (String? value) {
                  setState(() {
                    _description = value!;
                  });
                },
                validator: (String? value) {
                  if (value == null || value.isEmpty) {
                    return "Deskripsi tidak boleh kosong!";
                  }
                  return null;
                },
              ),
            ),
            Align(
              alignment: Alignment.bottomCenter,
              child: Padding(
                padding: const EdgeInsets.all(8.0),
                child: ElevatedButton(
                  style: ButtonStyle(
                    backgroundColor: MaterialStateProperty.all(Colors.indigo),
                  ),
                  onPressed: () {
                    if (_formKey.currentState!.validate()) {
                      showDialog(
                        context: context,
                        builder: (context) {
                          return AlertDialog(
                            title: const Text('Item berhasil tersimpan'),
                            content: SingleChildScrollView(
                              child: Column(
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                  Text('Nama: $_name'),
                                  Text('Jumlah: $_amount'),
                                  Text('Deskripsi: $_description'),
                                ],
                              ),
                            ),
                            actions: [
                              TextButton(
                                child: const Text('OK'),
                                onPressed: () {
                                  Navigator.pop(context);
                                },
                              ),
                            ],
                          );
                        },
                      );
                    }
                    _formKey.currentState!.reset();
                  },
                  child: const Text(
                    "Save",
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              ),
            ),
          ]),
        ),
      ),
    );
  }
}
```
- Selanjutnya memindahkan widget `Item` dari berkas `menu.dart` ke berkas baru `item_card.dart`.
- Menambahkan fungsi navigasi pada widget `ItemCard` saat tombol `Tambah Item` ditekan akan menuju ke form input, dengan memodifikasi isi dari atribut `onTap` pada `InkWell` menjadi:
```dart
...
Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Area responsive terhadap sentuhan
        onTap: () {
          // Memunculkan SnackBar ketika diklik
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("Kamu telah menekan tombol ${item.name}!")));
          // Navigate ke route yang sesuai (tergantung jenis tombol)
          if (item.name == "Tambah Item") {
            Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => const ItemFormPage(),
                ));
          }
        },
        ...
```
- Melakukan pengaturan kembali pada berkas - berkas pada direktori `lib`. Membuat direktori baru dalam direktori `lib`, yaitu direktori `screens` dan `widgets`. Kemudian memindahkan berkas `item_form.dart` dan `menu.dart` ke direktori `screens`, dan memindahkan berkas `item_card.dart` dan `left_drawer.dart` ke direktori `widgets`.

</details>

<details> 
<summary>Tugas 9</summary>

## Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?

Bisa saja, jika data JSON cukup sederhana dan strukturnya tidak terlalu kompleks, langsung mengambil data tanpa membuat model mungkin lebih efisien. Namun, jika data kompleks, membuat model bisa membantu dalam mengorganisir data dengan lebih mudah.

## Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.

CookieRequest adalah objek untuk mengelola permintaan dengan cookie dalam Flutter. Membagikan instance ke semua komponen memastikan konsistensi data, efisiensi sumber daya, dan kemudahan pemeliharaan, terutama jika cookie digunakan secara luas untuk otentikasi atau data bersama.

## Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.

- Melakukan flutter pub add http, melakukan import library dan package yang dibutuhkan:
```dart
import 'package:http/http.dart' as http;
import 'dart:convert';
```
- Melakukan fetch data dari url yang ditentukan:
```dart
Future<List<Item>> fetchProduct() async {
    // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
    var url = Uri.parse(
        'http://<URL_APP_KAMU>/json/');
    var response = await http.get(
        url,
        headers: {"Content-Type": "application/json"},
    );
```
- Melakukan decode response menjadi json:
```dart
var data = jsonDecode(utf8.decode(response.bodyBytes));
```
- Melakukan konversi data json menjadi object(dalam tugas ini object Item):
```dart
List<Item> list_item = [];
    for (var d in data) {
        if (d != null) {
            list_item.add(Item.fromJson(d));
        }
    }
```
- Data tersebut yaitu list_item sudah dapat digunakan untuk ditampilkan pada flutter.

## Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

- Input Data Akun di Flutter
- HTTP Request dari Flutter ke Django
- Autentikasi di Django
- Response ke Flutter
- Navigasi menu di Flutter

## Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.

- TextField, adalah widget yang memungkinkan pengguna memasukkan teks.
- SizedBox, adalah widget yang mengatur space kosong.
- ElevatedButton, adalah tombol dengan efek elevasi.
- SnackBar, adalah pesan yang muncul di bagian bawah layar.
- AlertDialog, adalah dialog yang muncul untuk menampilkan pesan.
- Navigator, adalah widget yang mengelola navigasi halaman.
- Provider, adalah bagian dari package provider yang digunakan untuk manajemen state.

## Step by step pengimplementasian



</details>