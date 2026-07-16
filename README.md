# quiz2
// คลาส Book สำหรับเก็บข้อมูลของหนังสือแต่ละเล่ม
class Book {
    private isbn: string;
    private title: string;
    private author: string;
    private price: number;

    constructor(isbn: string, title: string, author: string, price: number) {
        this.isbn = isbn;
        this.title = title;
        this.author = author;
        this.price = price;
    }

    // Public Getter Methods เพื่อให้คลาสภายนอกสามารถเข้าถึงข้อมูลที่จำเป็นได้
    public getIsbn(): string {
        return this.isbn;
    }

    public getTitle(): string {
        return this.title;
    }

    public getAuthor(): string {
        return this.author;
    }

    public getPrice(): number {
        return this.price;
    }
}

// คลาส Cart สำหรับจัดการข้อมูลตะกร้าสินค้า
class Cart {
    private cartId: string;
    private books: Book[]; // กำหนดรูปแบบเป็น Array ของ Class Book

    constructor(cartId: string) {
        this.cartId = cartId;
        this.books = []; // เริ่มต้นโดยให้เป็นตะกร้าว่างเปล่า
    }

    // เมธอดสำหรับเพิ่มวัตถุ Book เข้ามาในตะกร้า
    public addBook(book: Book): void {
        this.books.push(book);
    }

    // เมธอดสำหรับคำนวณผลรวมราคาสินค้าทั้งหมดในตะกร้า
    public getTotalPrice(): number {
        return this.books.reduce((total, book) => total + book.getPrice(), 0);
    }

    // เมธอดสำหรับแสดงใบเสร็จรับเงินตามโครงสร้างผลลัพธ์ที่คาดหวัง
    public getInfo(): void {
        console.log("=== ใบเสร็จรับเงิน ===");
        console.log(`รหัสตะกร้า: ${this.cartId}`);
        console.log("รายการ:");
        this.books.forEach(book => {
            console.log(`- ${book.getTitle()} (${book.getIsbn()}): ${book.getPrice()} บาท`);
        });
        console.log(`ราคารวม: ${this.getTotalPrice()} บาท`);
    }
}

// --- ส่วนการสร้าง Object และจำลองการทำงาน (Main Execution) ---

// 1. สร้าง Object หนังสือตามข้อมูลโจทย์กำหนด
const book1 = new Book("978-0132350884", "Clean Code", "Robert C. Martin", 450);
const book2 = new Book("978-1234567890", "TypeScript Deep Dive", "Basarat Ali Syed", 320);

// 2. สร้าง Object ตะกร้าสินค้า
const cart = new Cart("CO01");

// 3. หยิบหนังสือใส่ตะกร้าสินค้า
cart.addBook(book1);
cart.addBook(book2);

// 4. แสดงผลลัพธ์ใบเสร็จรับเงินออกทางหน้าจอ
cart.getInfo();
