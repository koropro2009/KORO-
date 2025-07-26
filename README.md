# KORO-
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>تسجيل أعضاء الكلان</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f0f8ff;
      padding: 20px;
      direction: rtl;
      text-align: right;
    }
    h2 {
      color: #008080;
    }
    input, select, textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 10px;
      border: 1px solid #ccc;
    }
    button {
      padding: 10px 20px;
      background-color: #00b894;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    .member {
      background-color: #dff9fb;
      padding: 10px;
      margin-top: 10px;
      border-radius: 10px;
    }
    .delete-btn {
      background-color: #d63031;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <h2>⚡ للتسجيل أملا ما يأتي: ⚡</h2>

  <form id="registerForm">
    <label>الاسم 🌺:</label>
    <input type="text" id="name" required>

    <label>المستوى 🏅:</label>
    <input type="text" id="level" required>

    <label>الفريمات ⚡:</label>
    <input type="text" id="frames">

    <label>التقييم 💠:</label>
    <input type="text" id="rank">

    <label>الكيدي 🔥:</label>
    <input type="text" id="kda">

    <label>كم سنة تلعب بوبجي ✨:</label>
    <input type="text" id="years">

    <label>الرتبة التي تريدها:</label>
    <input type="text" id="role">

    <button type="submit">تسجيل</button>
  </form>

  <h3>🌺 بالتوفيق للجميع 🌺</h3>

  <h2>📋 الأعضاء المسجلون:</h2>
  <div id="membersList"></div>



  <script>
    const form = document.getElementById('registerForm');
    const membersList = document.getElementById('membersList');

    // تحميل الأعضاء من LocalStorage عند فتح الصفحة
    window.onload = function() {
      showMembers();
    }

    form.onsubmit = function(event) {
      event.preventDefault();

      const member = {
        name: document.getElementById('name').value,
        level: document.getElementById('level').value,
        frames: document.getElementById('frames').value,
        rank: document.getElementById('rank').value,
        kda: document.getElementById('kda').value,
        years: document.getElementById('years').value,
        role: document.getElementById('role').value
      };

      // حفظ في LocalStorage
      let members = JSON.parse(localStorage.getItem('clanMembers')) || [];
      members.push(member);
      localStorage.setItem('clanMembers', JSON.stringify(members));

      form.reset();
      showMembers();
    };

    function showMembers() {
      const members = JSON.parse(localStorage.getItem('clanMembers')) || [];
      membersList.innerHTML = '';
      members.forEach((m, index) => {
        membersList.innerHTML += `
          <div class="member">
            <strong>الاسم:</strong> ${m.name}<br>
            <strong>المستوى:</strong> ${m.level}<br>
            <strong>الفريمات:</strong> ${m.frames}<br>
            <strong>التقييم:</strong> ${m.rank}<br>
            <strong>الكيدي:</strong> ${m.kda}<br>
            <strong>عدد سنوات اللعب:</strong> ${m.years}<br>
            <strong>الرتبة المطلوبة:</strong> ${m.role}
          </div>
        `;
      });
    }

    function clearMembers() {
      if (confirm("هل أنت متأكد أنك تريد مسح جميع بيانات الأعضاء؟")) {
        localStorage.removeItem('clanMembers');
        showMembers(); // لتحديث العرض بعد المسح
      }
    }
  </script>

</body>
</html>
