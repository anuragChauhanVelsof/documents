Certainly! Here's the application flow document:

# OC MAB Application Flow

## 1. Application Initialization

- The application begins in the `main.dart` file when the user opens it.
- `runApp()` loads the initial widget, `MyApp()`, which handles app setup.

## 2. App Initialization (MyApp)

- `MyApp()` initializes Firebase Messaging for notifications and deep linking.
- It sets up providers and routes for data sharing and navigation.
- The app navigates to the `SplashScreen`.

## 3. SplashScreen

- Performs checks:
  - Internet connection
  - Current location and permissions
  - App type (Demo or Not) using `appGetCheck` API
- If a demo app:
  - Logs out the user
  - Resets recent products
  - Sets default languageISO Code using SharedPreference
- Shows 'View Your Store' and 'View Demo' buttons.

## 4. View Your Store (Demo App)

- User selects OC Version and enters store URL.
- Calls `getAppConfig` API for various configurations.
- Navigates to `Base Navigator`.

## 5. View Demo (Demo App)

- Uses default URL and configuration from `getAppConfig` API.
- Data is stored in a Provider.
- Navigates to `Base Navigator`.

## 6. Not a Demo App

- Calls `getAppConfig` API with the default BaseUrl.
- Saves the URL in SharedPreference if not saved.
- Navigates to `Base Navigator`.

## 7. Base Navigator

- Initializes page index (default: Home Page) in `initState`.
- Handles:
  - API calls
  - App exit
  - User login status
  - Page refresh
  - Exit confirmation pop-up.

## 8. Home Page

- Displays products and categories from `getAppConfig`.
- Features horizontal sliding views, grid views, and more.
- Includes a side drawer and a Global App Bar with Menu Categories, profile data, and CMS links.
- Clicking widgets navigates to Category or Product pages.

## 9. Category Page

- Fetches products from categories using `getCategoriesDetails` API.
- Displays an app bar with the selected category title.
- Offers wishlist and cart icons.
- Allows sorting and filtering.
- Clicking products navigates to Product Page.

## 10. Product Page

- Uses Product ID to call `getProductDetails` API.
- Displays product details and reviews.
- Provides options to:
  - Write reviews
  - Add products to the cart (using `addToCart` API)
  - Register for notifications (using `appFCMregister`)
  - Save product reviews (using `appSaveProductReviews`)
- Offers checkout option if the user is logged in.

## 11. Checkout Page

- Calls `appCheckout` API to retrieve cart details.
- Displays cart items, pricing, shipping addresses, and charges.
- Allows users to:
  - Change the address
  - Add a new billing address
  - Add order comments
- Proceeds to the Payment Page.

## 12. Payment Page

- Calls `appGetPaymentMethods` API to list payment methods.
- Completing the payment triggers `appCreateOrder` API.
- Redirects to the Order Listing Page.

## 13. Order Listing Page

- Calls `apGetOrdersList` using `initState`.
- Displays order details.
- Offers a Reorder button, allowing users to reorder products via `appReorder`.

## 14. Shopping Bag Screen

- Calls `appGetCartDetails` using `initState` to fetch cart item details.
- Displays cart items.
- Allows users to:
  - Apply vouchers
  - Remove items
  - Update item quantities
- Features a "Continue Shopping" button that leads to the Home Page if the cart is empty.

## 15. Search Screen

- Includes a global app bar, text input field, and barcode scanner.
- Users can manually enter search terms or scan barcodes.
- Submits the search term using `appGetCategoryDetails` and displays results on the Category Screen.

## 16. Multi-Level Category Page

- Utilizes the global app bar to display categories fetched from the `getAppConfig` API.
- Users can select categories to navigate to the Category Screen.

## 17. My Account Page

- Features:
  - Login
  - Logout
  - Update profile
  - Add/Update addresses
- Displays CMS links from `getAppConfig`.
- Content displayed depends on user login status.

## 18. MyProfile Scaffold

- Available if the user is logged in.
- Options to:
  - View My Profiles
  - View My Orders
  - View My Addresses
  - Logout (using Shared Preferences)
  - Delete Account (using `appDeleteUser`)

## 19. MyGuestProfile Scaffold

- Available if the user is not logged in.
- Options to:
  - Login
  - Sign Up

## 20. SignUp Screen

- Provides various sign-up options (e.g., Google Login, Facebook Login, email, phone number).
- Sign-ups are done using `appSocialSignUp` API.

## 21. Login Screen

- Offers various login options (e.g., Google Login, Facebook Login, email, phone number, forgot password).
- Login is performed using `appSocialLogin` API.

## 22. WishList Screen

- Displays wishlisted products.
- Fetches wishlisted items using `appGetWishList`.
- Allows users to remove items (using `appRemoveRemoveWishList`).
- Clicking on a product opens the Product Page.

## 23. Custom Drawer

- Contains CMS links and categories fetched from `getAppConfig`.
- Provides login/signup options.
- Includes a currency selector dropdown using `getAppConfig`.

## 24. CMS Links

- Open URLs in a webview.

## 25. Forgot Password Page

- Allows users to enter their email.
- Sends a reset password link to the user's email using `AppForgotPassword` API.

## 26. Address Listing Page

- Displays user addresses fetched from `getCustomerAddress`.
- Provides options to add or edit addresses (using `appAddAdress` and `appUdpateAdress`).

## 27. Order Details Page

- Calls the `appGetOrder` API to display order details.
- Displays information such as status, price details, and order ID.

This comprehensive document outlines the flow of the OC MAB application, detailing the functionalities and interactions at each stage of the user experience.
