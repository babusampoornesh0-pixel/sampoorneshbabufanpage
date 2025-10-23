<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Send a Secret Message 💌</title>
  <style>
    /* 🌙 Aesthetic styling */
    body {
      margin: 0;
      padding: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: radial-gradient(circle at 10% 20%, #ff7eb3, #ff758c, #ff7eb3 70%);
      font-family: "Poppins", sans-serif;
      color: #fff;
      overflow: hidden;
    }

    .box {
      background: rgba(0, 0, 0, 0.25);
      border-radius: 18px;
      padding: 30px 25px;
      text-align: center;
      max-width: 400px;
      width: 90%;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
      backdrop-filter: blur(10px);
    }

    h1 {
      margin: 0;
      font-size: 22px;
      letter-spacing: 1px;
    }

    p {
      font-size: 14px;
      color: #ffe4ec;
      margin-top: 6px;
      margin-bottom: 20px;
    }

    textarea {
      width: 100%;
      height: 130px;
      border-radius: 12px;
      border: none;
      resize: none;
      outline: none;
      padding: 10px;
      background: rgba(255, 255, 255, 0.15);
      color: #fff;
      font-size: 15px;
      transition: 0.3s;
    }

    textarea::placeholder {
      color: #f8d8e2;
    }

    textarea:focus {
      background: rgba(255, 255, 255, 0.25);
    }

    button {
      margin-top: 15px;
      padding: 10px 25px;
      border-radius: 10px;
      border: none;
      background: linear-gradient(90deg, #ff6b6b, #ff9a9e);
      color: white;
      font-size: 15px;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      transform: scale(1.05);
      background: linear-gradient(90deg, #ff7eb3, #ff758c);
    }

    .note {
      margin-top: 12px;
      font-size: 13px;
      color: #ffe8ef;
      opacity: 0.8;
    }

    .sent {
      display: none;
      margin-top: 12px;
      background: rgba(0, 255, 128, 0.2);
      border-radius: 10px;
      padding: 10px;
      color: #caffbf;
      font-weight: 600;
      animation: fadeIn 0.6s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }

    footer {
      position: absolute;
      bottom: 10px;
      width: 100%;
      text-align: center;
      font-size: 12px;
      color: rgba(255, 255, 255, 0.6);
    }
  </style>
</head>
<body>
  <div class="box">
    <h1>Send Me a Secret 💌</h1>
    <p>Type anything you want to say — it's 100% anonymous!</p>

    <form id="confessionForm" action="https://formspree.io/f/xwprdgzr" method="POST">
      <textarea name="message" placeholder="Your secret message..." required></textarea>
      <button type="submit">Send</button>
      <div class="note">Your message is anonymous • no name, no email needed</div>
      <div class="sent" id="sentMsg">✅ Message sent! Thanks for sharing 💫</div>
    </form>
  </div>

  <footer>made with ❤️ for confessions</footer>

  <script>
    const form = document.getElementById("confessionForm");
    const sentMsg = document.getElementById("sentMsg");

    form.addEventListener("submit", async (e) => {
      e.preventDefault();
      const data = new FormData(form);
      const message = data.get("message").trim();

      if (!message) {
        alert("Please write something before sending!");
        return;
      }

      // Optional: prevent links/emails/phones
      if (message.includes("http") || message.includes("@") || /\d{7,}/.test(message)) {
        alert("Please don't include links, phone numbers, or emails!");
        return;
      }

      const response = await fetch(form.action, {
        method: "POST",
        body: data,
        headers: { Accept: "application/json" },
      });

      if (response.ok) {
        sentMsg.style.display = "block";
        form.reset();
        setTimeout(() => { sentMsg.style.display = "none"; }, 4000);
      } else {
        alert("Something went wrong. Please try again later!");
      }
    });
  </script>
</body>
</html>
