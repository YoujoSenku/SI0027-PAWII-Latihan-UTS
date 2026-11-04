1. npm install express mongoose cors dotenv express-async-errors
2. mongodb+srv://stevenchristianlauw2428240015_db_user:password@cluster0.jxpwzby.mongodb.net
3. pass: DZDSfh7eUKUkZQkZ
4. npm install -g newman
5. newman run collection -e environemnt
6. npm install -D nodemon (opsional)


JIKA LOKAL =>

// 1. Load file .env di baris paling pertama
require('dotenv').config(); 

const express = require('express');
const mongoose = require('mongoose');

const app = express();
app.use(express.json());

// 2. Ambil variabel dari file .env
const PORT = process.env.PORT || 3000;
const DB_URL = process.env.DATABASE_URL;

// 3. Koneksi ke MongoDB menggunakan variabel .env
mongoose.connect(DB_URL)
  .then(() => console.log('✅ Sukses terhubung ke MongoDB Lokal lewat .env'))
  .catch((err) => console.error('❌ Gagal terhubung ke MongoDB:', err));

// ==========================================
// CONTOH SCHEMA & ROUTE UNTUK TESTING
// ==========================================
const userSchema = new mongoose.Schema({
  nama: String,
  email: String
});
const User = mongoose.model('User', userSchema);

// Endpoint Tambah User
app.post('/users', async (req, res) => {
  try {
    const user Baru = new User(req.body);
    await userBaru.save();
    res.status(201).json(userBaru);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

// Endpoint Ambil User
app.get('/users', async (req, res) => {
  const users = await User.find();
  res.json(users);
});

// 4. Jalankan Server menggunakan PORT dari .env
app.listen(PORT, () => {
  console.log(`🚀 Server aktif di http://localhost:${PORT}`);
});
