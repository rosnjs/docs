# Catalogue des Écrans - Moteki Seller App

## Vue d'ensemble

Ce catalogue documente tous les écrans de l'application Moteki Seller, leurs états, actions disponibles et widgets utilisés.

## Écrans d'Authentification

### 1. WelcomeScreen

**Fichier** : `lib/view/screen/welcome_screen.dart`

**Description** : Écran d'accueil pour les nouveaux utilisateurs

**États** :
- `initial` : Écran d'accueil avec logo
- `loading` : Chargement de la configuration
- `error` : Erreur de configuration

**Actions** :
- Navigation vers LoginScreen
- Configuration Firebase Remote Config
- Vérification du mode démo

**Widgets utilisés** :
- `assetSvdImageWidget` - Logo de l'application
- `CommonButton` - Bouton de démarrage

### 2. LoginScreen

**Fichier** : `lib/view/screen/auth/login_widget.dart`

**Description** : Écran de connexion avec options multiples

**États** :
- `social_login` : Connexion via réseaux sociaux
- `email_login` : Connexion par email
- `loading` : Authentification en cours
- `error` : Erreur d'authentification
- `success` : Connexion réussie

**Actions** :
- Connexion Facebook
- Connexion Google
- Connexion Apple
- Connexion par email
- Navigation vers inscription
- Mot de passe oublié

**Widgets utilisés** :
- `CommonSocialButton` - Boutons réseaux sociaux
- `CommonTextField` - Champs de saisie
- `CommonButton` - Bouton de connexion
- `assetSvdImageWidget` - Icônes

### 3. SignupWidget

**Fichier** : `lib/view/screen/auth/signup_widget.dart`

**Description** : Écran d'inscription

**États** :
- `form` : Formulaire d'inscription
- `loading` : Inscription en cours
- `error` : Erreur d'inscription
- `success` : Inscription réussie

**Actions** :
- Création de compte
- Validation des champs
- Navigation vers login

### 4. ForgotPasswordWidget

**Fichier** : `lib/view/screen/auth/forgot_password_widget.dart`

**Description** : Récupération de mot de passe

**États** :
- `email_input` : Saisie de l'email
- `loading` : Envoi en cours
- `success` : Email envoyé
- `error` : Erreur d'envoi

### 5. VerifyOtp

**Fichier** : `lib/view/screen/auth/verify_otp.dart`

**Description** : Vérification du code OTP

**États** :
- `code_input` : Saisie du code
- `loading` : Vérification en cours
- `success` : Code valide
- `error` : Code invalide

## Écrans Principaux

### 6. DashBoardManagerScreen

**Fichier** : `lib/view/screen/dashboard_manager/dashboard_manager.dart`

**Description** : Écran principal avec navigation bottom

**États** :
- `dashboard` : Onglet Dashboard actif
- `orders` : Onglet Orders actif
- `products` : Onglet Products actif
- `categories` : Onglet Categories actif
- `settings` : Onglet Settings actif

**Actions** :
- Navigation entre onglets
- Gestion de l'état de navigation

**Widgets utilisés** :
- `CustomConvexAppBar` - Navigation bottom personnalisée
- `Obx` - Gestion d'état réactive

### 7. HomeScreen (Dashboard)

**Fichier** : `lib/view/screen/home_screen/home_screen.dart`

**Description** : Tableau de bord principal

**États** :
- `loading` : Chargement des données
- `data_loaded` : Données affichées
- `error` : Erreur de chargement
- `empty` : Aucune donnée

**Actions** :
- Rafraîchissement des données (pull-to-refresh)
- Sélection de boutique
- Quick Add (produit/catégorie/coupon)
- Navigation vers détails
- Suppression d'éléments

**Sections** :
- **Profile Section** : Informations utilisateur
- **Store Dropdown** : Sélection de boutique
- **Quick Add** : Ajout rapide
- **Statistics** : Statistiques avec graphiques
- **QR Code** : Code QR de la boutique
- **Totals** : Totaux (produits, ventes, commandes)
- **Orders Graph** : Graphique des commandes
- **Top Products** : Meilleurs produits
- **Recent Orders** : Commandes récentes
- **Visitors Chart** : Graphique des visiteurs
- **Product Coupons** : Coupons produits

**Widgets utilisés** :
- `LiquidPullToRefresh` - Rafraîchissement
- `LoadingWidget` - État de chargement
- `buildProfileTitle` - Titre profil
- `myStoreDropDown` - Dropdown boutique
- `CommonIconButton` - Boutons d'action
- `titleShowMoreWidget` - Titres avec "Voir plus"
- `qrCodeWidget` - Widget QR code
- `totalProductWidget` - Widget totaux
- `OrderGraph` - Graphique commandes
- `topProductWidget` - Widget produit
- `recentOrdersWidget` - Widget commande
- `VisitorChart` - Graphique visiteurs
- `productCouponWidget` - Widget coupon

## Écrans de Gestion des Produits

### 8. ProductsScreen

**Fichier** : `lib/view/screen/product_screen/products_screen.dart`

**Description** : Liste des produits avec gestion

**États** :
- `loading` : Chargement des produits
- `data_loaded` : Produits affichés
- `loading_more` : Chargement pagination
- `error` : Erreur de chargement
- `empty` : Aucun produit

**Actions** :
- Ajout de produit
- Recherche de produit
- Filtrage des produits
- Pagination infinie
- Suppression de produit
- Navigation vers détails

**Widgets utilisés** :
- `CommonIconButton` - Bouton d'ajout
- `searchFieldWidget` - Champ de recherche
- `ProductWidget` - Widget produit
- `LoadingWidget` - État de chargement

### 9. AddNewProductScreen

**Fichier** : `lib/view/screen/product_screen/add_new_product_screen.dart`

**Description** : Création/Modification de produit

**États** :
- `form` : Formulaire de saisie
- `loading` : Sauvegarde en cours
- `success` : Produit sauvegardé
- `error` : Erreur de sauvegarde

**Actions** :
- Création de produit
- Modification de produit
- Upload d'images
- Ajout de variants
- Sauvegarde des données

**Sections** :
- **Basic Info** : Informations de base
- **Pricing** : Prix et remises
- **Inventory** : Stock et gestion
- **Images** : Upload d'images
- **Variants** : Variantes du produit
- **SEO** : Optimisation SEO

### 10. ProductDetailScreen

**Fichier** : `lib/view/screen/product_screen/product_detail_screen.dart`

**Description** : Détails d'un produit

**États** :
- `loading` : Chargement des détails
- `data_loaded` : Détails affichés
- `error` : Erreur de chargement

**Actions** :
- Affichage des détails
- Modification du produit
- Suppression du produit
- Ajout d'avis
- Gestion des variants

### 11. AddRatingScreen

**Fichier** : `lib/view/screen/product_screen/add_rating_screen.dart`

**Description** : Ajout d'avis produit

**États** :
- `form` : Formulaire d'avis
- `loading` : Sauvegarde en cours
- `success` : Avis ajouté
- `error` : Erreur de sauvegarde

### 12. AddVariantScreen

**Fichier** : `lib/view/screen/product_screen/add_variant_screen.dart`

**Description** : Ajout de variantes produit

**États** :
- `form` : Formulaire de variante
- `loading` : Sauvegarde en cours
- `success` : Variante ajoutée
- `error` : Erreur de sauvegarde

## Écrans de Gestion des Commandes

### 13. OrderScreen

**Fichier** : `lib/view/screen/order_screen/order_screen.dart`

**Description** : Liste des commandes

**États** :
- `loading` : Chargement des commandes
- `data_loaded` : Commandes affichées
- `loading_more` : Chargement pagination
- `error` : Erreur de chargement
- `empty` : Aucune commande

**Actions** :
- Recherche de commande
- Filtrage par statut
- Pagination infinie
- Suppression de commande
- Navigation vers détails

### 14. OrderDetailScreen

**Fichier** : `lib/view/screen/order_screen/order_detail_screen.dart`

**Description** : Détails d'une commande

**États** :
- `loading` : Chargement des détails
- `data_loaded` : Détails affichés
- `error` : Erreur de chargement

**Actions** :
- Affichage des détails
- Mise à jour du statut
- Suppression de commande
- Génération de facture
- Impression de facture

### 15. InvoicePDFView

**Fichier** : `lib/view/screen/order_screen/invoice_pdf_view.dart`

**Description** : Affichage de la facture PDF

**États** :
- `loading` : Génération PDF
- `pdf_ready` : PDF affiché
- `error` : Erreur de génération

**Actions** :
- Affichage PDF
- Impression PDF
- Partage PDF
- Téléchargement PDF

## Écrans de Gestion des Catégories

### 16. CategoriesScreen

**Fichier** : `lib/view/screen/category_screen/category_screen.dart`

**Description** : Liste des catégories

**États** :
- `loading` : Chargement des catégories
- `data_loaded` : Catégories affichées
- `loading_more` : Chargement pagination
- `error` : Erreur de chargement
- `empty` : Aucune catégorie

**Actions** :
- Ajout de catégorie
- Modification de catégorie
- Suppression de catégorie
- Pagination infinie

### 17. AddCategoryBottomSheet

**Fichier** : `lib/view/screen/home_screen/add_category_bottomsheet.dart`

**Description** : Modal d'ajout de catégorie

**États** :
- `form` : Formulaire de catégorie
- `loading` : Sauvegarde en cours
- `success` : Catégorie ajoutée
- `error` : Erreur de sauvegarde

**Actions** :
- Création de catégorie
- Modification de catégorie
- Upload d'image
- Sauvegarde des données

## Écrans de Paramètres

### 18. SettingScreen

**Fichier** : `lib/view/screen/setting_screen/setting_screen.dart`

**Description** : Écran principal des paramètres

**États** :
- `menu` : Menu des paramètres
- `loading` : Chargement des paramètres
- `error` : Erreur de chargement

**Actions** :
- Navigation vers sous-paramètres
- Déconnexion
- Gestion des thèmes

**Sections** :
- **Store Settings** : Paramètres boutique
- **Store Theme Settings** : Thème boutique
- **Store Payment** : Paramètres paiement
- **Store Email Setting** : Paramètres email
- **Store Loyalty Program** : Programme fidélité
- **Logout** : Déconnexion

### 19. StoreSettingScreen

**Fichier** : `lib/view/screen/setting_screen/store_setting_screen.dart`

**Description** : Paramètres de la boutique

**États** :
- `form` : Formulaire de paramètres
- `loading` : Sauvegarde en cours
- `success` : Paramètres sauvegardés
- `error` : Erreur de sauvegarde

**Actions** :
- Modification des informations boutique
- Upload du logo
- Configuration des paramètres
- Sauvegarde des données

### 20. StoreThemeSettingScreen

**Fichier** : `lib/view/screen/setting_screen/store_theme_setting_screen/store_theme_setting_screen.dart`

**Description** : Paramètres de thème

**États** :
- `theme_selection` : Sélection de thème
- `customization` : Personnalisation
- `preview` : Aperçu du thème

**Actions** :
- Sélection de thème
- Personnalisation des couleurs
- Aperçu en temps réel
- Sauvegarde du thème

### 21. PaymentSettingScreen

**Fichier** : `lib/view/screen/setting_screen/payment_setting_screen/payment_setting_screen.dart`

**Description** : Paramètres de paiement

**États** :
- `payment_methods` : Méthodes de paiement
- `configuration` : Configuration
- `testing` : Test des paiements

**Actions** :
- Configuration COD
- Configuration virement bancaire
- Configuration Stripe
- Test des paiements

### 22. CODScreen

**Fichier** : `lib/view/screen/setting_screen/payment_setting_screen/cod_screen.dart`

**Description** : Configuration paiement à la livraison

**États** :
- `form` : Formulaire de configuration
- `loading` : Sauvegarde en cours
- `success` : Configuration sauvegardée
- `error` : Erreur de sauvegarde

### 23. BankTransferScreen

**Fichier** : `lib/view/screen/setting_screen/payment_setting_screen/bank_transfer_screen.dart`

**Description** : Configuration virement bancaire

**États** :
- `form` : Formulaire bancaire
- `loading` : Sauvegarde en cours
- `success` : Configuration sauvegardée
- `error` : Erreur de sauvegarde

### 24. StripeScreen

**Fichier** : `lib/view/screen/setting_screen/payment_setting_screen/stripe_screen.dart`

**Description** : Configuration Stripe

**États** :
- `form` : Formulaire Stripe
- `loading` : Sauvegarde en cours
- `success` : Configuration sauvegardée
- `error` : Erreur de sauvegarde

### 25. EmailSettingScreen

**Fichier** : `lib/view/screen/setting_screen/email_setting_screen.dart`

**Description** : Paramètres email

**États** :
- `form` : Formulaire SMTP
- `loading` : Sauvegarde en cours
- `testing` : Test d'envoi
- `success` : Configuration sauvegardée
- `error` : Erreur de sauvegarde

**Actions** :
- Configuration SMTP
- Test d'envoi d'email
- Sauvegarde des paramètres

### 26. LoyaltyProgramScreen

**Fichier** : `lib/view/screen/setting_screen/loyality_setting_screen.dart`

**Description** : Programme de fidélité

**États** :
- `form` : Formulaire de fidélité
- `loading` : Sauvegarde en cours
- `success` : Programme sauvegardé
- `error` : Erreur de sauvegarde

## Écrans de Statistiques

### 27. StatisticsScreen

**Fichier** : `lib/view/screen/statistics_screen/statistics_screen.dart`

**Description** : Statistiques détaillées

**États** :
- `loading` : Chargement des statistiques
- `data_loaded` : Statistiques affichées
- `error` : Erreur de chargement

**Actions** :
- Affichage des graphiques
- Filtrage par période
- Export des données

**Sections** :
- **Sales Chart** : Graphique des ventes
- **Orders Chart** : Graphique des commandes
- **Products Chart** : Graphique des produits
- **Visitors Chart** : Graphique des visiteurs
- **Revenue Chart** : Graphique des revenus

## Écrans de Coupons

### 28. CouponScreen

**Fichier** : `lib/view/screen/home_screen/coupon_screen/coupon_screen.dart`

**Description** : Liste des coupons

**États** :
- `loading` : Chargement des coupons
- `data_loaded` : Coupons affichés
- `loading_more` : Chargement pagination
- `error` : Erreur de chargement
- `empty` : Aucun coupon

**Actions** :
- Ajout de coupon
- Modification de coupon
- Suppression de coupon
- Pagination infinie

### 29. CouponDetailScreen

**Fichier** : `lib/view/screen/home_screen/coupon_screen/coupon_detail_screen.dart`

**Description** : Détails d'un coupon

**États** :
- `loading` : Chargement des détails
- `data_loaded` : Détails affichés
- `error` : Erreur de chargement

**Actions** :
- Affichage des détails
- Modification du coupon
- Suppression du coupon

### 30. NewCouponBottomSheet

**Fichier** : `lib/view/screen/home_screen/coupon_screen/new_coupon_bottomsheet.dart`

**Description** : Modal d'ajout de coupon

**États** :
- `form` : Formulaire de coupon
- `loading` : Sauvegarde en cours
- `success` : Coupon ajouté
- `error` : Erreur de sauvegarde

**Actions** :
- Création de coupon
- Modification de coupon
- Génération de code
- Sauvegarde des données

## Écrans de Livraison et Taxes

### 31. ShippingScreen

**Fichier** : `lib/view/screen/home_screen/shipping_screen.dart`

**Description** : Gestion des options de livraison

**États** :
- `loading` : Chargement des options
- `data_loaded` : Options affichées
- `loading_more` : Chargement pagination
- `error` : Erreur de chargement
- `empty` : Aucune option

**Actions** :
- Ajout d'option de livraison
- Modification d'option
- Suppression d'option
- Pagination infinie

### 32. AddShippingBottomSheet

**Fichier** : `lib/view/screen/home_screen/add_shipping_bottomsheet.dart`

**Description** : Modal d'ajout d'option de livraison

**États** :
- `form` : Formulaire de livraison
- `loading` : Sauvegarde en cours
- `success` : Option ajoutée
- `error` : Erreur de sauvegarde

### 33. TaxScreen

**Fichier** : `lib/view/screen/home_screen/tax_screen.dart`

**Description** : Gestion des taxes

**États** :
- `loading` : Chargement des taxes
- `data_loaded` : Taxes affichées
- `loading_more` : Chargement pagination
- `error` : Erreur de chargement
- `empty` : Aucune taxe

**Actions** :
- Ajout de taxe
- Modification de taxe
- Suppression de taxe
- Pagination infinie

### 34. AddTaxBottomSheet

**Fichier** : `lib/view/screen/home_screen/add_tax_bottomsheet.dart`

**Description** : Modal d'ajout de taxe

**États** :
- `form` : Formulaire de taxe
- `loading` : Sauvegarde en cours
- `success` : Taxe ajoutée
- `error` : Erreur de sauvegarde

## Écrans de Profil

### 35. ProfileScreen

**Fichier** : `lib/view/screen/profile_screen/profile_screen.dart`

**Description** : Profil utilisateur

**États** :
- `loading` : Chargement du profil
- `data_loaded` : Profil affiché
- `error` : Erreur de chargement

**Actions** :
- Affichage du profil
- Modification du profil
- Changement de mot de passe
- Déconnexion

## Widgets Réutilisables

### Widgets Communs

- `CommonButton` - Boutons standards
- `CommonTextField` - Champs de texte
- `CommonAppBar` - App bar personnalisée
- `CommonIconButton` - Boutons avec icônes
- `CommonDropDownWidget` - Dropdowns
- `CommonSnackBarWidget` - Messages toast
- `CommonSpaceDividerWidget` - Espacements
- `LoadingWidget` - État de chargement
- `IconAndImage` - Gestion des icônes/images

### Widgets Spécialisés

- `CustomBottomNavBar` - Navigation bottom
- `ProductWidget` - Widget produit
- `OrderWidget` - Widget commande
- `CategoryWidget` - Widget catégorie
- `CouponWidget` - Widget coupon
- `StatisticsWidget` - Widget statistiques

## États Globaux

### États de Chargement

- `isDataAvailable` - Données en cours de chargement
- `isLoading` - Chargement général
- `isRefreshing` - Rafraîchissement en cours

### États d'Erreur

- `hasError` - Présence d'erreur
- `errorMessage` - Message d'erreur
- `networkError` - Erreur réseau

### États de Navigation

- `currentIndex` - Index de navigation actuel
- `isBack` - Possibilité de retour
- `canNavigate` - Autorisation de navigation

---

Ce catalogue couvre tous les écrans de l'application Moteki Seller avec leurs états, actions et widgets utilisés. Pour plus de détails sur l'implémentation, consultez les fichiers source dans `lib/view/screen/`.
