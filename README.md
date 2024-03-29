## Prembly_flutter
Verify your user or customers with prembly_flutter, it's easy to use.

## Features
Prembly_flutter can be use for more than 4 Africa countries verification which include Nigeria, Ghana, South Africa, Uganda, Kenya, Sierra Leone and Rwanda.

## Getting started
Get started by installing prembly_flutter by following the instruction below.
## Install

Run the following command in your project directory:

`pub get prembly_flutter`

## Get Started

After prembly_flutter has been installed, you should initialize the prembly_flutter plugin in your ```main.dart``` file.

```
void main() {
  // Initializing prembly plugin
  PremblyPlugin.initialize(
    appId: "YOUR_APP_ID_FROM_PREMBLY",
    apiKey: "YOUR_API_KEY_FROM_PREMBLY",
  ).then((_) {
    return runApp(const MyApp());
  });
}
```

Your can get the `App_ID` and `Api-key` from [prembly.com](http://prembly.com).

## Usage
Visit [example/lib/main.dart](https://github.com/Whitecoode/prembly_flutter/blob/master/example/lib/main.dart) to see some short and useful examples of prembly_flutter and how to use them. Below are some examples:
### Examples
### Global
```
// Email verification
void verifyEmail() async {
    var response = await premblyPlugin
        .emailVerifier("test@whitecoode.com");
    print(response);
}

```
### Nigeria
```
// Nigeria Plate Number verification
void verifyPlateNumber() async {
    var response = await premblyPlugin
        .ngPlateNumberVerifier("AA0000000");
    print(response);
}

// Nigeria BVN Number 2.0 verification
void verifyBvnNumber() async {
    var response = await premblyPlugin
        .ngBvnNumberVerifier("54651333604");
    print(response);
}
```
### Ghana
```
// Ghana International Passport verification
void verifyInternationalPassport() async {
    var response = await premblyPlugin
        .ghVerifyInternationalPassport(number: "G0000575");
    print(response);
}

// Ghana Voters Card verification
void verifyVoter() async {
    var response = await premblyPlugin
        .ghVerifyVoters(number: "9001332866",type: "Main");
    print(response);
}
```
### Uganda
```
// Uganda Business verification
void verifyBusiness() async {
    var response = await premblyPlugin
        .ugVerifyBusinessVerification(customerReference: "ref", customerName: "Coode", reservationNumber: "001");
    print(response);
}
```
### Kenya
```

// Kenya International Passport verification
void verifyBusiness() async {
    var response = await premblyPlugin
        .kyVerifyInternationalPassport(customerName: "coode", number: '01234567', customerReference: "ref");
    print(response);
}

// Kenya National Identity verification
void verifyNationalIdentity() async {
    var response = await premblyPlugin
        .kyVerifyNationalIdentityNumber(customerName: "coode", number: '01234567', customerReference: "ref");
    print(response);
}

```
### South Africa
```
// South Africa National Identity verification
void verifyNationalIdentity() async {
    var response = await premblyPlugin.saVerifyNationalIdentity(firstName: "firstName", lastName: "Lethabo", nationalID: "0123474827482", dateOfBirth: "1985-01-20");
    print(response);
}
```
### Sierra Leone
```
// Sierra Leone National Identity verification
void verifyVoters() async {
    var response = await premblyPlugin.slVerifyVotersCard(searchMode: "ID or BIO", firstName: "firstName if(searchMode is BIO)", lastName: "lastName if(searchMode is BIO)", middleName: "middleName if(searchMode is BIO)", dateOfBirth: "dateOfBirth if(searchMode is BIO)", number: "number if(searchMode is BIO)");
    print(response);
}
```
### Rwanda
```
// Rwanda National Identity verification
void verifyVoters() async {
    var response = await premblyPlugin.rwVerifyNationalID(number: "ID number");
    print(response);
}
```

### Full Example
```
import 'package:flutter/material.dart';
import 'package:prembly_flutter/prembly_flutter.dart';

void main() {
  // Initializing prembly plugin
  PremblyPlugin.initialize(
    appId: "YOUR_APP_ID_FROM_PREMBLY",
    apiKey: "YOUR_API_KEY_FROM_PREMBLY",
  ).then((_) {
    return runApp(const MyApp());
  });
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Prembly Example',
      theme: ThemeData(
        primarySwatch: Colors.purple,
      ),
      home: HomePage(),
      // home: RegisteredNumberScreen(),
    );
  }
}

class HomePage extends StatefulWidget {
  HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  // Instance of PremblyPlugin
  PremblyPlugin premblyPlugin = PremblyPlugin();

  // Loading state controller
  bool loading = false;

  // Field controllers
  final TextEditingController _emailController = TextEditingController();

  final TextEditingController _plateNumberController = TextEditingController();

  final TextEditingController _bvnNumberController = TextEditingController();

  final TextEditingController _internationalPassportController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Prembly Flutter Example'),
        elevation: 0,
      ),
      body: Padding(
        padding: const EdgeInsets.all(10.0),
        child: Column(
          children: [
            // Email verification
            TextFormField(
              controller: _emailController,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                contentPadding: const EdgeInsets.all(10),
                hintText: "Verify Email",
                suffixIcon: InkWell(
                  onTap: loading
                      ? null
                      : () async {
                          setState(() => loading = true);
                          var response = await premblyPlugin
                              .emailVerifier(_emailController.text);
                          print(response);

                          setState(() => loading = false);
                        }, //Email verifier handler
                  child: Container(
                    width: 80,
                    padding: const EdgeInsets.all(8.0),
                    child: Center(
                      child: loading
                          ? const SizedBox(
                              width: 20,
                              height: 20,
                              child: CircularProgressIndicator(),
                            )
                          : const Text(
                              'Send',
                              style: TextStyle(
                                color: Colors.blue,
                                fontSize: 12,
                                fontWeight: FontWeight.w500,
                              ),
                            ),
                    ),
                  ),
                ),
              ),
            ),

            // Country
            // Nigeria
            // Plate Number verification
            TextFormField(
              controller: _plateNumberController,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                contentPadding: const EdgeInsets.all(10),
                hintText: "Verify Plate Number",
                suffixIcon: InkWell(
                  onTap: loading
                      ? null
                      : () async {
                          setState(() => loading = true);
                          var response =
                              await premblyPlugin.ngPlateNumberVerifier(
                                  _plateNumberController.text);
                          print(response);

                          setState(() => loading = false);
                        }, //Plate Number verifier handler
                  child: Container(
                    width: 80,
                    padding: const EdgeInsets.all(8.0),
                    child: Center(
                      child: loading
                          ? const SizedBox(
                              width: 20,
                              height: 20,
                              child: CircularProgressIndicator(),
                            )
                          : const Text(
                              'Send',
                              style: TextStyle(
                                color: Colors.blue,
                                fontSize: 12,
                                fontWeight: FontWeight.w500,
                              ),
                            ),
                    ),
                  ),
                ),
              ),
            ),
            // Bank verification Number verification
            TextFormField(
              controller: _plateNumberController,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                contentPadding: const EdgeInsets.all(10),
                hintText: "Verify BVN Number",
                suffixIcon: InkWell(
                  onTap: loading
                      ? null
                      : () async {
                          setState(() => loading = true);
                          var response = await premblyPlugin
                              .ngBvnNumberVerifier(_bvnNumberController.text);
                          print(response);

                          setState(() => loading = false);
                        }, //BVN verifier handler
                  child: Container(
                    width: 80,
                    padding: const EdgeInsets.all(8.0),
                    child: Center(
                      child: loading
                          ? const SizedBox(
                              width: 20,
                              height: 20,
                              child: CircularProgressIndicator(),
                            )
                          : const Text(
                              'Send',
                              style: TextStyle(
                                color: Colors.blue,
                                fontSize: 12,
                                fontWeight: FontWeight.w500,
                              ),
                            ),
                    ),
                  ),
                ),
              ),
            ),
            // Ghana
            // International Passport verification
            TextFormField(
              controller: _plateNumberController,
              decoration: InputDecoration(
                filled: true,
                fillColor: Colors.white,
                contentPadding: const EdgeInsets.all(10),
                hintText: "Verify International Passport Number",
                suffixIcon: InkWell(
                  onTap: loading
                      ? null
                      : () async {
                          setState(() => loading = true);
                          var response = await premblyPlugin.
                              ghVerifyInternationalPassport(number: _internationalPassportController.text);
                          print(response);

                          setState(() => loading = false);
                        }, //BVN verifier handler
                  child: Container(
                    width: 80,
                    padding: const EdgeInsets.all(8.0),
                    child: Center(
                      child: loading
                          ? const SizedBox(
                              width: 20,
                              height: 20,
                              child: CircularProgressIndicator(),
                            )
                          : const Text(
                              'Send',
                              style: TextStyle(
                                color: Colors.blue,
                                fontSize: 12,
                                fontWeight: FontWeight.w500,
                              ),
                            ),
                    ),
                  ),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

```

Note: The above example are just to showcase some of the features of prembly_flutter, feel free to read more [documentation]() on [prembly-flutter.whitecoode.com](http://prembly-flutter.whitecoode.com).

## Author: [Whitecoode](https://whitecoode.com)
Follow me on
- Twitter [@whitecoode](https://twitter.com/whitecoode)
- Github [@whitecoode](https://github.com/whitecoode) or [@ibnyahyah](https://github.com/ibnyahyah)
## License: [MIT](https://github.com/Whitecoode/prembly_flutter/blob/master/LICENSE)