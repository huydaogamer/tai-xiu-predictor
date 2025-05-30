<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8" />
<title>Tool Tra cứu và dự đoán bàn MD5</title>
<style>
  body { font-family: Arial, sans-serif; padding: 20px; max-width: 600px; margin: auto; }
  input, button { font-size: 16px; padding: 8px; margin-top: 10px; width: 100%; }
  .result { margin-top: 20px; background: #f5f5f5; padding: 15px; border-radius: 6px; }
</style>
</head>
<body>
  <h1>Tra cứu và dự đoán bàn MD5</h1>
  <input type="text" id="md5Input" placeholder="Nhập mã MD5 bàn ở đây" />
  <button onclick="lookupAndPredict()">Tra cứu & Dự đoán</button>
  <div id="result" class="result" style="display:none;"></div>

<script>
  const data = {
    "b06b32fee716ab1cbf83f7c1770c093c": [9, 10, 11, 7, 14, 13, 8],
    "7f2e7aa5c12daa7d88a877c8dbddbd75": [11, 9, 14, 10, 12],
    "abcdef1234567890abcdef1234567890": [10, 13, 9, 11, 15]
  };

  function lookupAndPredict() {
    const md5 = document.getElementById('md5Input').value.trim().toLowerCase();
    const resultDiv = document.getElementById('result');
    if (!md5) {
      alert('Vui lòng nhập mã MD5 bàn.');
      return;
    }
    if (!data.hasOwnProperty(md5)) {
      resultDiv.style.display = 'block';
      resultDiv.innerHTML = '<p>Không tìm thấy dữ liệu cho mã MD5 này.</p>';
      return;
    }
    const history = data[md5];
    const sum = history.reduce((a,b) => a+b, 0);
    const avg = Math.round(sum / history.length);
    const prediction = avg >= 11 ? 'Tài' : 'Xỉu';

    resultDiv.style.display = 'block';
    resultDiv.innerHTML = `<h3>Lịch sử tổng điểm các phiên bàn này:</h3>
                           <p>${history.join(', ')}</p>
                           <h3>Dự đoán phiên tiếp theo:</h3>
                           <p><strong>Tổng điểm:</strong> ${avg}</p>
                           <p><strong>Kết quả:</strong> ${prediction}</p>`;
  }
</script>
</body>
</html>
