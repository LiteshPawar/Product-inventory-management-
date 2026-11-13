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

    void display() {
        System.out.println("ID: " + id + ", Name: " +
        name + ", Price: " + price);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<Product> list = new ArrayList<>();
        int ch;

        do {
            System.out.println("\n--- Product Inventory Management ---");
            System.out.println("1. Add Product");
            System.out.println("2. Update Product Price");
            System.out.println("3. Remove Product");
            System.out.println("4. Display Products");
            System.out.println("5. Sort by Price");
            System.out.println("6. Sort by Name");
            System.out.println("7. Exit");

            System.out.print("Enter your choice: ");
            ch = sc.nextInt();

            switch(ch) {
                case 1:
                    System.out.print("Enter Product ID: ");
                    int id = sc.nextInt();
                    sc.nextLine();

                    System.out.print("Enter Product Name: ");
                    String name = sc.nextLine();

                    System.out.print("Enter Product Price: ");
                    double price = sc.nextDouble();

                    list.add(new Product(id, name, price));
                    System.out.println("Product added successfully.");
                    break;

                case 2:
                    System.out.print("Enter Product ID to update: ");
                    id = sc.nextInt();
                    boolean found = false;

                    for(Product p : list) {
                        if(p.id == id) {
                            System.out.print("Enter new price: ");
                            p.price = sc.nextDouble();
                            System.out.println("Price updated successfully.");
                            found = true;
                            break;
                        }
                    }
                    if(!found)
                        System.out.println("Product not found.");
                    break;

                case 3:
                    System.out.print("Enter Product ID to remove: ");
                    id = sc.nextInt();
                    found = list.removeIf(p -> p.id == id);

                    System.out.println(found ?
                    "Product removed successfully." : "Product not found.");
                    break;

                case 4:
                    for(Product p : list)
                        p.display();
                    break;

                case 5:
                    list.sort(Comparator.comparingDouble(p -> p.price));
                    System.out.println("Products sorted by price.");
                    for(Product p : list)
                        p.display();
                    break;

                case 6:
                    list.sort(Comparator.comparing(p -> p.name,
                    String.CASE_INSENSITIVE_ORDER));
                    System.out.println("Products sorted by name.");
                    for(Product p : list)
                        p.display();
                    break;

                case 7:
                    System.out.println("Exiting program.");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }
        } while(ch != 7);

        sc.close();
    }
}
