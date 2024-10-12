```
Program ini membuat sistem CRUD (Create, Read, Update, Delete) untuk mengelola data SPBU. Kita dapat membuat, membaca, mengubah, dan menghapus data SPBU menggunakan menu yang disediakan. Program ini menggunakan inheritance, encapsulation, abstraction, dan interface untuk membuat sistem yang fleksibel dan mudah dipahami.
```
Kodingan
```
package com.spbu.shell;

/**
 *
 * @author nuNox
 */
public final class SPBU {
    private String name;
    private String address;
    private int capacity;

    public SPBU(String name, String address, int capacity) {
        this.name = name;
        this.address = address;
        this.capacity = capacity;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public int getCapacity() {
        return capacity;
    }

    public void setCapacity(int capacity) {
        this.capacity = capacity;
    }

    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Address: " + address);
        System.out.println("Capacity: " + capacity);
    }
}
```

```
package com.spbu.shell;

/**
 *
 * @author nuNox
 */
import java.util.ArrayList;

public final class SPBUManager {
    private final ArrayList<SPBU> spbuList;

    public SPBUManager() {
        this.spbuList = new ArrayList<>();
    }

    public void addSPBU(SPBU spbu) {
        spbuList.add(spbu);
    }

    public void removeSPBU(SPBU spbu) {
        spbuList.remove(spbu);
    }

    public void displayAllSPBU() {
        for (SPBU spbu : spbuList) {
            spbu.displayInfo();
        }
    }

    public ArrayList<SPBU> getSpbuList() {
        return spbuList;
    }

    public static void mainMenu() {
        System.out.println("Main Menu:");
        System.out.println("1. Create SPBU");
        System.out.println("2. Read SPBU");
        System.out.println("3. Update SPBU");
        System.out.println("4. Delete SPBU");
        System.out.println("5. Exit");
    }

    public static int getChoice() {
        int choice;
        System.out.print("Enter your choice: ");
        choice = Integer.parseInt(System.console().readLine());
        return choice;
    }

    public SPBU getSPBUByName(String name) {
        throw new UnsupportedOperationException("Not supported yet."); // Generated from nbfs://nbhost/SystemFileSystem/Templates/Classes/Code/GeneratedMethodBody
    }
}
```

```
package com.spbu.shell.crud;

/**
 *
 * @author nuNox
 */
public interface CRUD {
    void create();
    void read();
    void update();
    void delete();
}
```

```
package com.spbu.shell.crud;

/**
 *
 * @author nuNox
 */
import com.spbu.shell.SPBUManager;

public final class Main {
    public static void main(String[] args) {
        SPBUManager spbuManager = new SPBUManager();
        ShellCRUD shellCRUD = new ShellCRUD(spbuManager);
        shellCRUD.run();
    }
}
```

```
package com.spbu.shell.crud;

/**
 *
 * @author nuNox
 */
import com.spbu.shell.SPBU;
import com.spbu.shell.SPBUManager;
import java.util.Scanner;

public final class SPBU_CRUD implements CRUD {
    private final SPBUManager spbuManager;

    public SPBU_CRUD(SPBUManager spbuManager) {
        this.spbuManager = spbuManager;
    }

    @Override
    public void create() {
        SPBU spbu = new SPBU("SPBU 1", "Jalan Raya", 1000);
        spbuManager.addSPBU(spbu);
    }

    @Override
    public void read() {
        spbuManager.displayAllSPBU();
    }

    @Override
    public void update() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the name of the SPBU to update: ");
        String name = scanner.nextLine();
        SPBU spbuToUpdate = spbuManager.getSPBUByName(name);
        if (spbuToUpdate != null) {
            System.out.print("Enter the new address: ");
            String newAddress = scanner.nextLine();
            System.out.print("Enter the new capacity: ");
            int newCapacity = scanner.nextInt();
            spbuToUpdate.setAddress(newAddress);
            spbuToUpdate.setCapacity(newCapacity);
            System.out.println("SPBU updated successfully!");
        } else {
            System.out.println("SPBU not found!");
        }
    }

    @Override
    public void delete() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the name of the SPBU to delete: ");
        String name = scanner.nextLine();
        SPBU spbuToDelete = spbuManager.getSPBUByName(name);
        if (spbuToDelete != null) {
            spbuManager.removeSPBU(spbuToDelete);
            System.out.println("SPBU deleted successfully!");
        } else {
            System.out.println("SPBU not found!");
        }
    }
}
```

```
package com.spbu.shell.crud;

/**
 *
 * @author nuNox
 */
import com.spbu.shell.SPBU;
import com.spbu.shell.SPBUManager;

import java.util.Scanner;

public final class ShellCRUD implements CRUD {
    private final SPBUManager spbuManager;
    private final Scanner scanner;

    public ShellCRUD(SPBUManager spbuManager) {
        this.spbuManager = spbuManager;
        this.scanner = new Scanner(System.in);
    }

    @Override
    public void create() {
        System.out.print("Enter SPBU name: ");
        String name = scanner.nextLine();
        System.out.print("Enter SPBU address: ");
        String address = scanner.nextLine();
        System.out.print("Enter SPBU capacity: ");
        int capacity = scanner.nextInt();
        scanner.nextLine(); 

        SPBU spbu = new SPBU(name, address, capacity);
        spbuManager.addSPBU(spbu);
    }

    @Override
    public void read() {
        spbuManager.displayAllSPBU();
    }

    @Override
    public void update() {
        System.out.print("Enter SPBU name to update: ");
        String name = scanner.nextLine();
        for (SPBU spbu : spbuManager.getSpbuList()) {
            if (spbu.getName().equals(name)) {
                System.out.print("Enter new SPBU name: ");
                String newName = scanner.nextLine();
                System.out.print("Enter new SPBU address: ");
                String newAddress = scanner.nextLine();
                System.out.print("Enter new SPBU capacity: ");
                int newCapacity = scanner.nextInt();
                scanner.nextLine(); // Consume newline left-over

                spbu.setName(newName);
                spbu.setAddress(newAddress);
                spbu.setCapacity(newCapacity);
                System.out.println("SPBU updated successfully!");
                return;
            }
        }
        System.out.println("SPBU not found!");
    }

    @Override
    public void delete() {
        System.out.print("Enter SPBU name to delete: ");
        String name = scanner.nextLine();
        for (SPBU spbu : spbuManager.getSpbuList()) {
            if (spbu.getName().equals(name)) {
                spbuManager.removeSPBU(spbu);
                System.out.println("SPBU deleted successfully!");
                return;
            }
        }
        System.out.println("SPBU not found!");
    }

    public void run() {
        int choice;
        do {
            SPBUManager.mainMenu();
            choice = SPBUManager.getChoice();
            switch (choice) {
                case 1 -> create();
                case 2 -> read();
                case 3 -> update();
                case 4 -> delete();
                case 5 -> System.out.println("Exiting...");
                default -> System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
    }
}
```
Cara Kerja Program
```
Langkah 1: Membuat Instance SPBUManager dan ShellCRUD

- Program memulai dengan membuat instance SPBUManager dan ShellCRUD.
- Instance SPBUManager bertanggung jawab untuk mengelola daftar objek SPBU.
- Instance ShellCRUD bertanggung jawab untuk berinteraksi dengan pengguna dan melakukan operasi CRUD.
```
```
Langkah 2: Menampilkan Menu Utama

Program menampilkan menu utama yang berisi opsi-opsi seperti:
- Create SPBU
- Read SPBU
- Update SPBU
- Delete SPBU
- Exit
```
```
Langkah 3: Memilih Opsi

- Pengguna memilih opsi yang diinginkan dari menu utama.
- Berdasarkan pilihan pengguna, program akan melakukan operasi CRUD yang sesuai.
```
```
Langkah 4: Operasi CRUD

Create SPBU:
- Program meminta pengguna untuk memasukkan nama, alamat, dan kapasitas SPBU baru.
- Program membuat objek SPBU baru dengan nilai-nilai yang dimasukkan pengguna.
- Program menambahkan objek SPBU baru ke daftar objek SPBU yang dikelola oleh SPBUManager.

Read SPBU:
- Program menampilkan semua objek SPBU yang ada di daftar objek SPBU yang dikelola oleh SPBUManager.
- Program mencetak detail setiap objek SPBU menggunakan metode displayInfo().

Update SPBU:
- Program meminta pengguna untuk memasukkan nama SPBU yang ingin diupdate.
- Program mencari objek SPBU yang sesuai dengan nama yang dimasukkan pengguna.
- Program meminta pengguna untuk memasukkan nilai-nilai baru untuk objek SPBU yang diupdate.
- Program memperbarui objek SPBU yang diupdate dengan nilai-nilai baru.

Delete SPBU:
- Program meminta pengguna untuk memasukkan nama SPBU yang ingin dihapus.
- Program mencari objek SPBU yang sesuai dengan nama yang dimasukkan pengguna.
- Program menghapus objek SPBU yang dihapus dari daftar objek SPBU yang dikelola oleh SPBUManager.
```
```
Langkah 5: Keluar dari Program

- Pengguna memilih opsi Exit untuk keluar dari program.
- Program menampilkan pesan "Exiting..." dan kemudian keluar dari program.
```
```
Berikut adalah class diagram dari program ini:

- SPBU: Kelas ini merepresentasikan data SPBU yang terdiri dari nama, alamat, dan kapasitas.
- SPBUManager: Kelas ini merepresentasikan manajer SPBU yang dapat melakukan operasi CRUD pada data SPBU.
- CRUD: Interface ini merepresentasikan operasi CRUD yang dapat dilakukan pada data SPBU.
- SPBU_CRUD: Kelas ini merepresentasikan implementasi operasi CRUD pada data SPBU.
- ShellCRUD: Kelas ini merepresentasikan implementasi operasi CRUD pada data SPBU menggunakan shell.
```
```
Inheritance

Dalam program ini, kita menggunakan inheritance untuk membuat subclass SPBU_CRUD dan ShellCRUD yang mengextends interface CRUD. Ini memungkinkan kita untuk membuat objek yang dapat melakukan operasi CRUD pada data SPBU.
```
```
Encapsulation

Kita menggunakan encapsulation untuk menyembunyikan data SPBU dan membuatnya tidak dapat diakses langsung dari luar. Kita menggunakan getter dan setter untuk mengakses dan mengubah data SPBU. Contohnya, kita menggunakan getName() dan setName() untuk mengakses dan mengubah nama SPBU.
```
```
Abstraction

Kita menggunakan abstraction untuk membuat interface CRUD yang dapat diimplementasikan oleh subclass SPBU_CRUD dan ShellCRUD. Ini memungkinkan kita untuk membuat objek yang dapat melakukan operasi CRUD tanpa perlu mengetahui implementasi detailnya.
```
```
Interface

Kita menggunakan interface CRUD untuk membuat objek yang dapat melakukan operasi CRUD. Interface ini memiliki method create(), read(), update(), dan delete() yang dapat diimplementasikan oleh subclass.
```
```
Final Keyword

Kita menggunakan final keyword untuk membuat properti yang tidak dapat diubah setelah diinisialisasi. Contohnya, kita menggunakan private final ArrayList<SPBU> spbuList; untuk membuat list SPBU yang tidak dapat diubah setelah diinisialisasi.
```

