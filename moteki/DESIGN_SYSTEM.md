# Design System - Moteki Seller App

## Vue d'ensemble

Le design system de Moteki Seller App suit les principes du Material Design avec une personnalisation cohérente pour une application e-commerce. Il utilise une palette de couleurs navy blue et vert, une typographie Outfit, et des composants réutilisables.

## Palette de Couleurs

### Couleurs Principales

#### Couleurs de Base
```dart
// Couleurs principales
static Color cBlack = Colors.black;                    // #000000
static Color cWhite = Color(0xffFFFFFF);              // #FFFFFF
static Color cTransparent = Colors.transparent;       // Transparent
```

#### Couleurs de Thème
```dart
// Couleurs de thème
static Color themeNavyBlueColor = Color(0xff172C4E);   // Navy Blue
static Color cBottomNavyBlueColor = Color(0xff172C4E); // Navy Blue
static Color themeGreenColor = Color(0xff6FD943);     // Green
```

#### Couleurs d'Interface
```dart
// Couleurs d'interface
static Color cBorder = Color(0xffCFD9E3);             // Border Grey
static Color cBackGround = Color(0xffFFFFFF);         // Background White
static Color cButton = Color(0xffF0F1F5);             // Button Grey
static Color cRed = Color(0xffFF754C);                // Red
```

#### Couleurs de Texte
```dart
// Couleurs de texte
static Color cWhiteFont = Color(0xffFAFBFD);          // White Text
static Color cBlackFont = Colors.black;               // Black Text
static Color cFont = Color(0xffB2BBCE);               // Grey Text
static Color cGreenFont = Color(0xff6FD943);          // Green Text
static Color cText = Color(0xff1E222B);               // Dark Text
static Color cDarkGreyFont = Color(0xff717887);       // Dark Grey Text
static Color cLabel = Color(0xff172C4E);              // Label Navy
static Color cRedText = Color(0xffFC275A);            // Red Text
static Color cHintFont = Color(0xffFFFFFF);           // Hint White
```

#### Couleurs d'État
```dart
// Couleurs d'état
static Color cLightGreen = Color.fromRGBO(111, 217, 67, 0.2);  // Light Green
static Color cLightRed = Color.fromRGBO(252, 39, 90, 0.2);    // Light Red
static Color cGreyOpacity = Color.fromRGBO(0, 0, 0, 0.52);     // Grey Overlay
```

#### Couleurs d'Ombre et Diviseurs
```dart
// Couleurs d'ombre et diviseurs
static Color cShadow = Color.fromRGBO(0, 0, 0, 0.04);          // Shadow
static Color cDivider = Color(0xffDCE2ED);                     // Divider
static Color cPDFPage = Color(0xfff5f5f5);                    // PDF Background
```

### Thèmes Clair et Sombre

#### Thème Clair (LightThemeColor)
```dart
class LightThemeColor {
  static Color cBackGround = Color(0xffFFFFFF);         // White Background
  static Color cWhiteFont = Colors.white;               // White Text
  static Color cBlackFont = Colors.black;               // Black Text
  static Color cText = Color(0xff1E222B);               // Dark Text
  static Color cLabel = Color(0xff172C4E);              // Navy Label
  static Color cBottomNavyBlueColor = Color(0xff172C4E); // Navy Bottom
}
```

#### Thème Sombre (DarkThemeColor)
```dart
class DarkThemeColor {
  static Color cBackGround = Color(0xff0A0A13);         // Dark Background
  static Color cWhiteFont = Colors.black;               // Black Text
  static Color cBlackFont = Colors.white;               // White Text
  static Color cText = Colors.white;                    // White Text
  static Color cLabel = Colors.white;                   // White Label
  static Color cBottomNavyBlueColor = Color(0xff222637); // Dark Navy Bottom
}
```

## Typographie

### Police de Base
- **Famille** : Outfit
- **Style** : Regular, Medium, SemiBold, Bold
- **Tailles** : 8px à 55px

### Hiérarchie Typographique

#### Regular (FontWeight.w400)
```dart
// Tailles disponibles : 8, 10, 12, 14, 16, 18, 20
TextStyle get pRegular8 => TextStyle(
  fontSize: 8,
  fontWeight: FontWeight.w400,
  color: AppColor.cLabel,
  fontFamily: 'Outfit',
);
```

#### Medium (FontWeight.w500)
```dart
// Tailles disponibles : 8, 10, 12, 14, 16, 18, 24, 36
TextStyle get pMedium14 => TextStyle(
  fontSize: 14,
  fontWeight: FontWeight.w500,
  color: AppColor.cLabel,
  fontFamily: 'Outfit',
);
```

#### SemiBold (FontWeight.w600)
```dart
// Tailles disponibles : 8, 10, 12, 14, 16, 18, 19, 21, 23, 27
TextStyle get pSemiBold16 => TextStyle(
  fontSize: 16,
  fontWeight: FontWeight.w600,
  color: AppColor.cLabel,
  fontFamily: 'Outfit',
);
```

#### Bold (FontWeight.w700)
```dart
// Tailles disponibles : 12, 14, 16, 18, 24, 30, 55
TextStyle get pBold30 => TextStyle(
  fontSize: 30,
  fontWeight: FontWeight.w700,
  color: AppColor.cLabel,
  fontFamily: 'Outfit',
);
```

### Utilisation des Styles

#### Titres
- **Titre Principal** : `pBold30` (30px, Bold)
- **Titre Section** : `pBold24` (24px, Bold)
- **Titre Sous-section** : `pBold18` (18px, Bold)

#### Corps de Texte
- **Texte Principal** : `pRegular16` (16px, Regular)
- **Texte Secondaire** : `pRegular14` (14px, Regular)
- **Texte Petit** : `pRegular12` (12px, Regular)

#### Labels et Boutons
- **Label** : `pMedium14` (14px, Medium)
- **Bouton** : `pBold14` (14px, Bold)
- **Lien** : `pMedium16` (16px, Medium)

## Composants Réutilisables

### 1. CommonButton

**Fichier** : `lib/view/widget/common_button.dart`

**Description** : Bouton standard avec personnalisation

```dart
CommonButton(
  title: 'LogIn',
  onPressed: () {
    // Action
  },
  height: 42,
  width: Get.width,
  btnColor: AppColor.themeGreenColor,
  textColor: AppColor.cWhite,
  fontSize: 14,
)
```

**Propriétés** :
- `title` : Texte du bouton
- `height` : Hauteur (défaut: 42)
- `width` : Largeur (défaut: Get.width)
- `onPressed` : Action au clic
- `btnColor` : Couleur de fond (défaut: themeGreenColor)
- `textColor` : Couleur du texte (défaut: cWhite)
- `fontSize` : Taille de police (défaut: 14)

### 2. CommonIconButton

**Description** : Bouton avec icône

```dart
CommonIconButton(
  title: 'Add Product',
  iconData: DefaultImages.addCircleIcn,
  onPressed: () {
    // Action
  },
  height: 43,
  btnColor: AppColor.themeGreenColor,
  textColor: AppColor.cWhite,
)
```

**Propriétés** :
- `title` : Texte du bouton
- `iconData` : Icône SVG
- `height` : Hauteur (défaut: 43)
- `onPressed` : Action au clic
- `btnColor` : Couleur de fond
- `textColor` : Couleur du texte
- `radius` : Rayon des coins (défaut: 35)

### 3. CommonTextField

**Fichier** : `lib/view/widget/common_text_field.dart`

**Description** : Champ de texte personnalisé

```dart
CommonTextField(
  controller: emailController,
  labelText: 'Email Address',
  hintText: 'johndoe@company.com',
  prefix: DefaultImages.envelopeIcn,
  keyboardType: TextInputType.emailAddress,
  validator: (value) {
    return Validator.validateEmail(value!);
  },
)
```

**Propriétés** :
- `controller` : Contrôleur de texte
- `labelText` : Label du champ
- `hintText` : Texte d'aide
- `prefix` : Icône préfixe
- `suffix` : Widget suffixe
- `keyboardType` : Type de clavier
- `validator` : Fonction de validation
- `obscureText` : Masquer le texte
- `readOnly` : Lecture seule

### 4. CommonAppBar

**Fichier** : `lib/view/widget/common_appbar_widget.dart`

**Description** : App bar personnalisée

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

### 5. CustomBottomNavBar

**Fichier** : `lib/view/widget/custom_bottom_nav_bar/custom_bottom_nav_bar.dart`

**Description** : Navigation bottom personnalisée

```dart
CustomConvexAppBar(
  backgroundColor: AppColor.cBottomNavyBlueColor,
  color: AppColor.cDarkGreyFont,
  activeColor: AppColor.cWhite,
  height: 65,
  style: TabStyle.fixedCircle,
  top: -35,
  curve: Curves.easeOut,
  initialActiveIndex: 2,
  items: [
    CustomTabItem(icon: ordersIcon, title: 'Orders'),
    CustomTabItem(icon: productsIcon, title: 'Products'),
    CustomTabItem(icon: dashboardIcon, title: 'Dashboard'),
    CustomTabItem(icon: categoriesIcon, title: 'Categories'),
    CustomTabItem(icon: settingsIcon, title: 'Settings'),
  ],
  onTap: (index) {
    // Navigation
  },
)
```

### 6. LoadingWidget

**Fichier** : `lib/view/widget/loading_widget.dart`

**Description** : Widget de chargement

```dart
LoadingWidget()
```

### 7. CommonDropDownWidget

**Fichier** : `lib/view/widget/common_drop_down_widget.dart`

**Description** : Dropdown personnalisé

```dart
CommonDropDownWidget(
  items: ['Option 1', 'Option 2', 'Option 3'],
  onChanged: (value) {
    // Action
  },
  hint: 'Select an option',
)
```

### 8. CommonSnackBarWidget

**Fichier** : `lib/view/widget/common_snak_bar_widget.dart`

**Description** : Messages toast

```dart
commonToast('Message to display');
```

### 9. CommonSpaceDividerWidget

**Fichier** : `lib/view/widget/common_space_divider_widget.dart`

**Description** : Espacements et diviseurs

```dart
// Espacement vertical
verticalSpace(20);

// Espacement horizontal
horizontalSpace(10);

// Diviseur horizontal
horizontalDivider();
```

### 10. IconAndImage

**Fichier** : `lib/view/widget/icon_and_image.dart`

**Description** : Gestion des icônes et images

```dart
// Icône SVG
assetSvdImageWidget(
  image: DefaultImages.addCircleIcn,
  width: 24,
  height: 24,
  colorFilter: ColorFilter.mode(AppColor.cLabel, BlendMode.srcIn),
);

// Image réseau
networkImageWidget(
  imageUrl: 'https://example.com/image.jpg',
  width: 100,
  height: 100,
);
```

## Espacements et Dimensions

### Espacements Standard

```dart
// Espacements verticaux
verticalSpace(5);   // Petit
verticalSpace(10); // Moyen
verticalSpace(15); // Standard
verticalSpace(20); // Grand
verticalSpace(25); // Très grand

// Espacements horizontaux
horizontalSpace(5);
horizontalSpace(10);
horizontalSpace(15);
horizontalSpace(20);
```

### Dimensions de Composants

```dart
// Hauteurs standard
height: 42,   // Boutons
height: 43,   // Boutons avec icône
height: 51,   // Boutons grands
height: 65,   // Navigation bottom

// Rayons de coins
BorderRadius.circular(12);  // Petits éléments
BorderRadius.circular(15);  // Moyens éléments
BorderRadius.circular(30);  // Grands éléments
BorderRadius.circular(35);  // Boutons
```

## Ombres et Effets

### Ombres Standard

```dart
// Ombre légère
BoxShadow(
  color: AppColor.cShadow,
  offset: Offset(0, 2),
  blurRadius: 4,
  spreadRadius: 0,
)

// Ombre moyenne
BoxShadow(
  color: AppColor.cShadow,
  offset: Offset(0, 4),
  blurRadius: 8,
  spreadRadius: 0,
)

// Ombre forte
BoxShadow(
  color: AppColor.cShadow,
  offset: Offset(0, 8),
  blurRadius: 15,
  spreadRadius: 0.5,
)
```

### Effets de Transparence

```dart
// Overlay modal
barrierColor: AppColor.cGreyOpacity,

// Effets de couleur
Color.fromRGBO(111, 217, 67, 0.2),  // Light Green
Color.fromRGBO(252, 39, 90, 0.2),   // Light Red
Color.fromRGBO(0, 0, 0, 0.52),      // Grey Overlay
```

## Animations et Transitions

### Transitions GetX

```dart
// Transitions disponibles
Transition.fadeIn        // Fondu d'entrée
Transition.slideInRight  // Glissement depuis la droite
Transition.slideInLeft   // Glissement depuis la gauche
Transition.slideInUp     // Glissement depuis le bas
Transition.zoom          // Zoom
Transition.cupertino     // Style iOS
```

### Durées d'Animation

```dart
// Durées standard
Duration(milliseconds: 200);  // Rapide
Duration(milliseconds: 300);  // Standard
Duration(milliseconds: 500);  // Lent
```

## Responsive Design

### Breakpoints

```dart
// Tailles d'écran
Get.width < 600;   // Mobile
Get.width >= 600;  // Tablet
Get.width >= 900;  // Desktop
```

### Adaptations

```dart
// Adaptation des tailles
width: Get.width * 0.9,  // 90% de la largeur
height: Get.height * 0.1, // 10% de la hauteur
padding: EdgeInsets.all(Get.width * 0.05), // 5% de padding
```

## Accessibilité

### Contraste des Couleurs

- **Texte sur fond clair** : Contraste minimum 4.5:1
- **Texte sur fond sombre** : Contraste minimum 3:1
- **Éléments interactifs** : Contraste minimum 3:1

### Tailles Minimales

- **Boutons** : Minimum 44x44 points
- **Zones de toucher** : Minimum 48x48 points
- **Texte** : Minimum 12px pour la lisibilité

## Thèmes et Personnalisation

### Configuration du Thème

```dart
// Configuration du thème dans ThemeController
class ThemeController extends GetxController {
  ThemeData get theme => isDarkMode.value 
    ? _darkTheme 
    : _lightTheme;
    
  ThemeData get _lightTheme => ThemeData(
    fontFamily: 'Outfit',
    primaryColor: AppColor.themeNavyBlueColor,
    scaffoldBackgroundColor: AppColor.cBackGround,
    // ... autres propriétés
  );
}
```

### Variables CSS-like

```dart
// Variables de thème
static const double borderRadius = 12.0;
static const double buttonHeight = 42.0;
static const double inputHeight = 48.0;
static const double spacingUnit = 8.0;
```

## Bonnes Pratiques

### Utilisation des Couleurs

1. **Cohérence** : Utiliser toujours les couleurs du design system
2. **Contraste** : Vérifier le contraste pour l'accessibilité
3. **Sémantique** : Utiliser les couleurs appropriées (vert = succès, rouge = erreur)

### Utilisation de la Typographie

1. **Hiérarchie** : Respecter la hiérarchie des tailles
2. **Lisibilité** : Utiliser des tailles appropriées
3. **Cohérence** : Utiliser les styles prédéfinis

### Utilisation des Composants

1. **Réutilisabilité** : Utiliser les composants existants
2. **Personnalisation** : Personnaliser via les propriétés
3. **Cohérence** : Maintenir la cohérence visuelle

---

Ce design system assure la cohérence visuelle et l'expérience utilisateur optimale de l'application Moteki Seller. Pour plus de détails sur l'implémentation, consultez les fichiers source dans `lib/view/widget/` et `lib/utils/`.
