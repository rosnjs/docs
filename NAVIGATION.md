# Navigation et Flux Utilisateur - Moteki Seller App

## Vue d'ensemble

L'application Moteki Seller utilise une architecture de navigation basée sur GetX avec une structure de navigation principale à 5 onglets et des écrans secondaires pour les fonctionnalités détaillées.

## Architecture de Navigation

### Structure Principale

L'application suit cette hiérarchie de navigation :

```
WelcomeScreen (Première installation)
    ↓
LoginScreen (Authentification)
    ↓
DashBoardManagerScreen (Navigation principale - 5 onglets)
    ├── HomeScreen (Dashboard)
    ├── OrderScreen (Commandes)
    ├── ProductsScreen (Produits)
    ├── CategoriesScreen (Catégories)
    └── SettingScreen (Paramètres)
```

## Diagramme de Navigation Principal

```mermaid
graph TD
    A[WelcomeScreen] --> B[LoginScreen]
    B --> C[DashBoardManagerScreen]
    
    C --> D[HomeScreen - Dashboard]
    C --> E[OrderScreen - Commandes]
    C --> F[ProductsScreen - Produits]
    C --> G[CategoriesScreen - Catégories]
    C --> H[SettingScreen - Paramètres]
    
    D --> D1[StatisticsScreen]
    D --> D2[ProductDetailScreen]
    D --> D3[OrderDetailScreen]
    D --> D4[QuickAdd - Modal]
    
    E --> E1[OrderDetailScreen]
    E1 --> E2[InvoicePDFView]
    
    F --> F1[AddNewProductScreen]
    F --> F2[ProductDetailScreen]
    F --> F3[AddRatingScreen]
    F --> F4[AddVariantScreen]
    
    G --> G1[AddCategoryBottomSheet]
    
    H --> H1[StoreSettingScreen]
    H --> H2[StoreThemeSettingScreen]
    H --> H3[PaymentSettingScreen]
    H --> H4[EmailSettingScreen]
    H --> H5[LoyaltyProgramScreen]
    
    H3 --> H3A[CODScreen]
    H3 --> H3B[BankTransferScreen]
    H3 --> H3C[StripeScreen]
```

## Navigation Bottom Tab

### Structure des Onglets

L'application utilise une navigation bottom custom avec 5 onglets :

```dart
class DashboardManagerController extends GetxController {
  RxInt currantIndex = 2.obs; // Dashboard par défaut
  RxList naviBarItemList = [
    {'icon': ordersIcon, 'title': 'Orders', 'screen': OrderScreen()},
    {'icon': productsIcon, 'title': 'Products', 'screen': ProductsScreen()},
    {'icon': dashboardIcon, 'title': 'Dashboard', 'screen': HomeScreen()},
    {'icon': categoriesIcon, 'title': 'Categories', 'screen': CategoriesScreen()},
    {'icon': settingsIcon, 'title': 'Settings', 'screen': SettingScreen()},
  ].obs;
}
```

### Index de Navigation

- **Index 0** : Orders (Commandes)
- **Index 1** : Products (Produits)
- **Index 2** : Dashboard (Tableau de bord) - **Par défaut**
- **Index 3** : Categories (Catégories)
- **Index 4** : Settings (Paramètres)

## Flux de Navigation Détaillé

### 1. Flux d'Authentification

```mermaid
sequenceDiagram
    participant U as User
    participant W as WelcomeScreen
    participant L as LoginScreen
    participant A as AuthController
    participant D as DashBoardManagerScreen

    U->>W: Lance l'app
    W->>L: Première installation
    U->>L: Saisit credentials
    L->>A: loginAuth(email, password)
    A->>A: Validation
    A->>A: Appel API /adminlogin
    A->>A: Stockage token
    A->>D: Navigation vers dashboard
    D->>U: Affichage interface principale
```

### 2. Flux Dashboard Principal

```mermaid
graph TD
    A[DashBoardManagerScreen] --> B[HomeScreen - Dashboard]
    
    B --> B1[Profile Section]
    B --> B2[Store Dropdown]
    B --> B3[Quick Add Section]
    B --> B4[Statistics Section]
    B --> B5[QR Code Widget]
    B --> B6[Total Products Widget]
    B --> B7[Total Sales Widget]
    B --> B8[Total Orders Widget]
    B --> B9[Orders Graph]
    B --> B10[Top Products List]
    B --> B11[Recent Orders List]
    B --> B12[Visitors Chart]
    B --> B13[Product Coupons List]
    
    B3 --> B3A[Add New Product]
    B3 --> B3B[Add New Category]
    B3 --> B3C[Add New Coupon]
    
    B4 --> B4A[StatisticsScreen]
    B10 --> B10A[ProductDetailScreen]
    B11 --> B11A[OrderDetailScreen]
    B13 --> B13A[CouponDetailScreen]
```

### 3. Flux Gestion Produits

```mermaid
graph TD
    A[ProductsScreen] --> B[Liste Produits]
    B --> C[ProductDetailScreen]
    B --> D[AddNewProductScreen]
    
    C --> C1[View Product Details]
    C --> C2[Edit Product]
    C --> C3[Delete Product]
    C --> C4[Add Rating]
    
    D --> D1[Create Product]
    D --> D2[Update Product]
    D --> D3[Add Variants]
    D --> D4[Upload Images]
    
    D --> D5[AddVariantScreen]
    C --> C5[AddRatingScreen]
```

### 4. Flux Gestion Commandes

```mermaid
graph TD
    A[OrderScreen] --> B[Liste Commandes]
    B --> C[OrderDetailScreen]
    
    C --> C1[View Order Details]
    C --> C2[Update Order Status]
    C --> C3[Delete Order]
    C --> C4[Generate Invoice]
    
    C4 --> D[InvoicePDFView]
    D --> D1[View PDF]
    D --> D2[Print PDF]
    D --> D3[Share PDF]
```

### 5. Flux Gestion Catégories

```mermaid
graph TD
    A[CategoriesScreen] --> B[Liste Catégories]
    B --> C[AddCategoryBottomSheet]
    
    C --> C1[Create Category]
    C --> C2[Update Category]
    C --> C3[Delete Category]
    C --> C4[Upload Category Image]
```

### 6. Flux Paramètres

```mermaid
graph TD
    A[SettingScreen] --> B[Store Settings]
    A --> C[Store Theme Settings]
    A --> D[Payment Settings]
    A --> E[Email Settings]
    A --> F[Loyalty Program]
    A --> G[Logout]
    
    B --> B1[StoreSettingScreen]
    C --> C1[StoreThemeSettingScreen]
    D --> D1[PaymentSettingScreen]
    D1 --> D1A[CODScreen]
    D1 --> D1B[BankTransferScreen]
    D1 --> D1C[StripeScreen]
    E --> E1[EmailSettingScreen]
    F --> F1[LoyaltyProgramScreen]
```

## Navigation GetX

### Méthodes de Navigation

```dart
// Navigation simple
Get.to(() => ProductDetailScreen(productId: "123"));

// Navigation avec remplacement
Get.off(() => HomeScreen());

// Navigation avec suppression de l'historique
Get.offAll(() => LoginScreen());

// Retour
Get.back();

// Navigation avec paramètres
Get.toNamed('/product-detail', arguments: {'productId': '123'});
```

### Gestion des Paramètres

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

## Navigation Conditionnelle

### Authentification

```dart
// Vérification du token
String accessToken = await Prefs.getToken();
if (accessToken.isNotEmpty) {
  return DashBoardManagerScreen();
} else {
  return NormalLoginWidget();
}
```

### Mode Démo

```dart
// Vérification du mode démo
if (Prefs.getBool(AppConstant.isDemoMode) == true) {
  commonToast(AppConstant.demoString);
  return;
}
```

## Navigation avec Bottom Sheets

### Modal Bottom Sheets

```dart
// Ajout de catégorie
showModalBottomSheet(
  context: context,
  backgroundColor: AppColor.cBackGround,
  barrierColor: AppColor.cGreyOpacity,
  isScrollControlled: true,
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.only(
      topLeft: Radius.circular(30),
      topRight: Radius.circular(30),
    ),
  ),
  builder: (context) {
    return AddNewCategoriesWidget(isUpdate: false);
  },
);
```

### Bottom Sheets Disponibles

- `AddNewCategoriesWidget` - Ajout/Modification catégorie
- `AddNewCouponWidget` - Ajout/Modification coupon
- `AddShippingBottomSheet` - Ajout option livraison
- `AddTaxBottomSheet` - Ajout taxe

## Navigation avec AppBar

### AppBar Standard

```dart
AppBar simpleAppBar({
  required bool isBack,
  required String title,
  String? date,
}) {
  return AppBar(
    backgroundColor: AppColor.cBackGround,
    elevation: 0,
    leading: isBack 
      ? IconButton(
          icon: Icon(Icons.arrow_back, color: AppColor.cLabel),
          onPressed: () => Get.back(),
        )
      : null,
    title: Text(title, style: pRegular20),
    actions: date != null ? [
      Text(date, style: pRegular12),
      SizedBox(width: 16),
    ] : null,
  );
}
```

### AppBar avec Actions

```dart
AppBar appBarWithActions({
  required String title,
  required List<Widget> actions,
}) {
  return AppBar(
    backgroundColor: AppColor.cBackGround,
    title: Text(title),
    actions: actions,
  );
}
```

## Gestion des États de Navigation

### États de Chargement

```dart
// État de chargement global
Obx(() => homeController.isDataAvailable.value 
  ? LoadingWidget() 
  : MainContent()
)
```

### États d'Erreur

```dart
// Gestion des erreurs de navigation
try {
  await Get.to(() => ProductDetailScreen());
} catch (e) {
  commonToast("Navigation error: ${e.toString()}");
}
```

## Navigation avec Deep Links

### Configuration Deep Links

```dart
// Android - android/app/src/main/AndroidManifest.xml
<intent-filter android:autoVerify="true">
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data android:scheme="https" android:host="moteki.app" />
</intent-filter>

// iOS - ios/Runner/Info.plist
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLName</key>
    <string>moteki.app</string>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>https</string>
    </array>
  </dict>
</array>
```

### Gestion des Deep Links

```dart
// Gestion des liens profonds
void handleDeepLink(String link) {
  if (link.contains('/product/')) {
    String productId = link.split('/product/')[1];
    Get.to(() => ProductDetailScreen(productId: productId));
  } else if (link.contains('/order/')) {
    String orderId = link.split('/order/')[1];
    Get.to(() => OrderDetailScreen(orderId: orderId));
  }
}
```

## Navigation avec Animations

### Transitions Personnalisées

```dart
// Transition personnalisée
Get.to(
  () => ProductDetailScreen(),
  transition: Transition.fadeIn,
  duration: Duration(milliseconds: 300),
  curve: Curves.easeInOut,
);
```

### Types de Transitions Disponibles

- `Transition.fadeIn` - Fondu d'entrée
- `Transition.slideInRight` - Glissement depuis la droite
- `Transition.slideInLeft` - Glissement depuis la gauche
- `Transition.slideInUp` - Glissement depuis le bas
- `Transition.zoom` - Zoom
- `Transition.cupertino` - Style iOS

## Navigation avec Guards

### Guards d'Authentification

```dart
// Middleware d'authentification
class AuthMiddleware extends GetMiddleware {
  @override
  RouteSettings? redirect(String? route) {
    String token = Prefs.getToken();
    if (token.isEmpty) {
      return RouteSettings(name: '/login');
    }
    return null;
  }
}
```

### Guards de Permissions

```dart
// Middleware de permissions
class PermissionMiddleware extends GetMiddleware {
  @override
  RouteSettings? redirect(String? route) {
    if (route == '/admin' && !isAdmin()) {
      return RouteSettings(name: '/dashboard');
    }
    return null;
  }
}
```

## Navigation avec Historique

### Gestion de l'Historique

```dart
// Sauvegarde de l'état de navigation
class NavigationController extends GetxController {
  RxList<String> navigationHistory = <String>[].obs;
  
  void addToHistory(String route) {
    navigationHistory.add(route);
  }
  
  void goBack() {
    if (navigationHistory.isNotEmpty) {
      navigationHistory.removeLast();
      Get.back();
    }
  }
}
```

### Navigation avec Historique Personnalisé

```dart
// Navigation avec historique
void navigateWithHistory(String route) {
  navigationController.addToHistory(route);
  Get.toNamed(route);
}
```

## Performance de Navigation

### Optimisations

```dart
// Lazy loading des écrans
class LazyScreen extends StatelessWidget {
  final Widget Function() builder;
  
  LazyScreen({required this.builder});
  
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      future: Future.delayed(Duration.zero),
      builder: (context, snapshot) {
        return builder();
      },
    );
  }
}
```

### Préchargement des Écrans

```dart
// Préchargement des écrans fréquents
class ScreenPreloader {
  static void preloadScreens() {
    // Précharger les écrans principaux
    Get.lazyPut(() => ProductController());
    Get.lazyPut(() => OrderController());
    Get.lazyPut(() => CategoryController());
  }
}
```

---

Cette documentation couvre tous les aspects de la navigation dans l'application Moteki Seller. Pour plus de détails sur l'implémentation, consultez les fichiers source dans `lib/view/screen/` et `lib/core/controller/`.
