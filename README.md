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
```
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
```
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
