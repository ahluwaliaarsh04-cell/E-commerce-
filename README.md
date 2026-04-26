import java.util.*;

class Product {
    int id;
    String name;
    double price;

    Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }
}

class CartItem {
    Product product;
    int quantity;

    CartItem(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
    }
}

public class ECommerceApp {

    static Scanner sc = new Scanner(System.in);
    static List<Product> products = new ArrayList<>();
    static List<CartItem> cart = new ArrayList<>();

    public static void main(String[] args) {
        addProducts();
        login();
        menu();
    }

    // Add sample products
    static void addProducts() {
        products.add(new Product(1, "Laptop", 50000));
        products.add(new Product(2, "Phone", 20000));
        products.add(new Product(3, "Headphones", 2000));
        products.add(new Product(4, "Smart Watch", 5000));
    }

    // Simple login
    static void login() {
        System.out.println("=== LOGIN ===");
        System.out.print("Enter username: ");
        String user = sc.next();
        System.out.print("Enter password: ");
        String pass = sc.next();

        if (user.equals("admin") && pass.equals("1234")) {
            System.out.println("Login Successful!\n");
        } else {
            System.out.println("Invalid login! Try again.");
            login();
        }
    }

    // Main Menu
    static void menu() {
        while (true) {
            System.out.println("\n=== MENU ===");
            System.out.println("1. View Products");
            System.out.println("2. Add to Cart");
            System.out.println("3. View Cart");
            System.out.println("4. Checkout");
            System.out.println("5. Exit");

            System.out.print("Enter choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    viewProducts();
                    break;
                case 2:
                    addToCart();
                    break;
                case 3:
                    viewCart();
                    break;
                case 4:
                    checkout();
                    break;
                case 5:
                    System.exit(0);
                default:
                    System.out.println("Invalid choice!");
            }
        }
    }

    // Show products
    static void viewProducts() {
        System.out.println("\n--- Products ---");
        for (Product p : products) {
            System.out.println(p.id + ". " + p.name + " - ₹" + p.price);
        }
    }

    // Add to cart
    static void addToCart() {
        viewProducts();
        System.out.print("Enter product ID: ");
        int id = sc.nextInt();
        System.out.print("Enter quantity: ");
        int qty = sc.nextInt();

        for (Product p : products) {
            if (p.id == id) {
                cart.add(new CartItem(p, qty));
                System.out.println("Added to cart!");
                return;
            }
        }
        System.out.println("Product not found!");
    }

    // View cart
    static void viewCart() {
        double total = 0;
        System.out.println("\n--- Cart ---");

        for (CartItem item : cart) {
            double cost = item.product.price * item.quantity;
            total += cost;
            System.out.println(item.product.name + " x " + item.quantity + " = ₹" + cost);
        }

        System.out.println("Total = ₹" + total);
    }

    // Checkout
    static void checkout() {
        double total = 0;

        System.out.println("\n--- BILL ---");

        for (CartItem item : cart) {
            double cost = item.product.price * item.quantity;
            total += cost;
            System.out.println(item.product.name + " x " + item.quantity + " = ₹" + cost);
        }

        System.out.println("Total Amount: ₹" + total);
        System.out.println("Thank you for shopping!");

        cart.clear();
    }
}
