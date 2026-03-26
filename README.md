<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>HS Chat 💬 | HISSAN SETHI</title>
  <style>
    :root {
      --bg: #050b14;
      --panel: rgba(13, 27, 46, 0.9);
      --border: rgba(140, 181, 255, 0.12);
      --text: #eff5ff;
      --muted: #9ab3d3;
      --primary: #4f8cff;
      --accent: #19d3a6;
      --danger: #ff4757;
      --radius: 20px;
    }

    * { box-sizing: border-box; outline: none; }
    body {
      margin: 0; min-height: 100vh; font-family: 'Inter', sans-serif;
      color: var(--text); background: var(--bg);
      background-image: radial-gradient(circle at 0% 0%, rgba(79, 140, 255, 0.15), transparent 40%),
                        radial-gradient(circle at 100% 100%, rgba(25, 211, 166, 0.1), transparent 40%);
      overflow-x: hidden;
    }

    .app { width: min(1200px, 95%); margin: 0 auto; padding: 20px 0; }

    .main-heading {
      font-size: 3.2rem;
      text-align: center;
      margin: 10px 0 30px;
      letter-spacing: 3px;
      font-weight: 900;
    }

    .topbar {
      display: flex; justify-content: space-between; align-items: center;
      padding: 15px 30px; background: rgba(8, 18, 33, 0.85);
      border-radius: 100px; border: 1px solid var(--border); margin-bottom: 25px;
      backdrop-filter: blur(15px); box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    }

    .brand { font-weight: 800; display: flex; align-items: center; gap: 12px; font-size: 1.2rem; }
    .logo-sq { width: 38px; height: 38px; background: linear-gradient(135deg, var(--primary), #8a6dff); border-radius: 12px; display: grid; place-items: center; box-shadow: 0 0 20px rgba(79, 140, 255, 0.4); }

    .card {
      background: var(--panel); border: 1px solid var(--border);
      border-radius: var(--radius); padding: 25px; backdrop-filter: blur(20px);
      box-shadow: 0 20px 50px rgba(0,0,0,0.3); margin-bottom: 20px;
    }

    .grid { display: grid; grid-template-columns: 1fr 1.3fr; gap: 20px; }
    @media (max-width: 950px) { .grid { grid-template-columns: 1fr; } }

    .gradient-text { background: linear-gradient(135deg, #fff, var(--primary)); -webkit-background-clip: text; color: transparent; font-weight: 800; }

    input, select {
      width: 100%; padding: 14px; border-radius: 12px; border: 1px solid var(--border);
      background: rgba(255,255,255,0.03); color: #fff; margin-bottom: 12px; transition: 0.3s;
    }

    .btn {
      padding: 14px 22px; border-radius: 12px; border: none; font-weight: 700;
      cursor: pointer; transition: 0.3s; display: inline-flex; align-items: center; justify-content: center; gap: 8px;
    }
    .btn-p { background: linear-gradient(135deg, var(--primary), #7a72ff); color: white; width: 100%; }
    .btn-s { background: rgba(255, 255, 255, 0.08); color: white; border: 1px solid var(--border); }
    .btn-danger { background: var(--danger); color: white; }
    .btn:hover { transform: translateY(-2px); filter: brightness(1.1); }

    .email-group { display: flex; gap: 8px; }
    .email-group input { flex: 1; }
    .email-group select { width: 140px; }

    /* Storage & Gallery */
    .storage-header { display: flex; justify-content: space-between; margin-bottom: 10px; font-size: 0.85rem; }
    .meter-bg { background: rgba(255,255,255,0.05); height: 10px; border-radius: 10px; overflow: hidden; margin-bottom: 20px; }
    .meter-fill { height: 100%; background: linear-gradient(90deg, var(--accent), var(--primary)); width: 0%; transition: 0.6s; }

    .vault-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 15px; }
    .media-item { border-radius: 12px; overflow: hidden; background: #000; aspect-ratio: 1; position: relative; border: 1px solid var(--border); cursor: pointer; }
    .media-item img, .media-item video { width: 100%; height: 100%; object-fit: cover; pointer-events: none; }
    .delete-media { position: absolute; top: 8px; right: 8px; background: var(--danger); border: none; color: white; border-radius: 50%; width: 26px; height: 26px; cursor: pointer; z-index: 10; font-weight: bold; }

    /* Chat Area */
    .chat-box { height: 380px; overflow-y: auto; padding: 15px; display: flex; flex-direction: column; gap: 12px; background: rgba(0,0,0,0.25); border-radius: 15px; margin-bottom: 15px; border: 1px solid var(--border); scroll-behavior: smooth; }
    .msg { padding: 12px 16px; border-radius: 16px; max-width: 85%; font-size: 0.92rem; line-height: 1.4; animation: fadeIn 0.3s ease; }
    .msg.bot { background: #1a2536; align-self: flex-start; border-bottom-left-radius: 4px; }
    .msg.user { background: var(--primary); align-self: flex-end; border-bottom-right-radius: 4px; }

    /* Recovery Sections */
    .recovery-label { font-size: 0.85rem; color: var(--accent); margin-bottom: 8px; display: block; }

    #viewerModal { position: fixed; inset: 0; background: rgba(0,0,0,0.98); z-index: 10000; display: none; place-items: center; }
    #viewerModal.active { display: grid; }
    #viewerContent img, #viewerContent video { max-width: 95vw; max-height: 90vh; border-radius: 10px; }
    .close-viewer { position: absolute; top: 20px; right: 20px; color: white; font-size: 35px; cursor: pointer; background: rgba(255,255,255,0.1); border: none; border-radius: 50%; width: 50px; height: 50px; }

    .modal { position: fixed; inset: 0; background: rgba(2, 6, 12, 0.98); z-index: 9999; display: none; place-items: center; padding: 20px; }
    .modal.active { display: grid; }
    .modal-card { background: var(--panel); border: 1px solid var(--primary); padding: 30px; border-radius: 25px; width: 100%; max-width: 900px; max-height: 90vh; overflow-y: auto; }
    
    .hidden { display: none !important; }
    .status-dot { width: 8px; height: 8px; border-radius: 50%; display: inline-block; background: #ff4757; margin-right: 5px; }
    .status-active { background: var(--accent) !important; box-shadow: 0 0 10px var(--accent); }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
  </style>
</head>
<body>

  <div class="app">
    <h1 class="main-heading gradient-text">HS-FREE STORAGE</h1>

    <header class="topbar">
      <div class="brand">
        <div class="logo-sq">HS</div>
        <span>HS Chat <small style="color:var(--muted)">| HISSAN SETHI</small></span>
      </div>
      <div id="sessionStatus"><span id="dot" class="status-dot"></
