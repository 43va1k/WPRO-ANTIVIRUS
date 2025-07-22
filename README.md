# WPRO-ANTIVIRUS
WPRO ANTIVIRUS
// Fichier principal de l'app Flutter Web : WPRO ANTIVIRUS
import 'package:flutter/material.dart';

void main() {
  runApp(WproAntivirusApp());
}

class WproAntivirusApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'WPRO ANTIVIRUS',
      debugShowCheckedModeBanner: false,
      theme: ThemeData.dark(),
      home: AntivirusHomePage(),
    );
  }
}

class AntivirusHomePage extends StatefulWidget {
  @override
  _AntivirusHomePageState createState() => _AntivirusHomePageState();
}

class _AntivirusHomePageState extends State<AntivirusHomePage> {
  bool isScanning = false;
  bool scanCompleted = false;
  bool foundThreats = true;
  bool isCleaning = false;
  bool cleanCompleted = false;

  void startScan() {
    setState(() {
      isScanning = true;
      scanCompleted = false;
      foundThreats = true;
      cleanCompleted = false;
    });
    Future.delayed(Duration(seconds: 3), () {
      setState(() {
        isScanning = false;
        scanCompleted = true;
      });
    });
  }

  void startClean() {
    setState(() {
      isCleaning = true;
      cleanCompleted = false;
    });
    Future.delayed(Duration(seconds: 2), () {
      setState(() {
        isCleaning = false;
        cleanCompleted = true;
        foundThreats = false;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('WPRO ANTIVIRUS'),
        centerTitle: true,
        backgroundColor: Colors.blueAccent,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: SingleChildScrollView(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.center,
            children: [
              SizedBox(height: 30),
              Text('Statut de l'appareil',
                  style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
              SizedBox(height: 20),
              if (isScanning)
                Column(
                  children: [
                    CircularProgressIndicator(),
                    SizedBox(height: 10),
                    Text('Analyse en cours...'),
                  ],
                )
              else if (scanCompleted && foundThreats)
                Column(
                  children: [
                    Icon(Icons.warning, color: Colors.red, size: 60),
                    SizedBox(height: 10),
                    Text('Menaces détectées !'),
                    SizedBox(height: 20),
                    ElevatedButton.icon(
                      onPressed: startClean,
                      icon: Icon(Icons.cleaning_services),
                      label: Text('Nettoyer maintenant'),
                    ),
                  ],
                )
              else if (cleanCompleted)
                Column(
                  children: [
                    Icon(Icons.check_circle, color: Colors.green, size: 60),
                    SizedBox(height: 10),
                    Text('Appareil propre !'),
                  ],
                )
              else
                ElevatedButton.icon(
                  onPressed: startScan,
                  icon: Icon(Icons.shield),
                  label: Text('Scanner maintenant'),
                ),
              SizedBox(height: 40),
              Divider(),
              ListTile(
                leading: Icon(Icons.copy),
                title: Text('Fichiers en double détectés : 5'),
                trailing: TextButton(
                  onPressed: () {},
                  child: Text('Voir'),
                ),
              ),
              ListTile(
                leading: Icon(Icons.memory),
                title: Text('RAM optimisée'),
                trailing: Icon(Icons.check, color: Colors.green),
              ),
              ListTile(
                leading: Icon(Icons.battery_charging_full),
                title: Text('Batterie économisée'),
                trailing: Icon(Icons.check, color: Colors.green),
              ),
              SizedBox(height: 30),
              Text(
                '🔗 Ce lien est un aperçu ChatGPT, pas une app web réelle. Pour l’utiliser sur co.medyan.com, tu dois héberger cette app sur GitHub Pages ou autre hébergement web public.',
                style: TextStyle(fontSize: 14, color: Colors.amberAccent),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 10),
              Text(
                '⛔ Exemple : le lien ChatGPT https://chatgpt.com/canvas/shared/... ne peut PAS être utilisé directement dans co.medyan.com.',
                style: TextStyle(fontSize: 13, color: Colors.redAccent),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 30),
            ],
          ),
        ),
      ),
    );
  }
}
 
