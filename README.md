// auth.js (Node.js + Express + JWT)
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();
app.use(express.json());

const SECRET = 'secret';
const USERS = [{ user: 'admin', pass: '1234' }];

app.post('/login', (req, res) => {
  const u = USERS.find(x => x.user === req.body.user && x.pass === req.body.pass);
  if (!u) return res.sendStatus(401);
  res.json({ token: jwt.sign({ user: u.user }, SECRET) });
});

app.get('/secure', (req, res) => {
  const t = req.headers.authorization?.split(' ')[1];
  try {
    const data = jwt.verify(t, SECRET);
    res.json({ msg: `Hello ${data.user}` });
  } catch {
    res.sendStatus(403);
  }
});

app.listen(3000);
