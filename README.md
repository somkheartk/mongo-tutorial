# MongoDB Tutorial - สอน MongoDB ตั้งแต่เริ่มต้นจน Advanced

คู่มือสอน MongoDB แบบครบวงจร จากพื้นฐานจนถึงระดับสูง | Complete MongoDB Tutorial from Beginner to Advanced

## 📚 สารบัญ (Table of Contents)

1. [เริ่มต้นกับ MongoDB (Getting Started)](#1-เริ่มต้นกับ-mongodb)
2. [การติดตั้ง (Installation)](#2-การติดตั้ง-installation)
3. [พื้นฐาน MongoDB (MongoDB Basics)](#3-พื้นฐาน-mongodb-basics)
4. [การจัดการข้อมูล (CRUD Operations)](#4-การจัดการข้อมูล-crud-operations)
5. [การค้นหาข้อมูล (Querying Data)](#5-การค้นหาข้อมูล-querying-data)
6. [Aggregation Framework](#6-aggregation-framework)
7. [Indexing และ Performance](#7-indexing-และ-performance)
8. [Data Modeling](#8-data-modeling)
9. [Replication](#9-replication)
10. [Sharding](#10-sharding)
11. [Security](#11-security)
12. [Best Practices](#12-best-practices)

---

## 1. เริ่มต้นกับ MongoDB

### MongoDB คืออะไร? (What is MongoDB?)

MongoDB เป็นฐานข้อมูลแบบ NoSQL (Not Only SQL) ที่จัดเก็บข้อมูลในรูปแบบของ Document (เอกสาร) โดยใช้รูปแบบคล้าย JSON ที่เรียกว่า BSON (Binary JSON)

**ข้อดีของ MongoDB:**
- ✅ ความยืดหยุ่นในการจัดเก็บข้อมูล (Flexible Schema)
- ✅ Scalability แนวนอน (Horizontal Scaling)
- ✅ Performance สูงในการอ่านและเขียนข้อมูล
- ✅ รองรับข้อมูลที่มีโครงสร้างซับซ้อน
- ✅ ง่ายต่อการใช้งานกับ Modern Applications

**โครงสร้างข้อมูลใน MongoDB:**
```
Database (ฐานข้อมูล)
  └── Collection (คอลเลกชัน - เทียบเท่ากับ Table)
      └── Document (เอกสาร - เทียบเท่ากับ Row)
          └── Field (ฟิลด์ - เทียบเท่ากับ Column)
```

---

## 2. การติดตั้ง (Installation)

### 2.1 ติดตั้ง MongoDB Community Edition

#### Windows:
```bash
# ดาวน์โหลดตัวติดตั้งจาก:
https://www.mongodb.com/try/download/community

# หรือใช้ chocolatey:
choco install mongodb
```

#### macOS:
```bash
# ใช้ Homebrew:
brew tap mongodb/brew
brew install mongodb-community

# เริ่มต้น MongoDB:
brew services start mongodb-community
```

#### Linux (Ubuntu/Debian):
```bash
# Import MongoDB public GPG Key:
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

# เพิ่ม MongoDB repository:
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# อัปเดตและติดตั้ง:
sudo apt-get update
sudo apt-get install -y mongodb-org

# เริ่มต้น MongoDB:
sudo systemctl start mongod
sudo systemctl enable mongod
```

### 2.2 ติดตั้ง MongoDB Shell (mongosh)

```bash
# ดาวน์โหลดจาก:
https://www.mongodb.com/try/download/shell

# หรือใช้ npm:
npm install -g mongosh
```

### 2.3 ติดตั้ง MongoDB Compass (GUI Tool)

ดาวน์โหลดจาก: https://www.mongodb.com/try/download/compass

---

## 3. พื้นฐาน MongoDB (MongoDB Basics)

### 3.1 เชื่อมต่อกับ MongoDB

```bash
# เชื่อมต่อกับ MongoDB บน localhost:
mongosh

# เชื่อมต่อกับ MongoDB บนเซิร์ฟเวอร์อื่น:
mongosh "mongodb://username:password@host:port/database"

# เชื่อมต่อกับ MongoDB Atlas:
mongosh "mongodb+srv://username:password@cluster.mongodb.net/database"
```

### 3.2 คำสั่งพื้นฐาน (Basic Commands)

```javascript
// แสดงฐานข้อมูลทั้งหมด
show dbs

// สร้างหรือเปลี่ยนไปใช้ฐานข้อมูล
use myDatabase

// แสดง collection ทั้งหมด
show collections

// แสดงฐานข้อมูลปัจจุบัน
db

// ลบฐานข้อมูล
db.dropDatabase()

// สร้าง collection
db.createCollection("users")

// ลบ collection
db.users.drop()
```

---

## 4. การจัดการข้อมูล (CRUD Operations)

### 4.1 Create - การเพิ่มข้อมูล

```javascript
// เพิ่มเอกสารเดียว (Insert One Document)
db.users.insertOne({
  name: "John Doe",
  email: "john@example.com",
  age: 30,
  address: {
    street: "123 Main St",
    city: "Bangkok",
    country: "Thailand"
  },
  hobbies: ["reading", "coding", "travel"],
  createdAt: new Date()
})

// เพิ่มหลายเอกสาร (Insert Many Documents)
db.users.insertMany([
  {
    name: "Jane Smith",
    email: "jane@example.com",
    age: 25,
    role: "developer"
  },
  {
    name: "Bob Johnson",
    email: "bob@example.com",
    age: 35,
    role: "manager"
  }
])

// ตัวอย่างการเพิ่มข้อมูล Products
db.products.insertMany([
  {
    name: "Laptop",
    brand: "Dell",
    price: 25000,
    stock: 50,
    categories: ["electronics", "computers"],
    specifications: {
      cpu: "Intel i7",
      ram: "16GB",
      storage: "512GB SSD"
    }
  },
  {
    name: "Smartphone",
    brand: "Samsung",
    price: 15000,
    stock: 100,
    categories: ["electronics", "mobile"]
  }
])
```

### 4.2 Read - การอ่านข้อมูล

```javascript
// ค้นหาเอกสารทั้งหมด
db.users.find()

// ค้นหาเอกสารทั้งหมด (แสดงผลแบบสวยงาม)
db.users.find().pretty()

// ค้นหาเอกสารตามเงื่อนไข
db.users.find({ age: 30 })

// ค้นหาเอกสารแรกที่ตรงเงื่อนไข
db.users.findOne({ name: "John Doe" })

// ค้นหาเอกสารโดยใช้ _id
db.users.findOne({ _id: ObjectId("...") })

// เลือกเฉพาะฟิลด์ที่ต้องการ (Projection)
db.users.find({}, { name: 1, email: 1, _id: 0 })

// จำกัดจำนวนผลลัพธ์
db.users.find().limit(10)

// ข้ามผลลัพธ์ (Pagination)
db.users.find().skip(10).limit(10)

// เรียงลำดับผลลัพธ์ (1 = ascending, -1 = descending)
db.users.find().sort({ age: -1 })

// นับจำนวนเอกสาร
db.users.countDocuments()
db.users.countDocuments({ age: { $gte: 25 } })
```

### 4.3 Update - การแก้ไขข้อมูล

```javascript
// แก้ไขเอกสารเดียว
db.users.updateOne(
  { name: "John Doe" },
  { $set: { age: 31, email: "john.doe@example.com" } }
)

// แก้ไขหลายเอกสาร
db.users.updateMany(
  { age: { $lt: 30 } },
  { $set: { status: "young" } }
)

// เพิ่มค่าในฟิลด์ที่เป็นตัวเลข
db.users.updateOne(
  { name: "John Doe" },
  { $inc: { age: 1 } }
)

// เพิ่มสมาชิกใน array
db.users.updateOne(
  { name: "John Doe" },
  { $push: { hobbies: "swimming" } }
)

// เพิ่มหลายสมาชิกใน array
db.users.updateOne(
  { name: "John Doe" },
  { $push: { hobbies: { $each: ["gaming", "cooking"] } } }
)

// ลบสมาชิกจาก array
db.users.updateOne(
  { name: "John Doe" },
  { $pull: { hobbies: "reading" } }
)

// แก้ไขหรือเพิ่มถ้าไม่พบ (Upsert)
db.users.updateOne(
  { email: "new@example.com" },
  { $set: { name: "New User", age: 28 } },
  { upsert: true }
)

// แทนที่เอกสารทั้งหมด
db.users.replaceOne(
  { name: "John Doe" },
  {
    name: "John Doe",
    email: "john.new@example.com",
    age: 32
  }
)
```

### 4.4 Delete - การลบข้อมูล

```javascript
// ลบเอกสารเดียว
db.users.deleteOne({ name: "John Doe" })

// ลบหลายเอกสาร
db.users.deleteMany({ age: { $lt: 25 } })

// ลบเอกสารทั้งหมดใน collection
db.users.deleteMany({})
```

---

## 5. การค้นหาข้อมูล (Querying Data)

### 5.1 Query Operators

#### Comparison Operators

```javascript
// $eq (equal)
db.products.find({ price: { $eq: 25000 } })

// $ne (not equal)
db.products.find({ brand: { $ne: "Dell" } })

// $gt (greater than), $gte (greater than or equal)
db.products.find({ price: { $gt: 20000 } })
db.products.find({ stock: { $gte: 50 } })

// $lt (less than), $lte (less than or equal)
db.products.find({ price: { $lt: 20000 } })
db.products.find({ stock: { $lte: 100 } })

// $in (in array)
db.products.find({ brand: { $in: ["Dell", "HP", "Lenovo"] } })

// $nin (not in array)
db.products.find({ brand: { $nin: ["Dell", "HP"] } })
```

#### Logical Operators

```javascript
// $and
db.products.find({
  $and: [
    { price: { $gte: 10000 } },
    { price: { $lte: 30000 } }
  ]
})

// สั้นกว่า (implicit AND)
db.products.find({
  price: { $gte: 10000, $lte: 30000 }
})

// $or
db.products.find({
  $or: [
    { brand: "Dell" },
    { brand: "HP" }
  ]
})

// $nor (not or)
db.products.find({
  $nor: [
    { price: { $lt: 10000 } },
    { stock: { $lt: 10 } }
  ]
})

// $not
db.products.find({
  price: { $not: { $gt: 30000 } }
})
```

#### Element Operators

```javascript
// $exists (ตรวจสอบว่ามีฟิลด์หรือไม่)
db.products.find({ discount: { $exists: true } })

// $type (ตรวจสอบชนิดข้อมูล)
db.products.find({ price: { $type: "number" } })
db.products.find({ price: { $type: ["int", "double"] } })
```

#### Array Operators

```javascript
// $all (มีสมาชิกทั้งหมดใน array)
db.products.find({ categories: { $all: ["electronics", "computers"] } })

// $elemMatch (มีสมาชิกที่ตรงเงื่อนไข)
db.orders.find({
  items: {
    $elemMatch: {
      price: { $gte: 100 },
      quantity: { $gte: 2 }
    }
  }
})

// $size (ขนาดของ array)
db.products.find({ categories: { $size: 2 } })
```

#### String Operators

```javascript
// $regex (Regular Expression)
db.users.find({ name: { $regex: /^John/i } })
db.users.find({ email: { $regex: /@example\.com$/ } })

// ค้นหาแบบ case-insensitive
db.users.find({ name: { $regex: "john", $options: "i" } })
```

### 5.2 การค้นหาใน Nested Documents

```javascript
// ค้นหาใน embedded document
db.users.find({ "address.city": "Bangkok" })

// ค้นหาหลายฟิลด์ใน embedded document
db.users.find({
  "address.city": "Bangkok",
  "address.country": "Thailand"
})
```

### 5.3 Text Search

```javascript
// สร้าง text index
db.articles.createIndex({ title: "text", content: "text" })

// ค้นหาด้วย text search
db.articles.find({ $text: { $search: "mongodb tutorial" } })

// ค้นหาวลีที่แน่นอน
db.articles.find({ $text: { $search: "\"mongodb atlas\"" } })

// ยกเว้นคำบางคำ
db.articles.find({ $text: { $search: "mongodb -atlas" } })
```

---

## 6. Aggregation Framework

Aggregation Framework เป็นเครื่องมือที่ทรงพลังสำหรับการประมวลผลและวิเคราะห์ข้อมูล

### 6.1 พื้นฐาน Aggregation

```javascript
// โครงสร้างพื้นฐาน
db.collection.aggregate([
  { $stage1: { ... } },
  { $stage2: { ... } },
  { $stage3: { ... } }
])

// ตัวอย่าง: คำนวณราคาเฉลี่ยของสินค้า
db.products.aggregate([
  {
    $group: {
      _id: null,
      averagePrice: { $avg: "$price" }
    }
  }
])
```

### 6.2 Aggregation Stages

#### $match - กรองข้อมูล

```javascript
db.orders.aggregate([
  {
    $match: {
      status: "completed",
      total: { $gte: 1000 }
    }
  }
])
```

#### $group - จัดกลุ่มข้อมูล

```javascript
// จัดกลุ่มตาม brand และนับจำนวน
db.products.aggregate([
  {
    $group: {
      _id: "$brand",
      count: { $sum: 1 },
      totalStock: { $sum: "$stock" },
      avgPrice: { $avg: "$price" },
      minPrice: { $min: "$price" },
      maxPrice: { $max: "$price" }
    }
  }
])

// จัดกลุ่มตามหลายฟิลด์
db.orders.aggregate([
  {
    $group: {
      _id: {
        year: { $year: "$orderDate" },
        month: { $month: "$orderDate" }
      },
      totalSales: { $sum: "$total" },
      orderCount: { $sum: 1 }
    }
  }
])
```

#### $project - เลือกและแปลงฟิลด์

```javascript
db.users.aggregate([
  {
    $project: {
      _id: 0,
      name: 1,
      email: 1,
      fullAddress: {
        $concat: [
          "$address.street", ", ",
          "$address.city", ", ",
          "$address.country"
        ]
      },
      ageCategory: {
        $cond: {
          if: { $gte: ["$age", 30] },
          then: "Adult",
          else: "Young"
        }
      }
    }
  }
])
```

#### $sort - เรียงลำดับ

```javascript
db.products.aggregate([
  { $sort: { price: -1, name: 1 } }
])
```

#### $limit และ $skip - จำกัดและข้ามผลลัพธ์

```javascript
db.products.aggregate([
  { $sort: { price: -1 } },
  { $skip: 10 },
  { $limit: 10 }
])
```

#### $unwind - แยก array

```javascript
// ข้อมูลต้นฉบับ:
// { _id: 1, name: "John", hobbies: ["reading", "coding"] }

db.users.aggregate([
  { $unwind: "$hobbies" }
])

// ผลลัพธ์:
// { _id: 1, name: "John", hobbies: "reading" }
// { _id: 1, name: "John", hobbies: "coding" }
```

#### $lookup - Join collections

```javascript
// เหมือน SQL JOIN
db.orders.aggregate([
  {
    $lookup: {
      from: "customers",
      localField: "customerId",
      foreignField: "_id",
      as: "customerInfo"
    }
  }
])

// Lookup with pipeline (advanced)
db.orders.aggregate([
  {
    $lookup: {
      from: "products",
      let: { productIds: "$items.productId" },
      pipeline: [
        {
          $match: {
            $expr: { $in: ["$_id", "$$productIds"] }
          }
        }
      ],
      as: "productDetails"
    }
  }
])
```

#### $addFields - เพิ่มฟิลด์ใหม่

```javascript
db.products.aggregate([
  {
    $addFields: {
      totalValue: { $multiply: ["$price", "$stock"] },
      discountedPrice: {
        $subtract: ["$price", { $multiply: ["$price", 0.1] }]
      }
    }
  }
])
```

### 6.3 ตัวอย่าง Aggregation แบบซับซ้อน

```javascript
// วิเคราะห์ยอดขายรายเดือน
db.orders.aggregate([
  // 1. กรองเฉพาะปีปัจจุบัน
  {
    $match: {
      orderDate: {
        $gte: new Date("2024-01-01"),
        $lt: new Date("2025-01-01")
      },
      status: "completed"
    }
  },
  // 2. แยก items ออกจาก array
  {
    $unwind: "$items"
  },
  // 3. เพิ่มฟิลด์คำนวณ
  {
    $addFields: {
      itemTotal: { $multiply: ["$items.price", "$items.quantity"] }
    }
  },
  // 4. จัดกลุ่มตามเดือน
  {
    $group: {
      _id: {
        year: { $year: "$orderDate" },
        month: { $month: "$orderDate" }
      },
      totalSales: { $sum: "$itemTotal" },
      orderCount: { $sum: 1 },
      avgOrderValue: { $avg: "$itemTotal" }
    }
  },
  // 5. เรียงลำดับ
  {
    $sort: { "_id.year": 1, "_id.month": 1 }
  },
  // 6. จัดรูปแบบผลลัพธ์
  {
    $project: {
      _id: 0,
      year: "$_id.year",
      month: "$_id.month",
      totalSales: { $round: ["$totalSales", 2] },
      orderCount: 1,
      avgOrderValue: { $round: ["$avgOrderValue", 2] }
    }
  }
])
```

---

## 7. Indexing และ Performance

### 7.1 ทำไมต้องใช้ Index?

Index ช่วยให้การค้นหาข้อมูลเร็วขึ้นมาก โดยไม่ต้องสแกนทุก document (Collection Scan)

### 7.2 ประเภทของ Index

#### Single Field Index

```javascript
// สร้าง index สำหรับฟิลด์เดียว
db.users.createIndex({ email: 1 })  // 1 = ascending, -1 = descending

// สร้าง unique index
db.users.createIndex({ email: 1 }, { unique: true })

// index สำหรับ nested field
db.users.createIndex({ "address.city": 1 })
```

#### Compound Index

```javascript
// สร้าง index สำหรับหลายฟิลด์
db.products.createIndex({ brand: 1, price: -1 })

// ลำดับของฟิลด์ใน compound index มีความสำคัญ
// index { brand: 1, price: -1 } จะช่วย:
// ✅ { brand: "Dell" }
// ✅ { brand: "Dell", price: { $gte: 20000 } }
// ❌ { price: { $gte: 20000 } }  // ไม่ได้ใช้ index อย่างเต็มประสิทธิภาพ
```

#### Text Index

```javascript
// สร้าง text index
db.articles.createIndex({ title: "text", content: "text" })

// text index พร้อม weight
db.articles.createIndex(
  { title: "text", content: "text" },
  { weights: { title: 10, content: 5 } }
)
```

#### Geospatial Index

```javascript
// สร้าง 2dsphere index สำหรับข้อมูลตำแหน่ง
db.places.createIndex({ location: "2dsphere" })

// ค้นหาสถานที่ใกล้เคียง
db.places.find({
  location: {
    $near: {
      $geometry: {
        type: "Point",
        coordinates: [100.5018, 13.7563]  // Bangkok
      },
      $maxDistance: 5000  // 5 km
    }
  }
})
```

#### Wildcard Index

```javascript
// สร้าง wildcard index สำหรับทุกฟิลด์
db.products.createIndex({ "$**": 1 })

// wildcard index สำหรับ embedded documents
db.products.createIndex({ "specifications.$**": 1 })
```

### 7.3 การจัดการ Index

```javascript
// แสดง index ทั้งหมด
db.users.getIndexes()

// ลบ index
db.users.dropIndex("email_1")
db.users.dropIndex({ email: 1 })

// ลบ index ทั้งหมด (ยกเว้น _id)
db.users.dropIndexes()

// ตรวจสอบขนาด index
db.users.stats()
```

### 7.4 Explain Plan - วิเคราะห์ Query Performance

```javascript
// แสดงแผนการทำงานของ query
db.users.find({ email: "john@example.com" }).explain("executionStats")

// ข้อมูลสำคัญใน explain output:
// - executionTimeMillis: เวลาที่ใช้ในการทำงาน
// - totalDocsExamined: จำนวน document ที่ตรวจสอบ
// - totalKeysExamined: จำนวน index key ที่ตรวจสอบ
// - stage: วิธีการทำงาน (IXSCAN = ใช้ index, COLLSCAN = scan ทั้ง collection)

// ตัวอย่างผลลัพธ์ที่ดี:
// - stage: "IXSCAN" (ใช้ index)
// - totalDocsExamined ≈ nReturned (ไม่ต้องตรวจสอบเอกสารที่ไม่จำเป็น)
```

### 7.5 Performance Best Practices

```javascript
// 1. สร้าง index สำหรับ query ที่ใช้บ่อย
db.orders.createIndex({ customerId: 1, orderDate: -1 })

// 2. ใช้ projection เพื่อลดข้อมูลที่ส่งคืน
db.users.find({ age: { $gte: 25 } }, { name: 1, email: 1 })

// 3. จำกัดจำนวนผลลัพธ์
db.users.find().limit(100)

// 4. ใช้ covered query (query ที่ใช้เฉพาะข้อมูลจาก index)
db.users.createIndex({ email: 1, name: 1 })
db.users.find({ email: "john@example.com" }, { _id: 0, email: 1, name: 1 })

// 5. หลีกเลี่ยง $where และ $regex ที่ไม่มี anchor
// ❌ ช้า
db.users.find({ name: { $regex: /john/ } })
// ✅ เร็ว
db.users.find({ name: { $regex: /^john/ } })

// 6. ใช้ hint เพื่อบังคับให้ใช้ index ที่ต้องการ
db.users.find({ age: 30, city: "Bangkok" }).hint({ age: 1 })
```

---

## 8. Data Modeling

### 8.1 Embedded Documents vs References

#### Embedded Documents (Denormalization)

```javascript
// เหมาะสำหรับข้อมูลที่ใช้ร่วมกันบ่อย และมีความสัมพันธ์แบบ one-to-few
{
  _id: 1,
  name: "John Doe",
  address: {
    street: "123 Main St",
    city: "Bangkok",
    country: "Thailand"
  },
  orders: [
    {
      orderId: 1001,
      product: "Laptop",
      price: 25000,
      date: ISODate("2024-01-15")
    },
    {
      orderId: 1002,
      product: "Mouse",
      price: 500,
      date: ISODate("2024-02-20")
    }
  ]
}

// ข้อดี:
// ✅ อ่านข้อมูลได้ในครั้งเดียว (ไม่ต้อง join)
// ✅ Performance ดีกว่าในการอ่าน
// ✅ Atomic operations (update ทั้งหมดในครั้งเดียว)

// ข้อเสีย:
// ❌ ขนาด document อาจใหญ่เกินไป (มีขีดจำกัด 16MB)
// ❌ การอัปเดตข้อมูลซ้ำๆ ต้องอัปเดตหลายที่
```

#### References (Normalization)

```javascript
// Users Collection
{
  _id: ObjectId("..."),
  name: "John Doe",
  email: "john@example.com"
}

// Orders Collection
{
  _id: ObjectId("..."),
  userId: ObjectId("..."),
  products: [
    {
      productId: ObjectId("..."),
      quantity: 2,
      price: 25000
    }
  ],
  total: 50000,
  orderDate: ISODate("2024-01-15")
}

// Products Collection
{
  _id: ObjectId("..."),
  name: "Laptop",
  brand: "Dell",
  price: 25000
}

// ข้อดี:
// ✅ ไม่มีการซ้ำซ้อนของข้อมูล
// ✅ เหมาะกับความสัมพันธ์แบบ one-to-many หรือ many-to-many
// ✅ ง่ายต่อการอัปเดตข้อมูล

// ข้อเสีย:
// ❌ ต้องใช้ $lookup หรือ multiple queries
// ❌ Performance อาจช้ากว่า embedded documents
```

### 8.2 Design Patterns

#### Pattern 1: One-to-Few (Embedded)

```javascript
// เหมาะสำหรับข้อมูลที่มีจำนวนน้อยและไม่ค่อยเปลี่ยนแปลง
{
  _id: 1,
  name: "John Doe",
  emails: [
    "john@work.com",
    "john@personal.com"
  ],
  addresses: [
    { type: "home", street: "123 Main St", city: "Bangkok" },
    { type: "work", street: "456 Office Rd", city: "Bangkok" }
  ]
}
```

#### Pattern 2: One-to-Many (Reference)

```javascript
// Blog Posts Collection
{
  _id: ObjectId("post1"),
  title: "MongoDB Tutorial",
  content: "...",
  authorId: ObjectId("user1")
}

// Users Collection
{
  _id: ObjectId("user1"),
  name: "John Doe",
  email: "john@example.com"
}

// Comments Collection
{
  _id: ObjectId("comment1"),
  postId: ObjectId("post1"),
  userId: ObjectId("user1"),
  content: "Great post!",
  createdAt: ISODate("2024-01-15")
}
```

#### Pattern 3: Many-to-Many

```javascript
// Students Collection
{
  _id: ObjectId("student1"),
  name: "John Doe",
  courseIds: [
    ObjectId("course1"),
    ObjectId("course2")
  ]
}

// Courses Collection
{
  _id: ObjectId("course1"),
  title: "MongoDB Basics",
  studentIds: [
    ObjectId("student1"),
    ObjectId("student2")
  ]
}
```

#### Pattern 4: Computed Pattern

```javascript
// เก็บค่าที่คำนวณไว้เพื่อประสิทธิภาพ
{
  _id: ObjectId("product1"),
  name: "Laptop",
  reviews: [
    { rating: 5, comment: "Great!" },
    { rating: 4, comment: "Good" },
    { rating: 5, comment: "Excellent!" }
  ],
  // คำนวณและเก็บค่าไว้
  totalReviews: 3,
  averageRating: 4.67
}

// อัปเดตเมื่อมี review ใหม่
db.products.updateOne(
  { _id: ObjectId("product1") },
  {
    $push: { reviews: { rating: 5, comment: "Amazing!" } },
    $inc: { totalReviews: 1 },
    $set: { averageRating: 4.75 }  // คำนวณใหม่
  }
)
```

#### Pattern 5: Bucket Pattern

```javascript
// เหมาะสำหรับข้อมูล time-series หรือข้อมูลที่มีจำนวนมาก
// แทนที่จะเก็บ 1 document ต่อ 1 measurement
{
  _id: ObjectId("..."),
  sensorId: "sensor1",
  timestamp: ISODate("2024-01-15T10:00:00Z"),
  temperature: 25.5
}

// ใช้ bucket pattern เก็บหลาย measurements ใน 1 document
{
  _id: ObjectId("..."),
  sensorId: "sensor1",
  date: ISODate("2024-01-15"),
  measurements: [
    { time: "10:00", temp: 25.5 },
    { time: "10:01", temp: 25.6 },
    { time: "10:02", temp: 25.4 },
    // ... อีก 57 measurements
  ],
  count: 60
}
```

### 8.3 Schema Validation

```javascript
// กำหนดโครงสร้างข้อมูลด้วย JSON Schema
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email", "age"],
      properties: {
        name: {
          bsonType: "string",
          description: "must be a string and is required"
        },
        email: {
          bsonType: "string",
          pattern: "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$",
          description: "must be a valid email and is required"
        },
        age: {
          bsonType: "int",
          minimum: 0,
          maximum: 150,
          description: "must be an integer between 0 and 150"
        },
        status: {
          enum: ["active", "inactive", "pending"],
          description: "can only be one of the enum values"
        }
      }
    }
  }
})

// แก้ไข validation rule ของ collection ที่มีอยู่แล้ว
db.runCommand({
  collMod: "users",
  validator: {
    $jsonSchema: {
      // ... schema definition
    }
  },
  validationLevel: "moderate",  // "off", "strict", "moderate"
  validationAction: "error"     // "error", "warn"
})
```

---

## 9. Replication

Replication คือการทำสำเนาข้อมูลไปยังหลายเซิร์ฟเวอร์เพื่อความพร้อมใช้งานสูง (High Availability)

### 9.1 Replica Set คืออะไร?

Replica Set ประกอบด้วย:
- **Primary Node**: รับคำสั่ง write ทั้งหมด
- **Secondary Nodes**: คัดลอกข้อมูลจาก Primary และรับคำสั่ง read
- **Arbiter** (optional): ไม่เก็บข้อมูล แต่ช่วยในการเลือก Primary ใหม่

```
┌─────────────┐
│   Primary   │ ← write operations
└─────┬───────┘
      │ replicate
      ├──────────────┬──────────────┐
      ▼              ▼              ▼
┌───────────┐  ┌───────────┐  ┌───────────┐
│Secondary 1│  │Secondary 2│  │  Arbiter  │
└───────────┘  └───────────┘  └───────────┘
```

### 9.2 การตั้งค่า Replica Set

```bash
# 1. เริ่ม MongoDB instances (3 nodes)
mongod --replSet rs0 --port 27017 --dbpath /data/rs0-1
mongod --replSet rs0 --port 27018 --dbpath /data/rs0-2
mongod --replSet rs0 --port 27019 --dbpath /data/rs0-3

# 2. เชื่อมต่อกับ node แรก
mongosh --port 27017

# 3. กำหนดค่า replica set
rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "localhost:27017" },
    { _id: 1, host: "localhost:27018" },
    { _id: 2, host: "localhost:27019" }
  ]
})
```

### 9.3 คำสั่งจัดการ Replica Set

```javascript
// ตรวจสอบสถานะ
rs.status()

// ดูการตั้งค่า
rs.conf()

// เพิ่ม member
rs.add("localhost:27020")

// ลบ member
rs.remove("localhost:27020")

// เปลี่ยน priority (ค่าสูงมีโอกาสเป็น Primary มากกว่า)
cfg = rs.conf()
cfg.members[0].priority = 2
rs.reconfig(cfg)

// ตรวจสอบว่า node ไหนเป็น Primary
rs.isMaster()

// บังคับให้เกิด election ใหม่
rs.stepDown()
```

### 9.4 Read Preference

```javascript
// อ่านจาก Primary เท่านั้น (default)
db.users.find().readPref("primary")

// อ่านจาก Secondary ก่อน
db.users.find().readPref("secondary")

// อ่านจาก Primary ก่อน ถ้าไม่ได้ค่อยอ่านจาก Secondary
db.users.find().readPref("primaryPreferred")

// อ่านจาก Secondary ก่อน ถ้าไม่ได้ค่อยอ่านจาก Primary
db.users.find().readPref("secondaryPreferred")

// อ่านจาก node ที่ใกล้ที่สุด
db.users.find().readPref("nearest")
```

### 9.5 Write Concern

```javascript
// รอให้ Primary acknowledge เท่านั้น (default)
db.users.insertOne(
  { name: "John" },
  { writeConcern: { w: 1 } }
)

// รอให้ majority ของ nodes acknowledge
db.users.insertOne(
  { name: "John" },
  { writeConcern: { w: "majority", wtimeout: 5000 } }
)

// รอให้ทุก node acknowledge
db.users.insertOne(
  { name: "John" },
  { writeConcern: { w: 3 } }
)
```

---

## 10. Sharding

Sharding คือการแบ่งข้อมูลออกเป็นส่วนๆ (shards) เพื่อกระจายการทำงานและเพิ่ม capacity

### 10.1 สถาปัตยกรรมของ Sharded Cluster

```
┌─────────────────┐
│  Application    │
└────────┬────────┘
         │
    ┌────▼─────┐
    │  mongos  │  (Query Router)
    └────┬─────┘
         │
    ┌────┴──────────────┬──────────────┐
    ▼                   ▼              ▼
┌─────────┐       ┌─────────┐    ┌─────────┐
│ Shard 1 │       │ Shard 2 │    │ Shard 3 │
│(Replica │       │(Replica │    │(Replica │
│  Set)   │       │  Set)   │    │  Set)   │
└─────────┘       └─────────┘    └─────────┘

┌────────────────┐
│ Config Servers │  (Metadata)
│ (Replica Set)  │
└────────────────┘
```

### 10.2 การตั้งค่า Sharded Cluster

```bash
# 1. เริ่ม Config Servers
mongod --configsvr --replSet configRS --port 27019 --dbpath /data/configdb

# 2. เริ่ม Shards (แต่ละ shard เป็น replica set)
mongod --shardsvr --replSet shard1RS --port 27018 --dbpath /data/shard1
mongod --shardsvr --replSet shard2RS --port 27020 --dbpath /data/shard2

# 3. เริ่ม mongos (Query Router)
mongos --configdb configRS/localhost:27019 --port 27017

# 4. เชื่อมต่อกับ mongos และเพิ่ม shards
mongosh --port 27017
sh.addShard("shard1RS/localhost:27018")
sh.addShard("shard2RS/localhost:27020")
```

### 10.3 Shard Key

```javascript
// เปิดใช้งาน sharding สำหรับ database
sh.enableSharding("myDatabase")

// กำหนด shard key (ต้องมี index ก่อน)
db.users.createIndex({ userId: 1 })
sh.shardCollection("myDatabase.users", { userId: 1 })

// Compound shard key
db.orders.createIndex({ customerId: 1, orderDate: 1 })
sh.shardCollection("myDatabase.orders", { customerId: 1, orderDate: 1 })

// Hashed shard key (กระจายข้อมูลสม่ำเสมอ)
db.products.createIndex({ productId: "hashed" })
sh.shardCollection("myDatabase.products", { productId: "hashed" })
```

### 10.4 การเลือก Shard Key ที่ดี

Shard key ที่ดีควรมีคุณสมบัติ:

1. **High Cardinality**: มีค่าที่หลากหลายมาก
2. **Low Frequency**: แต่ละค่าไม่ปรากฏบ่อยเกินไป
3. **Non-Monotonic**: ไม่เป็นค่าที่เพิ่มขึ้นเรื่อยๆ (เช่น timestamp)

```javascript
// ❌ Shard key ที่ไม่ดี
sh.shardCollection("myDatabase.orders", { orderDate: 1 })
// ปัญหา: ข้อมูลใหม่จะไปที่ shard เดียวเสมอ

// ✅ Shard key ที่ดี
sh.shardCollection("myDatabase.orders", { customerId: 1, orderDate: 1 })
// ข้อมูลกระจายตาม customerId และ orderDate
```

### 10.5 คำสั่งจัดการ Sharding

```javascript
// ตรวจสอบสถานะ sharded cluster
sh.status()

// ดู shard distribution
db.users.getShardDistribution()

// ตรวจสอบว่า collection ถูก shard หรือไม่
db.users.stats()

// ดู chunk distribution
use config
db.chunks.find({ ns: "myDatabase.users" }).pretty()

// Manual chunk split
sh.splitAt("myDatabase.users", { userId: 50000 })

// Move chunk
sh.moveChunk("myDatabase.users", { userId: 50000 }, "shard2RS")

// Balance chunks
sh.enableBalancing("myDatabase.users")
sh.disableBalancing("myDatabase.users")
sh.isBalancerRunning()
```

---

## 11. Security

### 11.1 Authentication

```javascript
// สร้าง admin user
use admin
db.createUser({
  user: "admin",
  pwd: "securePassword123",
  roles: [
    { role: "userAdminAnyDatabase", db: "admin" },
    { role: "readWriteAnyDatabase", db: "admin" }
  ]
})

// สร้าง user สำหรับ database เฉพาะ
use myDatabase
db.createUser({
  user: "appUser",
  pwd: "appPassword123",
  roles: [
    { role: "readWrite", db: "myDatabase" }
  ]
})

// เปิดใช้งาน authentication
// แก้ไขไฟล์ mongod.conf:
# security:
#   authorization: enabled

// เชื่อมต่อด้วย authentication
mongosh -u admin -p securePassword123 --authenticationDatabase admin
```

### 11.2 Roles และ Privileges

```javascript
// Built-in roles:
// - read: อ่านข้อมูลได้
// - readWrite: อ่านและเขียนข้อมูลได้
// - dbAdmin: จัดการ database
// - userAdmin: จัดการ users
// - clusterAdmin: จัดการ cluster
// - root: สิทธิ์ทั้งหมด

// สร้าง custom role
use myDatabase
db.createRole({
  role: "customRole",
  privileges: [
    {
      resource: { db: "myDatabase", collection: "users" },
      actions: ["find", "insert", "update"]
    }
  ],
  roles: []
})

// เพิ่ม role ให้ user
db.grantRolesToUser("appUser", [{ role: "customRole", db: "myDatabase" }])

// ดู roles ของ user
db.getUser("appUser")
```

### 11.3 Encryption

#### Encryption at Rest

```bash
# ใช้ --enableEncryption
mongod --enableEncryption \
  --encryptionKeyFile /path/to/keyfile \
  --dbpath /data/db
```

#### Encryption in Transit (TLS/SSL)

```bash
# สร้าง self-signed certificate
openssl req -newkey rsa:2048 -new -x509 -days 365 -nodes \
  -out mongodb-cert.crt -keyout mongodb-cert.key

# รวมไฟล์ certificate และ key
cat mongodb-cert.key mongodb-cert.crt > mongodb.pem

# เริ่ม mongod ด้วย TLS
mongod --tlsMode requireTLS \
  --tlsCertificateKeyFile /path/to/mongodb.pem \
  --dbpath /data/db
```

### 11.4 IP Whitelisting

```javascript
// แก้ไข mongod.conf:
# net:
#   bindIp: localhost,192.168.1.100
#   port: 27017

// หรือใช้ firewall
// Linux (iptables)
sudo iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 27017 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 27017 -j DROP
```

### 11.5 Auditing

```javascript
// เปิดใช้งาน auditing (MongoDB Enterprise)
// แก้ไข mongod.conf:
# auditLog:
#   destination: file
#   format: JSON
#   path: /var/log/mongodb/audit.json

// ตัวอย่างการกำหนดค่า audit filter
db.adminCommand({
  setParameter: 1,
  auditAuthorizationSuccess: true
})
```

---

## 12. Best Practices

### 12.1 Schema Design

```javascript
// ✅ DO: ใช้ embedded documents สำหรับข้อมูลที่อ่านพร้อมกันบ่อย
{
  _id: 1,
  name: "John Doe",
  address: {
    street: "123 Main St",
    city: "Bangkok"
  }
}

// ❌ DON'T: แยก collection เมื่อไม่จำเป็น
// Users collection
{ _id: 1, name: "John Doe", addressId: 100 }
// Addresses collection
{ _id: 100, street: "123 Main St", city: "Bangkok" }

// ✅ DO: ใช้ references สำหรับ many-to-many relationships
// ❌ DON'T: ฝัง array ขนาดใหญ่ที่เติบโตไม่จำกัด
```

### 12.2 Indexing

```javascript
// ✅ DO: สร้าง index สำหรับ query ที่ใช้บ่อย
db.orders.createIndex({ customerId: 1, orderDate: -1 })

// ✅ DO: ใช้ compound index อย่างมีประสิทธิภาพ
db.products.createIndex({ category: 1, price: -1, name: 1 })

// ❌ DON'T: สร้าง index มากเกินไป
// index ทุกอันมีค่าใช้จ่ายในการ maintain

// ✅ DO: ตรวจสอบการใช้งาน index
db.collection.aggregate([{ $indexStats: {} }])

// ❌ DON'T: ลืมสร้าง index สำหรับ foreign keys
db.orders.createIndex({ customerId: 1 })
```

### 12.3 Query Optimization

```javascript
// ✅ DO: ใช้ projection
db.users.find(
  { age: { $gte: 25 } },
  { name: 1, email: 1 }
)

// ❌ DON'T: ดึงข้อมูลทั้งหมดเมื่อไม่จำเป็น
db.users.find({ age: { $gte: 25 } })

// ✅ DO: ใช้ limit
db.users.find().limit(100)

// ✅ DO: ใช้ explain เพื่อตรวจสอบ performance
db.users.find({ email: "john@example.com" }).explain("executionStats")

// ❌ DON'T: ใช้ $where (ช้ามาก)
db.users.find({ $where: "this.age > 25" })
// ✅ DO: ใช้ query operators
db.users.find({ age: { $gt: 25 } })
```

### 12.4 Connection Management

```javascript
// ✅ DO: ใช้ connection pooling
const client = new MongoClient(uri, {
  maxPoolSize: 50,
  minPoolSize: 10,
  maxIdleTimeMS: 30000
})

// ✅ DO: Handle connection errors
try {
  await client.connect()
  // ... operations
} catch (error) {
  console.error("Connection error:", error)
} finally {
  await client.close()
}

// ❌ DON'T: สร้าง connection ใหม่ทุกครั้ง
```

### 12.5 Error Handling

```javascript
// ✅ DO: Handle duplicate key errors
try {
  await db.users.insertOne({ email: "john@example.com" })
} catch (error) {
  if (error.code === 11000) {
    console.error("Duplicate email")
  }
}

// ✅ DO: ใช้ transactions สำหรับ multi-document operations
const session = client.startSession()
try {
  await session.withTransaction(async () => {
    await db.accounts.updateOne(
      { _id: accountA },
      { $inc: { balance: -100 } },
      { session }
    )
    await db.accounts.updateOne(
      { _id: accountB },
      { $inc: { balance: 100 } },
      { session }
    )
  })
} finally {
  await session.endSession()
}
```

### 12.6 Monitoring

```javascript
// ✅ DO: ตรวจสอบ performance metrics
db.serverStatus()
db.stats()
db.collection.stats()

// ✅ DO: ใช้ profiler สำหรับ slow queries
db.setProfilingLevel(1, { slowms: 100 })
db.system.profile.find().pretty()

// ✅ DO: Monitor replication lag
rs.printReplicationInfo()
rs.printSecondaryReplicationInfo()
```

### 12.7 Backup และ Recovery

```bash
# ✅ DO: สำรองข้อมูลเป็นประจำ
mongodump --uri="mongodb://localhost:27017/myDatabase" --out=/backup

# Restore
mongorestore --uri="mongodb://localhost:27017" /backup

# ✅ DO: สำรองข้อมูล specific collection
mongodump --uri="mongodb://localhost:27017/myDatabase" \
  --collection=users --out=/backup

# ✅ DO: ใช้ point-in-time backups สำหรับ production
# (ต้องใช้ MongoDB Atlas หรือ Ops Manager)
```

### 12.8 Document Size

```javascript
// ❌ DON'T: เกิน 16MB document size limit
// ✅ DO: แบ่งข้อมูลออกหรือใช้ GridFS สำหรับไฟล์ขนาดใหญ่

// GridFS example
const bucket = new GridFSBucket(db)
const uploadStream = bucket.openUploadStream("myfile.pdf")
fs.createReadStream("./myfile.pdf").pipe(uploadStream)
```

### 12.9 ตัวอย่าง Connection String

```javascript
// Local MongoDB
mongodb://localhost:27017/myDatabase

// MongoDB with authentication
mongodb://username:password@localhost:27017/myDatabase

// MongoDB Replica Set
mongodb://host1:27017,host2:27017,host3:27017/myDatabase?replicaSet=rs0

// MongoDB Atlas
mongodb+srv://username:password@cluster.mongodb.net/myDatabase

// Connection options
mongodb://localhost:27017/myDatabase?maxPoolSize=50&retryWrites=true
```

---

## 📖 ทรัพยากรเพิ่มเติม (Additional Resources)

### Official Documentation
- [MongoDB Manual](https://docs.mongodb.com/manual/)
- [MongoDB University](https://university.mongodb.com/) - คอร์สฟรี
- [MongoDB Blog](https://www.mongodb.com/blog)

### Tools
- [MongoDB Compass](https://www.mongodb.com/products/compass) - GUI tool
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) - Cloud database
- [Studio 3T](https://studio3t.com/) - Advanced GUI tool

### Community
- [MongoDB Community Forums](https://www.mongodb.com/community/forums/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/mongodb)

---

## 🎯 สรุป (Summary)

MongoDB เป็นฐานข้อมูล NoSQL ที่ทรงพลังและยืดหยุ่น เหมาะสำหรับ:
- ✅ Applications ที่ต้องการ scalability สูง
- ✅ ข้อมูลที่มีโครงสร้างซับซ้อนและเปลี่ยนแปลงบ่อย
- ✅ Real-time analytics และ big data
- ✅ Content management systems
- ✅ IoT applications

**จุดสำคัญที่ต้องจำ:**
1. เข้าใจความแตกต่างระหว่าง embedded documents และ references
2. สร้าง index อย่างมีประสิทธิภาพ
3. ใช้ aggregation framework สำหรับการวิเคราะห์ข้อมูล
4. ตั้งค่า replication และ sharding สำหรับ high availability
5. ใส่ใจ security และ backup เสมอ

---

## 📝 License

This tutorial is open source and available for educational purposes.

---

**Happy Learning MongoDB! 🚀**