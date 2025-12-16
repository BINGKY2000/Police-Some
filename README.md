# Police-Some<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>ระบบคำนวณคดีตำรวจ FiveM</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #020617, #0f172a);
      color: #e5e7eb;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }
    .box {
      background: #020617;
      padding: 24px;
      border-radius: 16px;
      width: 100%;
      max-width: 380px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.6);
    }
    h2 {
      text-align: center;
      margin-bottom: 6px;
    }
    .subtitle {
      text-align: center;
      font-size: 13px;
      color: #94a3b8;
      margin-bottom: 16px;
    }
    label {
      display: block;
      margin-top: 12px;
      font-size: 14px;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 6px;
      border-radius: 8px;
      border: none;
      font-size: 15px;
    }
    button {
      width: 100%;
      margin-top: 16px;
      padding: 12px;
      background: #22c55e;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }
    button.copy {
      background: #3b82f6;
      margin-top: 10px;
    }
    .result {
      margin-top: 16px;
      background: #020617;
      padding: 14px;
      border-radius: 10px;
      font-size: 15px;
      line-height: 1.6;
    }
    footer {
      text-align: center;
      margin-top: 14px;
      font-size: 12px;
      color: #64748b;
    }
  </style>
</head>
<body>
  <div class="box">
    <h2>👮‍♂️ คำนวณคดีตำรวจ FiveM</h2>
    <div class="subtitle">เวอร์ชันใช้งานจริง สำหรับเจ้าหน้าที่</div>

    <label>ประเภทคดี</label>
    <select id="caseType">
      <option value="assault">ทำร้ายร่างกาย</option>
      <option value="assault_uncon">ทำร้ายร่างกายจนสลบ</option>
      <option value="weapon">พกพาอาวุธผิดกฎหมาย</option>
      <option value="drug">ครอบครองยาเสพติด</option>
    </select>

    <label>จำนวนครั้ง / จำนวนของ</label>
    <input type="number" id="count" value="1" min="1" />

    <button onclick="calculate()">คำนวณโทษ</button>

    <div class="result" id="result">ยังไม่ได้คำนวณ</div>
    <button class="copy" onclick="copyResult()">📋 คัดลอกไปวาง Discord</button>

    <footer>FiveM Police Case Calculator</footer>
  </div>

  <script>
    let lastText = '';

    function calculate() {
      const type = document.getElementById('caseType').value;
      const count = Number(document.getElementById('count').value);

      let jail = 0;
      let fine = 0;
      let name = '';

      if (type === 'assault') {
        name = 'ทำร้ายร่างกาย';
        jail = 10 * count;
        fine = 5000 * count;
      } else if (type === 'assault_uncon') {
        name = 'ทำร้ายร่างกายจนสลบ';
        jail = 20 * count;
        fine = 10000 * count;
      } else if (type === 'weapon') {
        name = 'พกพาอาวุธผิดกฎหมาย';
        jail = 15 * count;
        fine = 8000 * count;
      } else if (type === 'drug') {
        name = 'ครอบครองยาเสพติด';
        jail = 20 * count;
        fine = 12000 * count;
      }

      lastText = `📄 รายการคดี: ${name}\n⏱️ จำคุก: ${jail} นาที\n💰 ค่าปรับ: ${fine.toLocaleString()} IC`;

      document.getElementById('result').innerHTML = lastText.replace(/\n/g, '<br>');
    }

    function copyResult() {
      if (!lastText) return alert('ยังไม่มีผลลัพธ์ให้คัดลอก');
      navigator.clipboard.writeText(lastText);
      alert('คัดลอกเรียบร้อยแล้ว');
    }
  </script>
</body>
</html>
