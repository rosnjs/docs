# Documentation API - Moteki Seller App

## Vue d'ensemble

L'API Moteki Seller utilise une architecture REST avec authentification Bearer Token. La base URL est configurée dynamiquement via Firebase Remote Config.

### Configuration

- **Base URL** : Configurée via Firebase Remote Config (`base_url`)
- **Authentification** : Bearer Token dans header `Authorization`
- **Content-Type** : `application/json`
- **Cache Control** : `no-cache`

### Headers Requis

```http
Authorization: Bearer {token}
Content-Type: application/json
Cache-Control: no-cache
```

## Endpoints d'Authentification

### POST /adminlogin

**Description** : Authentification de l'administrateur/vendeur

**Request Body** :
```json
{
  "email": "admin@example.com",
  "password": "password123"
}
```

**Response Success (200)** :
```json
{
  "status": 1,
  "message": "Login successful",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": 1,
      "name": "Admin User",
      "email": "admin@example.com",
      "image": "user.jpg"
    }
  }
}
```

**Response Error (401)** :
```json
{
  "status": 0,
  "message": "Invalid credentials",
  "data": {
    "message": "Email or password is incorrect"
  }
}
```

## Endpoints Dashboard

### POST /dashboard

**Description** : Récupère les données du tableau de bord

**Request Body** :
```json
{}
```

**Response (200)** :
```json
{
  "status": 1,
  "message": "Dashboard data retrieved",
  "data": {
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
    "product": [
      {
        "id": 1,
        "name": "Product Name",
        "categoryName": "Category",
        "finalPrice": "29.99",
        "productStock": 10,
        "coverImagePath": "product.jpg"
      }
    ],
    "recent_order": [
      {
        "id": 1,
        "productOrderId": "ORD-001",
        "userName": "Customer Name",
        "orderDate": "2024-01-15",
        "finalPrice": "59.98",
        "deliveryStatus": "pending"
      }
    ],
    "coupons": [
      {
        "id": 1,
        "couponName": "SUMMER20",
        "couponCode": "SUMMER20",
        "discountAmount": 20,
        "couponType": "percentage"
      }
    ],
    "orderchart": [
      {
        "date": "2024-01-01",
        "orders": 5
      }
    ],
    "visitorchart": [
      {
        "date": "2024-01-01",
        "visitors": 25
      }
    ]
  }
}
```

### GET /base_url

**Description** : Récupère l'URL de base pour les images

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "image_url": "https://api.example.com/images/",
    "payment_url": "https://api.example.com/payments/"
  }
}
```

### POST /changestore

**Description** : Change le store actuel

**Request Body** :
```json
{
  "store_id": "1"
}
```

**Response (200)** :
```json
{
  "status": 1,
  "message": "Store changed successfully",
  "data": {
    "message": "Store updated"
  }
}
```

## Endpoints Produits

### GET /productlist?page=1

**Description** : Liste paginée des produits

**Query Parameters** :
- `page` : Numéro de page (défaut: 1)

**Response (200)** :
```json
{
  "status": 1,
  "message": "Products retrieved",
  "data": {
    "products": [
      {
        "id": 1,
        "name": "Product Name",
        "categoryId": 1,
        "categoryName": "Category",
        "finalPrice": "29.99",
        "discountPrice": "24.99",
        "productStock": 10,
        "coverImagePath": "product.jpg",
        "description": "Product description",
        "trending": 1,
        "variantAttribute": "Size: M, Color: Red",
        "tag": "new,popular",
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
    "pagination": {
      "current_page": 1,
      "total_pages": 5,
      "total_items": 50
    }
  }
}
```

### POST /createproduct

**Description** : Crée un nouveau produit

**Request Body** :
```json
{
  "name": "New Product",
  "category_id": 1,
  "price": "29.99",
  "discount_price": "24.99",
  "stock": 10,
  "description": "Product description",
  "images": ["image1.jpg", "image2.jpg"],
  "trending": 1,
  "tag": "new,popular"
}
```

**Response (200)** :
```json
{
  "status": 1,
  "message": "Product created successfully",
  "data": {
    "product_id": 123,
    "message": "Product added"
  }
}
```

### POST /updateproduct

**Description** : Met à jour un produit existant

**Request Body** :
```json
{
  "product_id": 123,
  "name": "Updated Product",
  "category_id": 1,
  "price": "35.99",
  "discount_price": "30.99",
  "stock": 15,
  "description": "Updated description"
}
```

### POST /deleteproduct

**Description** : Supprime un produit

**Request Body** :
```json
{
  "product_id": 123
}
```

**Response (200)** :
```json
{
  "status": 1,
  "message": "Product deleted successfully"
}
```

### GET /viewproduct?product_id=123

**Description** : Détails d'un produit spécifique

**Query Parameters** :
- `product_id` : ID du produit

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "product": {
      "id": 123,
      "name": "Product Name",
      "categoryName": "Category",
      "finalPrice": "29.99",
      "productStock": 10,
      "coverImagePath": "product.jpg",
      "description": "Product description",
      "images": ["image1.jpg", "image2.jpg"],
      "variants": [
        {
          "attribute": "Size",
          "value": "M"
        }
      ]
    }
  }
}
```

### POST /searchproduct

**Description** : Recherche de produits

**Request Body** :
```json
{
  "search_term": "product name",
  "page": 1
}
```

## Endpoints Commandes

### GET /orderlist?page=1

**Description** : Liste paginée des commandes

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "orders": [
      {
        "id": 1,
        "productOrderId": "ORD-001",
        "userName": "Customer Name",
        "userEmail": "customer@example.com",
        "orderDate": "2024-01-15",
        "finalPrice": "59.98",
        "deliveryStatus": "pending",
        "paymentStatus": "paid",
        "products": [
          {
            "name": "Product Name",
            "quantity": 2,
            "price": "29.99"
          }
        ]
      }
    ]
  }
}
```

### GET /vieworder?order_id=1

**Description** : Détails d'une commande

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "order": {
      "id": 1,
      "productOrderId": "ORD-001",
      "userName": "Customer Name",
      "userEmail": "customer@example.com",
      "userPhone": "+1234567890",
      "orderDate": "2024-01-15",
      "deliveryDate": "2024-01-20",
      "finalPrice": "59.98",
      "deliveryStatus": "pending",
      "paymentStatus": "paid",
      "shippingAddress": {
        "street": "123 Main St",
        "city": "City",
        "state": "State",
        "zipCode": "12345"
      },
      "products": [
        {
          "id": 1,
          "name": "Product Name",
          "quantity": 2,
          "price": "29.99",
          "image": "product.jpg"
        }
      ]
    }
  }
}
```

### POST /deleteorder

**Description** : Supprime une commande

**Request Body** :
```json
{
  "order_id": 1
}
```

## Endpoints Catégories

### GET /categorylist?page=1

**Description** : Liste des catégories

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "categories": [
      {
        "id": 1,
        "name": "Electronics",
        "description": "Electronic products",
        "image": "category.jpg",
        "product_count": 25
      }
    ]
  }
}
```

### POST /addcategory

**Description** : Ajoute une nouvelle catégorie

**Request Body** :
```json
{
  "name": "New Category",
  "description": "Category description",
  "image": "category.jpg"
}
```

### POST /updatecategory

**Description** : Met à jour une catégorie

**Request Body** :
```json
{
  "maincategory_id": 1,
  "name": "Updated Category",
  "description": "Updated description"
}
```

### POST /deletecategory

**Description** : Supprime une catégorie

**Request Body** :
```json
{
  "maincategory_id": 1
}
```

## Endpoints Coupons

### GET /couponlist

**Description** : Liste des coupons

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "coupons": [
      {
        "id": 1,
        "couponName": "SUMMER20",
        "couponCode": "SUMMER20",
        "discountAmount": 20,
        "couponType": "percentage",
        "validFrom": "2024-01-01",
        "validTo": "2024-12-31",
        "usageLimit": 100,
        "usedCount": 25
      }
    ]
  }
}
```

### POST /addcoupon

**Description** : Crée un nouveau coupon

**Request Body** :
```json
{
  "coupon_name": "SUMMER20",
  "coupon_code": "SUMMER20",
  "discount_amount": 20,
  "coupon_type": "percentage",
  "valid_from": "2024-01-01",
  "valid_to": "2024-12-31",
  "usage_limit": 100
}
```

### POST /updatecoupon

**Description** : Met à jour un coupon

**Request Body** :
```json
{
  "coupon_id": 1,
  "coupon_name": "SUMMER25",
  "discount_amount": 25
}
```

### POST /deletecoupon

**Description** : Supprime un coupon

**Request Body** :
```json
{
  "coupon_id": 1
}
```

### GET /view-used-coupon

**Description** : Liste des coupons utilisés

## Endpoints Livraison et Taxes

### GET /shippinglist

**Description** : Liste des options de livraison

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "shipping_options": [
      {
        "id": 1,
        "name": "Standard Shipping",
        "price": 5.99,
        "delivery_days": "3-5"
      }
    ]
  }
}
```

### POST /addshipping

**Description** : Ajoute une option de livraison

**Request Body** :
```json
{
  "name": "Express Shipping",
  "price": 9.99,
  "delivery_days": "1-2"
}
```

### GET /taxlist

**Description** : Liste des taxes

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "taxes": [
      {
        "id": 1,
        "name": "VAT",
        "rate": 20.0,
        "type": "percentage"
      }
    ]
  }
}
```

### POST /addtax

**Description** : Ajoute une taxe

**Request Body** :
```json
{
  "name": "VAT",
  "rate": 20.0,
  "type": "percentage"
}
```

## Endpoints Paramètres

### GET /getemailsetting

**Description** : Récupère les paramètres email

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "smtp_host": "smtp.gmail.com",
    "smtp_port": 587,
    "smtp_username": "email@example.com",
    "smtp_password": "encrypted_password",
    "from_email": "noreply@example.com"
  }
}
```

### POST /emailsetting

**Description** : Configure les paramètres email

**Request Body** :
```json
{
  "smtp_host": "smtp.gmail.com",
  "smtp_port": 587,
  "smtp_username": "email@example.com",
  "smtp_password": "password",
  "from_email": "noreply@example.com"
}
```

### GET /getloyalitysetting

**Description** : Récupère les paramètres de fidélité

### POST /loyalitysetting

**Description** : Configure le programme de fidélité

## Endpoints Paiement

### GET /get-cod-payment

**Description** : Récupère les paramètres paiement à la livraison

### POST /cod-payment

**Description** : Configure le paiement à la livraison

### GET /get-bank-payment

**Description** : Récupère les paramètres virement bancaire

### POST /bank-payment

**Description** : Configure le virement bancaire

### GET /get-stripe-payment

**Description** : Récupère les paramètres Stripe

### POST /stripe-payment

**Description** : Configure Stripe

## Endpoints Statistiques

### GET /staticsdata

**Description** : Récupère les statistiques

**Response (200)** :
```json
{
  "status": 1,
  "data": {
    "total_products": 25,
    "total_orders": 45,
    "total_sales": 1500.00,
    "total_customers": 30,
    "monthly_sales": [
      {
        "month": "January",
        "sales": 500.00
      }
    ],
    "top_products": [
      {
        "product_id": 1,
        "name": "Product Name",
        "sales_count": 10
      }
    ]
  }
}
```

## Endpoints Profil

### POST /editprofile

**Description** : Met à jour le profil utilisateur

**Request Body** :
```json
{
  "name": "Updated Name",
  "email": "updated@example.com",
  "phone": "+1234567890"
}
```

### POST /updatepassword

**Description** : Change le mot de passe

**Request Body** :
```json
{
  "current_password": "oldpassword",
  "new_password": "newpassword"
}
```

## Gestion des Erreurs

### Codes de Statut HTTP

- **200** : Succès
- **201** : Créé avec succès
- **400** : Requête invalide
- **401** : Non autorisé (token invalide/expiré)
- **404** : Ressource non trouvée
- **500** : Erreur serveur

### Format des Erreurs

```json
{
  "status": 0,
  "message": "Error message",
  "data": {
    "message": "Detailed error description"
  }
}
```

### Gestion 401

En cas d'erreur 401, l'application :
1. Efface le token stocké
2. Redirige vers l'écran de login
3. Affiche un message d'erreur

## Pagination

La plupart des endpoints de liste supportent la pagination :

- **Query Parameter** : `page` (numéro de page, commence à 1)
- **Response** : Inclut les métadonnées de pagination

```json
{
  "pagination": {
    "current_page": 1,
    "total_pages": 5,
    "total_items": 50,
    "items_per_page": 10
  }
}
```

## Recherche

### POST /searchdata

**Description** : Recherche globale dans l'application

**Request Body** :
```json
{
  "search_term": "search query",
  "type": "all" // ou "products", "orders", "customers"
}
```

## Tests

### POST /testmail

**Description** : Teste la configuration email

**Request Body** :
```json
{
  "to_email": "test@example.com",
  "subject": "Test Email",
  "message": "This is a test email"
}
```

---

Cette documentation couvre tous les endpoints disponibles dans l'API Moteki Seller. Pour plus de détails sur l'implémentation côté client, consultez `ARCHITECTURE.md`.
