# Documentation des Modèles de Données - Moteki Seller App

## Vue d'ensemble

Cette documentation décrit tous les modèles de données utilisés dans l'application Moteki Seller. Chaque modèle suit le pattern standard avec des méthodes `fromJson()` et `toJson()` pour la sérialisation/désérialisation JSON.

## Structure Générale des Modèles

Tous les modèles suivent cette structure :

```dart
class ModelName {
  int? status;           // Statut de la réponse (1 = succès, 0 = erreur)
  String? message;       // Message de la réponse
  ModelData? data;       // Données principales
  
  // Constructeurs et méthodes de sérialisation
  ModelName.fromJson(Map<String, dynamic> json);
  Map<String, dynamic> toJson();
}
```

## Modèles Principaux

### 1. DashboardModel

**Fichier** : `lib/core/model/dashboard_model.dart`

**Description** : Modèle principal pour les données du tableau de bord

```dart
class DashboardModel {
  int? status;
  String? message;
  DashboardData? data;
}
```

**Structure DashboardData** :
```json
{
  "user": {
    "id": 1,
    "name": "Admin User",
    "email": "admin@example.com",
    "image": "user.jpg"
  },
  "store": [
    {
      "id": 1,
      "name": "My Store"
    }
  ],
  "qr-code": {
    "name": "My Store",
    "url": "https://example.com/qr"
  },
  "products": 25,
  "sales": 1500.00,
  "order": 45,
  "product": [...], // Liste des produits
  "recent_order": [...], // Commandes récentes
  "coupons": [...], // Coupons disponibles
  "orderchart": [...], // Graphique des commandes
  "visitorchart": [...] // Graphique des visiteurs
}
```

**Classes associées** :
- `User` : Informations utilisateur
- `Store` : Informations boutique
- `QrCode` : Données QR code
- `ProductData` : Produits (voir ProductModel)
- `RecentOrder` : Commandes récentes
- `Coupons` : Coupons de réduction
- `Orderchart` : Données graphique commandes
- `Visitorchart` : Données graphique visiteurs

### 2. ProductModel

**Fichier** : `lib/core/model/product_model.dart`

**Description** : Modèle pour la gestion des produits avec pagination

```dart
class ProductModel {
  int? status;
  String? message;
  ProductModelData? data;
}
```

**Structure ProductModelData** :
```json
{
  "current_page": 1,
  "data": [
    {
      "id": 1,
      "name": "Product Name",
      "categoryId": 1,
      "categoryName": "Electronics",
      "finalPrice": "29.99",
      "discountPrice": "24.99",
      "productStock": 10,
      "coverImagePath": "product.jpg",
      "description": "Product description",
      "trending": 1,
      "variantAttribute": "Size: M, Color: Red",
      "tag": "new,popular",
      "retuenText": "Tax info",
      "otherDescriptionArray": [
        {
          "description": "Additional info 1"
        },
        {
          "description": "Additional info 2"
        }
      ]
    }
  ],
  "first_page_url": "https://api.example.com/products?page=1",
  "from": 1,
  "last_page": 5,
  "last_page_url": "https://api.example.com/products?page=5",
  "links": [...],
  "next_page_url": "https://api.example.com/products?page=2",
  "path": "https://api.example.com/products",
  "per_page": 10,
  "prev_page_url": null,
  "to": 10,
  "total": 50
}
```

**Classes associées** :
- `ProductData` : Données produit individuelles
- `Links` : Liens de pagination
- `OtherDescriptionArray` : Descriptions supplémentaires

### 3. OrderModel

**Fichier** : `lib/core/model/order_model.dart`

**Description** : Modèle pour la gestion des commandes

```dart
class OrderModel {
  int? status;
  String? message;
  OrderModelData? data;
}
```

**Structure OrderData** :
```json
{
  "id": 1,
  "productOrderId": "ORD-001",
  "orderDate": "2024-01-15",
  "userId": 123,
  "isGuest": 0,
  "productJson": "{\"products\":[...]}",
  "productId": "1,2,3",
  "productName": "Product 1, Product 2",
  "productPrice": "29.99,19.99",
  "productQuantity": "2,1",
  "productImage": "image1.jpg,image2.jpg",
  "userName": "Customer Name",
  "userEmail": "customer@example.com",
  "userPhone": "+1234567890",
  "deliveryAddress": "123 Main St, City, State",
  "deliveryStatus": "pending",
  "paymentStatus": "paid",
  "finalPrice": "59.98",
  "shippingPrice": "5.99",
  "taxPrice": "4.80",
  "couponCode": "SUMMER20",
  "couponDiscount": "10.00",
  "paymentMethod": "credit_card",
  "transactionId": "txn_123456789"
}
```

**Classes associées** :
- `OrderData` : Données commande individuelles
- `OrderModelData` : Structure avec pagination

### 4. CategoriesModel

**Fichier** : `lib/core/model/categories_model.dart`

**Description** : Modèle pour la gestion des catégories

```dart
class CategoriesModel {
  int? status;
  String? message;
  CategoriesModelData? data;
}
```

**Structure CategoryData** :
```json
{
  "id": 1,
  "name": "Electronics",
  "description": "Electronic products and gadgets",
  "image": "electronics.jpg",
  "product_count": 25,
  "is_active": 1,
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-15T10:30:00Z"
}
```

### 5. CouponModel

**Fichier** : `lib/core/model/coupon_model.dart`

**Description** : Modèle pour la gestion des coupons

```dart
class CouponModel {
  int? status;
  String? message;
  CouponModelData? data;
}
```

**Structure CouponData** :
```json
{
  "id": 1,
  "couponName": "Summer Sale",
  "couponCode": "SUMMER20",
  "discountAmount": 20,
  "couponType": "percentage",
  "validFrom": "2024-01-01",
  "validTo": "2024-12-31",
  "usageLimit": 100,
  "usedCount": 25,
  "minimumAmount": 50.00,
  "maximumDiscount": 100.00,
  "isActive": 1,
  "created_at": "2024-01-01T00:00:00Z"
}
```

**Types de coupons** :
- `percentage` : Réduction en pourcentage
- `fixed` : Réduction fixe en montant

### 6. ShippingModel

**Fichier** : `lib/core/model/shipping_model.dart`

**Description** : Modèle pour les options de livraison

```dart
class ShippingModel {
  int? status;
  String? message;
  ShippingModelData? data;
}
```

**Structure ShippingData** :
```json
{
  "id": 1,
  "name": "Standard Shipping",
  "price": 5.99,
  "deliveryDays": "3-5",
  "description": "Standard delivery within 3-5 business days",
  "isActive": 1,
  "freeShippingThreshold": 50.00,
  "weightLimit": 5.0,
  "created_at": "2024-01-01T00:00:00Z"
}
```

### 7. TaxModel

**Fichier** : `lib/core/model/tax_model.dart`

**Description** : Modèle pour les taxes

```dart
class TaxModel {
  int? status;
  String? message;
  TaxModelData? data;
}
```

**Structure Tax** :
```json
{
  "id": 1,
  "name": "VAT",
  "rate": 20.0,
  "type": "percentage",
  "description": "Value Added Tax",
  "isActive": 1,
  "appliesTo": "all",
  "created_at": "2024-01-01T00:00:00Z"
}
```

**Types de taxes** :
- `percentage` : Taxe en pourcentage
- `fixed` : Taxe fixe

### 8. StaticsDataModel

**Fichier** : `lib/core/model/static_model.dart`

**Description** : Modèle pour les statistiques et analytics

```dart
class StaticsDataModel {
  int? status;
  String? message;
  StaticData? data;
}
```

**Structure StaticData** :
```json
{
  "visitorchart": [
    {
      "date": "2024-01-01",
      "visitors": 25,
      "page_views": 100
    }
  ],
  "topurl": [
    {
      "url": "/products/electronics",
      "visits": 150,
      "percentage": 30.5
    }
  ],
  "platform": [
    {
      "name": "Android",
      "visitors": 60,
      "percentage": 40.0
    },
    {
      "name": "iOS",
      "visitors": 40,
      "percentage": 26.7
    }
  ],
  "browser": [
    {
      "name": "Chrome",
      "visitors": 80,
      "percentage": 53.3
    }
  ],
  "device": [
    {
      "name": "Mobile",
      "visitors": 90,
      "percentage": 60.0
    }
  ]
}
```

**Classes associées** :
- `VisitorChartData` : Données graphique visiteurs
- `TopUrl` : URLs les plus visitées
- `PlatformData` : Données par plateforme
- `BrowserData` : Données par navigateur
- `DeviceData` : Données par appareil

## Modèles de Configuration

### 9. EmailSettingModel

**Fichier** : `lib/core/model/email_setting_model.dart`

**Description** : Configuration des paramètres email

```json
{
  "smtp_host": "smtp.gmail.com",
  "smtp_port": 587,
  "smtp_username": "email@example.com",
  "smtp_password": "encrypted_password",
  "from_email": "noreply@example.com",
  "from_name": "Moteki Store",
  "is_active": 1
}
```

### 10. ImageBaseUrlModel

**Fichier** : `lib/core/model/image_base_url_model.dart`

**Description** : Configuration des URLs d'images

```json
{
  "image_url": "https://api.example.com/images/",
  "payment_url": "https://api.example.com/payments/",
  "cdn_url": "https://cdn.example.com/"
}
```

## Modèles de Révision

### 11. ReviewModel

**Fichier** : `lib/core/model/review_model.dart`

**Description** : Modèle pour les avis produits

```json
{
  "id": 1,
  "productId": 123,
  "userId": 456,
  "userName": "Customer Name",
  "rating": 5,
  "comment": "Excellent product!",
  "isApproved": 1,
  "created_at": "2024-01-15T10:30:00Z"
}
```

## Modèles de Pagination

### Structure Links

Tous les modèles avec pagination utilisent cette structure :

```dart
class Links {
  String? url;
  String? label;
  bool? active;
}
```

**Exemple JSON** :
```json
{
  "url": "https://api.example.com/products?page=2",
  "label": "2",
  "active": false
}
```

## Modèles de Réponse Standard

### Structure de Réponse API

Tous les endpoints retournent cette structure :

```json
{
  "status": 1,                    // 1 = succès, 0 = erreur
  "message": "Success message",    // Message descriptif
  "data": {                       // Données spécifiques
    // Contenu variable selon l'endpoint
  }
}
```

### Gestion des Erreurs

```json
{
  "status": 0,
  "message": "Error occurred",
  "data": {
    "message": "Detailed error description",
    "code": "ERROR_CODE",
    "field": "field_name"  // Si erreur de validation
  }
}
```

## Utilisation dans les Controllers

### Pattern GetX

```dart
class ExampleController extends GetxController {
  // Variables réactives
  RxList<ProductData> productList = <ProductData>[].obs;
  RxBool isLoading = false.obs;
  
  // Repository
  ProductRepository repository = ProductRepository();
  
  // Méthode de récupération des données
  Future<void> getProducts() async {
    isLoading.value = true;
    try {
      var response = await repository.getProductList();
      if (response != null) {
        ProductModel model = ProductModel.fromJson(response);
        if (model.status == 1) {
          productList.value = model.data!.data!;
        }
      }
    } catch (e) {
      // Gestion d'erreur
    } finally {
      isLoading.value = false;
    }
  }
}
```

## Validation des Données

### Validation Côté Client

```dart
// Exemple de validation pour un produit
bool validateProduct(ProductData product) {
  if (product.name == null || product.name!.isEmpty) {
    return false;
  }
  if (product.finalPrice == null || double.tryParse(product.finalPrice!) == null) {
    return false;
  }
  return true;
}
```

### Validation Côté Serveur

Les modèles incluent des champs de validation :
- `required` : Champs obligatoires
- `format` : Format des données (email, URL, etc.)
- `range` : Valeurs min/max
- `length` : Longueur des chaînes

## Sérialisation/Désérialisation

### Méthodes Standard

```dart
// Désérialisation depuis JSON
ProductModel model = ProductModel.fromJson(jsonData);

// Sérialisation vers JSON
Map<String, dynamic> json = model.toJson();

// Utilisation avec GetX
RxList<ProductData> products = <ProductData>[].obs;
products.value = model.data!.data!;
```

### Gestion des Null Safety

Tous les modèles utilisent la null safety de Dart :
- `int?` : Entiers optionnels
- `String?` : Chaînes optionnelles
- `List<Type>?` : Listes optionnelles
- `Type?` : Objets optionnels

## Performance et Optimisation

### Lazy Loading

```dart
// Chargement paresseux des images
CachedNetworkImage(
  imageUrl: "${imageBaseUrl}${product.coverImagePath}",
  placeholder: (context, url) => CircularProgressIndicator(),
  errorWidget: (context, url, error) => Icon(Icons.error),
)
```

### Pagination

```dart
// Gestion de la pagination
ScrollController scrollController = ScrollController();

scrollController.addListener(() {
  if (scrollController.position.pixels == 
      scrollController.position.maxScrollExtent) {
    // Charger la page suivante
    loadNextPage();
  }
});
```

---

Cette documentation couvre tous les modèles de données utilisés dans l'application Moteki Seller. Pour plus de détails sur l'implémentation, consultez les fichiers source dans `lib/core/model/`.
