<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>دردشة جماعية مع بروفايل مجمل</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      direction: rtl;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
    }

    .chat-container {
      width: 400px;
      margin: 50px auto;
      background-color: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px;
      background-color: #4CAF50;
      border-radius: 10px 10px 0 0;
    }

    .user-icon {
      width: 40px;
      height: 40px;
      background-color: #fff;
      color: #4CAF50;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 50%;
      font-weight: bold;
      cursor: pointer;
    }

    .title {
      color: #fff;
      font-size: 18px;
    }

    .notification-icon {
      font-size: 20px;
      cursor: pointer;
    }

    .messages {
      padding: 20px;
      height: 300px;
      overflow-y: auto;
      background-color: #f9f9f9;
    }

    .message-input {
      width: calc(100% - 40px);
      padding: 10px;
      margin: 10px;
      border-radius: 5px;
      border: 1px solid #ddd;
    }

    button {
      padding: 10px 15px;
      background-color: #4CAF50;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #45a049;
    }

    /* تصميم البروفايل */
    .profile-container {
      padding: 20px;
      background-color: #fff;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    .profile-container input,
    .profile-container button {
      width: 100%;
      padding: 10px;
      margin: 5px 0;
      border-radius: 5px;
      border: 1px solid #ddd;
    }

    .profile-container img {
      border-radius: 50%;
      width: 60px;
      height: 60px;
      margin-right: 10px;
    }

    .profile-comment {
      margin-top: 10px;
      color: gray;
      font-style: italic;
    }

    /* تصميم التعليقات */
    .message {
      display: flex;
      align-items: center;
      margin-bottom: 15px;
    }

    .message img {
      border-radius: 50%;
      width: 40px;
      height: 40px;
      margin-left: 10px;
    }

    .message-info {
      background-color: #e1f5e1;
      padding: 10px;
      border-radius: 10px;
      max-width: 70%;
    }

    .message-username {
      font-weight: bold;
      margin-bottom: 5px;
    }

    .message-text {
      margin: 0;
    }

    /* وضعية الإشعار */
    .notification-active {
      color: red;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="header">
      <div class="user-icon" id="userIcon" onclick="toggleProfile()">A</div>
      <div class="title">دردشة جماعية</div>
      <div class="notification-icon" id="notification">🔔</div>
    </div>
    <div class="messages" id="messages"></div>
    <input type="text" id="messageInput" class="message-input" placeholder="أكتب رسالتك...">
    <button onclick="sendMessage()">إرسال</button>
  </div>

  <div class="profile-container" id="profileContainer">
    <h3>الملف الشخصي</h3>
    <div>
      <img src="https://via.placeholder.com/60" alt="الصورة الشخصية" id="profileImage">
      <input type="file" id="profileImageInput" onchange="updateProfileImage()">
      <input type="text" id="usernameInput" placeholder="أدخل اسم المستخدم" value="أحمد">
      <button onclick="saveProfile()">حفظ التغييرات</button>
      <div class="profile-comment" id="profileComment">يمكنك تعديل اسم المستخدم أو تغيير الصورة الشخصية.</div>
    </div>
  </div>

  <script>
    let messagesContainer = document.getElementById('messages');
    let messageInput = document.getElementById('messageInput');
    let notificationIcon = document.getElementById('notification');
    let userIcon = document.getElementById('userIcon');
    let profileContainer = document.getElementById('profileContainer');
    let usernameInput = document.getElementById('usernameInput');
    let profileImageInput = document.getElementById('profileImageInput');
    let profileImage = document.getElementById('profileImage');
    let profileComment = document.getElementById('profileComment');

    // معلومات المستخدم الافتراضية
    let currentUsername = 'أحمد';
    let currentUserImage = 'https://via.placeholder.com/60';

    function sendMessage() {
      let messageText = messageInput.value.trim();

      if (messageText) {
        // إضافة الرسالة إلى واجهة المستخدم
        let newMessage = document.createElement('div');
        newMessage.classList.add('message');

        // إضافة صورة واسم المستخدم مع الرسالة
        newMessage.innerHTML = `
          <img src="${currentUserImage}" alt="الصورة الشخصية">
          <div class="message-info">
            <div class="message-username">${currentUsername}</div>
            <p class="message-text">${messageText}</p>
          </div>
        `;

        messagesContainer.appendChild(newMessage);

        // مسح المدخل بعد إرسال الرسالة
        messageInput.value = '';

        // تفعيل الإشعار
        notificationIcon.classList.add('notification-active');

        // إعادة تعيين الإشعار بعد 3 ثواني
        setTimeout(() => {
          notificationIcon.classList.remove('notification-active');
        }, 3000);

        // تمرير الرسائل إلى أسفل
        messagesContainer.scrollTop = messagesContainer.scrollHeight;
      }
    }

    function toggleProfile() {
      // إظهار أو إخفاء نافذة البروفايل
      if (profileContainer.style.display === 'none' || profileContainer.style.display === '') {
        profileContainer.style.display = 'block';
      } else {
        profileContainer.style.display = 'none';
      }
    }

    function saveProfile() {
      // حفظ التغييرات
      currentUsername = usernameInput.value;

      if (profileImageInput.files[0]) {
        let reader = new FileReader();
        reader.onload = function (e) {
          currentUserImage = e.target.result;
        };
        reader.readAsDataURL(profileImageInput.files[0]);
      }

      // تحديث أيقونة المستخدم
      userIcon.textContent = currentUsername.charAt(0).toUpperCase();

      // تحديث التعليق
      profileComment.textContent = 'تم حفظ التغييرات بنجاح!';

      // إغلاق نافذة البروفايل بعد 3 ثواني
      setTimeout(() => {
        profileContainer.style.display = 'none';
      }, 3000);
    }

    function updateProfileImage() {
      let newImage = profileImageInput.files[0];
      if (newImage) {
        let reader = new FileReader();
        reader.onload = function (e) {
          profileImage.src = e.target.result;
        };
        reader.readAsDataURL(newImage);
      }
    }
  </script>
</body>
</html>
