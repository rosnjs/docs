# Guide Développeur - Moteki Seller App

## Vue d'ensemble

Ce guide fournit toutes les informations nécessaires pour contribuer au développement de l'application Moteki Seller. Il couvre l'architecture, les conventions de code, les bonnes pratiques et les processus de développement.

## Table des Matières

1. [Prérequis et Installation](#prérequis-et-installation)
2. [Architecture de l'Application](#architecture-de-lapplication)
3. [Conventions de Code](#conventions-de-code)
4. [Structure du Projet](#structure-du-projet)
5. [Développement](#développement)
6. [Tests](#tests)
7. [Déploiement](#déploiement)
8. [Dépannage](#dépannage)
9. [Contribution](#contribution)

## Prérequis et Installation

### Prérequis

- **Flutter SDK** : Version 3.0.6 ou supérieure
- **Dart SDK** : Version 3.0.0 ou supérieure
- **Android Studio** ou **VS Code** avec extensions Flutter
- **Git** pour le contrôle de version
- **Firebase CLI** pour la configuration Firebase

### Installation

1. **Cloner le repository**
```bash
git clone https://github.com/your-org/moteki-seller-app.git
cd moteki-seller-app
```

2. **Installer les dépendances**
```bash
flutter pub get
```

3. **Configuration Firebase**
```bash
# Installer Firebase CLI
npm install -g firebase-tools

# Se connecter à Firebase
firebase login

# Initialiser Firebase
firebase init
```

4. **Configuration des fichiers de configuration**
- Copier `google-services.json` dans `android/app/`
- Copier `GoogleService-Info.plist` dans `ios/Runner/`
- Créer le fichier `.env` dans `assets/`

5. **Lancer l'application**
```bash
flutter run
```

## Architecture de l'Application

### Pattern MVC avec GetX

L'application suit le pattern Model-View-Controller avec GetX pour la gestion d'état :

```
lib/
├── core/
│   ├── controller/     # Controllers GetX (logique métier)
│   └── model/          # Modèles de données
├── config/
│   └── repository/     # Couche d'accès aux données
├── view/
│   ├── screen/         # Écrans UI
│   └── widget/         # Widgets réutilisables
├── network_dio/        # Couche HTTP
└── utils/              # Utilitaires
```

### Flux de Données

1. **View** → **Controller** (événements utilisateur)
2. **Controller** → **Repository** (requêtes données)
3. **Repository** → **NetworkHttps** (appels API)
4. **NetworkHttps** → **API Backend**
5. **Retour** : API → Model → Controller → View

### Gestion d'État

- **GetX Controllers** : Gestion de l'état réactive
- **Obx()** : Widgets réactifs
- **GetBuilder()** : Widgets avec contrôle manuel
- **RxList, RxBool, RxString** : Variables réactives

## Conventions de Code

### Nommage

#### Fichiers et Dossiers
```
# Fichiers
user_controller.dart          # snake_case
user_model.dart              # snake_case
user_screen.dart             # snake_case

# Dossiers
user_controller/             # snake_case
user_screen/                 # snake_case
```

#### Classes et Variables
```dart
// Classes - PascalCase
class UserController extends GetxController {}

// Variables - camelCase
String userName = '';
RxBool isLoading = false.obs;

// Constantes - UPPER_SNAKE_CASE
static const String API_BASE_URL = 'https://api.example.com';
```

#### Méthodes et Fonctions
```dart
// Méthodes - camelCase
void getUserData() {}
Future<void> loadData() async {}

// Fonctions privées - _camelCase
void _handleError() {}
```

### Structure des Controllers

```dart
class ExampleController extends GetxController {
  // Variables réactives
  RxList<DataModel> dataList = <DataModel>[].obs;
  RxBool isLoading = false.obs;
  RxString errorMessage = ''.obs;
  
  // Repository
  ExampleRepository repository = ExampleRepository();
  
  // Lifecycle
  @override
  void onInit() {
    super.onInit();
    // Initialisation
  }
  
  @override
  void onClose() {
    // Nettoyage
    super.onClose();
  }
  
  // Méthodes publiques
  Future<void> getData() async {
    // Logique métier
  }
}
```

### Structure des Modèles

```dart
class ExampleModel {
  int? status;
  String? message;
  ExampleData? data;
  
  ExampleModel({this.status, this.message, this.data});
  
  ExampleModel.fromJson(Map<String, dynamic> json) {
    status = json['status'];
    message = json['message'];
    data = json['data'] != null ? ExampleData.fromJson(json['data']) : null;
  }
  
  Map<String, dynamic> toJson() {
    final map = <String, dynamic>{};
    map['status'] = status;
    map['message'] = message;
    if (data != null) {
      map['data'] = data!.toJson();
    }
    return map;
  }
}
```

### Structure des Écrans

```dart
class ExampleScreen extends StatefulWidget {
  final String? parameter;
  
  const ExampleScreen({Key? key, this.parameter}) : super(key: key);
  
  @override
  State<ExampleScreen> createState() => _ExampleScreenState();
}

class _ExampleScreenState extends State<ExampleScreen> {
  ExampleController controller = Get.put(ExampleController());
  
  @override
  void initState() {
    super.initState();
    // Initialisation
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // UI
    );
  }
}
```

## Structure du Projet

### Organisation des Fichiers

```
lib/
├── core/
│   ├── controller/
│   │   ├── auth/                    # Authentification
│   │   ├── dashboard_manager_controller/
│   │   ├── home_controller/         # Dashboard
│   │   ├── product_controller/      # Produits
│   │   ├── order_controller/        # Commandes
│   │   ├── profile_controller/      # Profil
│   │   ├── setting_controller/      # Paramètres
│   │   └── optimized_controller_mixin.dart
│   └── model/
│       ├── dashboard_model.dart
│       ├── product_model.dart
│       ├── order_model.dart
│       └── ...
├── config/
│   └── repository/
│       ├── dashboard_repository.dart
│       ├── product_repository.dart
│       └── ...
├── view/
│   ├── screen/
│   │   ├── auth/
│   │   ├── dashboard_manager/
│   │   ├── home_screen/
│   │   │   └── widgets/             # Widgets spécifiques
│   │   ├── product_screen/
│   │   ├── order_screen/
│   │   └── ...
│   └── widget/
│       ├── common_button.dart
│       ├── common_text_field.dart
│       └── ...
├── network_dio/
│   ├── network_dio.dart
│   └── network_dio_optimized.dart
├── utils/
│   ├── base_api.dart
│   ├── colors.dart
│   ├── constant.dart
│   ├── helper.dart
│   ├── images.dart
│   ├── prefer.dart
│   ├── text_style.dart
│   ├── validator.dart
│   ├── secure_storage.dart
│   ├── input_sanitizer.dart
│   └── security_manager.dart
├── main.dart
└── store_go.dart
```

### Conventions de Dossiers

- **Controllers** : Un dossier par domaine fonctionnel
- **Models** : Un fichier par entité métier
- **Screens** : Un dossier par écran principal
- **Widgets** : Widgets réutilisables dans `view/widget/`
- **Utils** : Utilitaires communs dans `utils/`

## Développement

### Ajout d'une Nouvelle Fonctionnalité

1. **Créer le modèle de données**
```dart
// lib/core/model/new_feature_model.dart
class NewFeatureModel {
  // Structure du modèle
}
```

2. **Créer le repository**
```dart
// lib/config/repository/new_feature_repository.dart
class NewFeatureRepository {
  Future<dynamic> getData() async {
    // Appel API
  }
}
```

3. **Créer le controller**
```dart
// lib/core/controller/new_feature_controller.dart
class NewFeatureController extends GetxController {
  // Logique métier
}
```

4. **Créer l'écran**
```dart
// lib/view/screen/new_feature_screen.dart
class NewFeatureScreen extends StatelessWidget {
  // Interface utilisateur
}
```

### Ajout d'un Nouveau Widget

1. **Créer le widget**
```dart
// lib/view/widget/new_widget.dart
class NewWidget extends StatelessWidget {
  final String title;
  final Function()? onPressed;
  
  const NewWidget({
    Key? key,
    required this.title,
    this.onPressed,
  }) : super(key: key);
  
  @override
  Widget build(BuildContext context) {
    // Implémentation
  }
}
```

2. **Documenter le widget**
```dart
/// Widget personnalisé pour [description]
/// 
/// Exemple d'utilisation :
/// ```dart
/// NewWidget(
///   title: 'Mon titre',
///   onPressed: () => print('Action'),
/// )
/// ```
```

### Gestion des États

#### États de Chargement
```dart
// Controller
RxBool isLoading = false.obs;

Future<void> loadData() async {
  isLoading.value = true;
  try {
    // Chargement des données
  } finally {
    isLoading.value = false;
  }
}

// View
Obx(() => isLoading.value 
  ? LoadingWidget() 
  : DataWidget()
)
```

#### États d'Erreur
```dart
// Controller
RxString errorMessage = ''.obs;

void handleError(String error) {
  errorMessage.value = error;
  commonToast(error);
}

// View
Obx(() => errorMessage.value.isNotEmpty
  ? ErrorWidget(errorMessage.value)
  : ContentWidget()
)
```

### Navigation

#### Navigation Simple
```dart
// Navigation vers un écran
Get.to(() => ProductDetailScreen(productId: '123'));

// Navigation avec remplacement
Get.off(() => HomeScreen());

// Navigation avec suppression de l'historique
Get.offAll(() => LoginScreen());

// Retour
Get.back();
```

#### Navigation avec Paramètres
```dart
// Passage de paramètres
Get.to(() => ProductDetailScreen(
  productId: product.id.toString(),
  categoryId: product.categoryId.toString(),
));

// Récupération des paramètres
class ProductDetailScreen extends StatelessWidget {
  final String productId;
  final String categoryId;
  
  ProductDetailScreen({
    required this.productId,
    required this.categoryId,
  });
}
```

### Gestion des Données

#### Appels API
```dart
// Repository
class ProductRepository {
  Future<dynamic> getProductList({int page = 1}) async {
    return await NetworkHttps.getRequest(
      '${API.productListUrl}?page=$page'
    );
  }
}

// Controller
class ProductController extends GetxController {
  ProductRepository repository = ProductRepository();
  
  Future<void> getProductData(int page) async {
    try {
      var response = await repository.getProductList(page: page);
      if (response != null) {
        ProductModel model = ProductModel.fromJson(response);
        if (model.status == 1) {
          productList.value = model.data!.data!;
        }
      }
    } catch (e) {
      handleError('Error loading products: ${e.toString()}');
    }
  }
}
```

#### Pagination
```dart
// Controller avec pagination
class ProductController extends GetxController {
  RxInt currentPage = 1.obs;
  RxBool hasMoreData = true.obs;
  
  void loadMoreData() {
    if (hasMoreData.value) {
      currentPage.value++;
      getProductData(currentPage.value);
    }
  }
}

// View avec scroll listener
ScrollController scrollController = ScrollController();

scrollController.addListener(() {
  if (scrollController.position.pixels >= 
      scrollController.position.maxScrollExtent) {
    controller.loadMoreData();
  }
});
```

### Gestion des Erreurs

#### Gestion Centralisée
```dart
// Utils/error_handler.dart
class ErrorHandler {
  static void handleError(dynamic error) {
    if (error is SocketException) {
      commonToast('No Internet connection');
    } else if (error is HttpException) {
      commonToast('Server error occurred');
    } else {
      commonToast('An unexpected error occurred');
    }
  }
}
```

#### Gestion dans les Controllers
```dart
Future<void> getData() async {
  try {
    // Appel API
  } on SocketException catch (e) {
    handleError('No Internet connection');
  } on HttpException catch (e) {
    handleError('Server error: ${e.message}');
  } catch (e) {
    handleError('Unexpected error: ${e.toString()}');
  }
}
```

## Tests

### Structure des Tests

```
test/
├── unit/
│   ├── models/
│   ├── controllers/
│   ├── repositories/
│   └── utils/
├── widget/
└── integration/
```

### Tests Unitaires

#### Test de Modèle
```dart
// test/unit/models/product_model_test.dart
import 'package:flutter_test/flutter_test.dart';
import 'package:seller_app/core/model/product_model.dart';

void main() {
  group('ProductModel', () {
    test('should create ProductModel from JSON', () {
      // Arrange
      final json = {
        'status': 1,
        'message': 'Success',
        'data': {
          'id': 1,
          'name': 'Test Product',
        }
      };
      
      // Act
      final model = ProductModel.fromJson(json);
      
      // Assert
      expect(model.status, 1);
      expect(model.message, 'Success');
    });
  });
}
```

#### Test de Controller
```dart
// test/unit/controllers/product_controller_test.dart
import 'package:flutter_test/flutter_test.dart';
import 'package:get/get.dart';
import 'package:seller_app/core/controller/product_controller/product_controller.dart';

void main() {
  group('ProductController', () {
    late ProductController controller;
    
    setUp(() {
      controller = ProductController();
    });
    
    tearDown(() {
      Get.reset();
    });
    
    test('should initialize with empty product list', () {
      expect(controller.productList.length, 0);
    });
  });
}
```

### Tests Widget

```dart
// test/widget/common_button_test.dart
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:seller_app/view/widget/common_button.dart';

void main() {
  group('CommonButton', () {
    testWidgets('should display button with title', (WidgetTester tester) async {
      // Arrange
      const title = 'Test Button';
      
      // Act
      await tester.pumpWidget(
        MaterialApp(
          home: Scaffold(
            body: CommonButton(
              title: title,
              onPressed: () {},
            ),
          ),
        ),
      );
      
      // Assert
      expect(find.text(title), findsOneWidget);
    });
  });
}
```

### Tests d'Intégration

```dart
// test/integration/app_test.dart
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:seller_app/main.dart' as app;

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();
  
  group('App Integration Tests', () {
    testWidgets('should navigate to login screen', (WidgetTester tester) async {
      app.main();
      await tester.pumpAndSettle();
      
      expect(find.text('Log In'), findsOneWidget);
    });
  });
}
```

### Exécution des Tests

```bash
# Tests unitaires
flutter test

# Tests avec couverture
flutter test --coverage

# Tests d'intégration
flutter test integration_test/
```

## Déploiement

### Configuration de Build

#### Android
```gradle
// android/app/build.gradle
android {
    compileSdkVersion 34
    
    defaultConfig {
        applicationId "com.moteki.seller"
        minSdkVersion 21
        targetSdkVersion 34
        versionCode 1
        versionName "1.0.0"
    }
    
    buildTypes {
        release {
            signingConfig signingConfigs.release
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}
```

#### iOS
```xml
<!-- ios/Runner/Info.plist -->
<key>CFBundleShortVersionString</key>
<string>1.0.0</string>
<key>CFBundleVersion</key>
<string>1</string>
```

### Build de Production

#### Android APK
```bash
# Build APK
flutter build apk --release

# Build App Bundle
flutter build appbundle --release
```

#### iOS
```bash
# Build iOS
flutter build ios --release
```

### Configuration Firebase

#### Remote Config
```dart
// Configuration des valeurs par défaut
final FirebaseRemoteConfig remoteConfig = FirebaseRemoteConfig.instance;
await remoteConfig.setDefaults({
  'base_url': 'https://api.example.com',
  'is_demo_mode': false,
});
```

#### Analytics
```dart
// Événements personnalisés
FirebaseAnalytics.instance.logEvent(
  name: 'product_viewed',
  parameters: {
    'product_id': productId,
    'category': category,
  },
);
```

### Variables d'Environnement

#### Configuration .env
```env
# assets/.env
IS_DEMO_MODE=false
API_BASE_URL=https://api.moteki.com
```

#### Utilisation
```dart
import 'package:flutter_dotenv/flutter_dotenv.dart';

String baseUrl = dotenv.get('API_BASE_URL');
bool isDemoMode = dotenv.get('IS_DEMO_MODE') == 'true';
```

## Dépannage

### Problèmes Courants

#### Erreurs de Build
```bash
# Nettoyer le projet
flutter clean
flutter pub get

# Vérifier les dépendances
flutter pub deps
```

#### Erreurs de Navigation
```dart
// Vérifier que GetX est initialisé
GetMaterialApp(
  // Configuration
)

// Vérifier les routes
Get.to(() => ScreenName());
```

#### Erreurs de Réseau
```dart
// Vérifier la connectivité
try {
  final result = await InternetAddress.lookup('google.com');
  if (result.isNotEmpty && result[0].rawAddress.isNotEmpty) {
    // Internet disponible
  }
} catch (e) {
  // Pas d'internet
}
```

### Debug

#### Logs de Debug
```dart
// Activer les logs
import 'dart:developer' as developer;

developer.log('Debug message', name: 'MyApp');
```

#### Profiling
```bash
# Profiler l'application
flutter run --profile
```

### Performance

#### Optimisation des Images
```dart
// Utiliser cached_network_image
CachedNetworkImage(
  imageUrl: imageUrl,
  placeholder: (context, url) => CircularProgressIndicator(),
  errorWidget: (context, url, error) => Icon(Icons.error),
)
```

#### Optimisation des Listes
```dart
// Utiliser ListView.builder pour les grandes listes
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ListTile(title: Text(items[index]));
  },
)
```

## Contribution

### Workflow Git

1. **Fork du repository**
2. **Créer une branche feature**
```bash
git checkout -b feature/nouvelle-fonctionnalite
```

3. **Développer la fonctionnalité**
4. **Tester les modifications**
```bash
flutter test
flutter analyze
```

5. **Commit des modifications**
```bash
git add .
git commit -m "feat: ajouter nouvelle fonctionnalité"
```

6. **Push vers la branche**
```bash
git push origin feature/nouvelle-fonctionnalite
```

7. **Créer une Pull Request**

### Conventions de Commit

```
feat: nouvelle fonctionnalité
fix: correction de bug
docs: documentation
style: formatage
refactor: refactorisation
test: tests
chore: tâches de maintenance
```

### Code Review

#### Checklist
- [ ] Code respecte les conventions
- [ ] Tests passent
- [ ] Documentation mise à jour
- [ ] Pas de code dupliqué
- [ ] Gestion d'erreurs appropriée
- [ ] Performance optimisée

#### Bonnes Pratiques
- Écrire du code lisible et maintenable
- Ajouter des commentaires pour la logique complexe
- Tester les modifications
- Documenter les nouvelles fonctionnalités
- Respecter l'architecture existante

### Documentation

#### Documentation du Code
```dart
/// Calcule le prix total avec les taxes
/// 
/// [basePrice] Le prix de base
/// [taxRate] Le taux de taxe en pourcentage
/// 
/// Retourne le prix total incluant les taxes
double calculateTotalPrice(double basePrice, double taxRate) {
  return basePrice * (1 + taxRate / 100);
}
```

#### Documentation des API
```dart
/// Repository pour la gestion des produits
/// 
/// Fournit des méthodes pour interagir avec l'API des produits
class ProductRepository {
  /// Récupère la liste des produits
  /// 
  /// [page] Numéro de page pour la pagination
  /// 
  /// Retourne une liste paginée des produits
  Future<List<Product>> getProducts({int page = 1}) async {
    // Implémentation
  }
}
```

---

Ce guide fournit toutes les informations nécessaires pour contribuer efficacement au développement de l'application Moteki Seller. Pour plus de détails, consultez la documentation spécifique dans chaque section du projet.
