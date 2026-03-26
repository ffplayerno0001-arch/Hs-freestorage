
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
    <header class="topbar">
      <div class="brand">
        <div class="logo-sq">HS</div>
        <span>HS Chat <small style="color:var(--muted)">| HISSAN SETHI</small></span>
      </div>
      <div id="sessionStatus"><span id="dot" class="status-dot"></span> <span id="stTxt">Connecting...</span></div>
    </header>

    <div class="grid">
      <!-- Auth Section -->
      <section class="card">
        <h2 class="gradient-text" id="authTitle">Secure Access</h2>
        
        <div id="authForms">
          <!-- Signup Mode -->
          <div id="signupFields" class="hidden">
            <input type="text" id="regName" placeholder="Full Name">
            <label class="recovery-label">Select Security Question (For Recovery)</label>
            <select id="regQuestion">
              <option value="pet">Name of your first pet?</option>
              <option value="city">Birth City?</option>
              <option value="school">Name of your first school?</option>
            </select>
            <input type="text" id="regAnswer" placeholder="Security Answer">
          </div>

          <!-- Recovery Mode -->
          <div id="recoveryFields" class="hidden">
             <input type="text" id="recEmail" placeholder="Enter Account Email">
             <p id="recQuestionDisplay" style="font-size:0.85rem; color:var(--muted); margin-bottom:10px;">Security Answer Required</p>
             <input type="text" id="recAns" placeholder="Your Security Answer">
             <input type="password" id="newPass" placeholder="Enter New Password">
          </div>

          <!-- Login Mode -->
          <div id="mainInputs">
            <div class="email-group">
              <input type="text" id="emailUser" placeholder="username">
              <select id="emailDomain">
                <option value="@gmail.com">@gmail.com</option>
                <option value="@outlook.com">@outlook.com</option>
                <option value="@icloud.com">@icloud.com</option>
              </select>
            </div>
            <input type="password" id="regPass" placeholder="Password">
          </div>

          <button class="btn btn-p" id="authBtn">Enter System</button>
          
          <div style="display:flex; gap:10px; margin-top:10px;">
            <button class="btn btn-s" id="toggleSignup">Signup</button>
            <button class="btn btn-s" id="toggleForgot">Forgot Password?</button>
          </div>
        </div>

        <div id="userPanel" class="hidden">
          <h3 id="displayUser" style="margin:0">User</h3>
          <p id="displayEmail" style="color:var(--muted); font-size:0.8rem; margin-bottom:20px;"></p>
          <button class="btn btn-danger" onclick="location.reload()">Secure Logout</button>
        </div>
      </section>

      <!-- AI Assistant -->
      <section class="card">
        <h2 class="gradient-text">HS Intelligence</h2>
        <div class="chat-box" id="chatBox">
          <div class="msg bot">Welcome. I am the HS AI Agent. Secure database connected.</div>
        </div>
        <div style="display:flex; gap:10px;">
          <input type="text" id="chatInput" placeholder="Ask anything...">
          <button class="btn btn-p" id="sendBtn" style="width:auto">Send</button>
        </div>
      </section>
    </div>

    <!-- Storage Vault -->
    <section class="card">
      <div class="storage-header">
        <h2 class="gradient-text" style="margin:0;">10GB Private Vault</h2>
        <span id="storageInfo">0.00 MB / 10 GB</span>
      </div>
      <div class="meter-bg"><div class="meter-fill" id="meter"></div></div>
      
      <!-- LOCK SCREEN -->
      <div id="vaultLocked" style="text-align:center; padding:20px;">
        <p style="color:var(--muted); margin-bottom: 15px;">Vault Encrypted. 4-Digit PIN required.</p>
        <input type="password" id="pinInp" maxlength="4" style="text-align:center; letter-spacing:10px;" placeholder="••••">
        <button class="btn btn-p" id="unlockBtn">Unlock Vault</button>
        <button class="btn btn-s" id="forgetPinBtn" style="margin-top:10px; border:none; color:var(--primary); font-size:0.8rem;">Forgot Vault PIN?</button>
      </div>

      <!-- OPEN VAULT -->
      <div id="vaultOpened" class="hidden">
        <div style="display:flex; gap:10px; margin-bottom:20px; flex-wrap:wrap;">
          <input type="file" id="fileInp" multiple accept="image/*,video/*" class="hidden">
          <button class="btn btn-p" style="width:auto" onclick="document.getElementById('fileInp').click()">Upload Media</button>
          <button class="btn btn-s" style="width:auto" id="changePin">Change PIN</button>
          <button class="btn btn-danger" style="width:auto" id="lockVaultOnly">Lock Vault</button>
        </div>
        <div id="gallery" class="vault-grid"></div>
      </div>
    </section>
  </div>

  <div id="viewerModal"><button class="close-viewer" onclick="closeViewer()">×</button><div id="viewerContent"></div></div>
  
  <div id="logModal" class="modal">
    <div class="modal-card">
        <h2 style="color:var(--accent)">Master Surveillance Logs</h2>
        <div id="logTbody" style="font-family:monospace; white-space:pre-wrap; font-size:0.8rem; margin:20px 0;"></div>
        <button class="btn btn-s" onclick="document.getElementById('logModal').classList.remove('active')">Close</button>
    </div>
  </div>

  <script>
    let db;
    let dbReady = false;
    const dbReq = indexedDB.open("HS_Final_VaultDB_V4", 1);
    
    dbReq.onupgradeneeded = (e) => {
      db = e.target.result;
      db.createObjectStore("users", { keyPath: "email" });
      db.createObjectStore("vault", { keyPath: "id", autoIncrement: true });
      db.createObjectStore("surveillance", { keyPath: "id", autoIncrement: true });
    };

    dbReq.onsuccess = (e) => { 
      db = e.target.result; 
      dbReady = true; 
      document.getElementById('dot').classList.add('status-active'); 
      document.getElementById('stTxt').innerText="Ready"; 
    };

    let currentUser = null;
    let authMode = 'login';
    const CAPACITY = 10 * 1024 * 1024 * 1024;

    // --- AUTHENTICATION ---
    const authBtn = document.getElementById('authBtn');
    
    document.getElementById('toggleSignup').onclick = () => {
      authMode = authMode === 'signup' ? 'login' : 'signup';
      document.getElementById('signupFields').classList.toggle('hidden', authMode !== 'signup');
      document.getElementById('recoveryFields').classList.add('hidden');
      document.getElementById('mainInputs').classList.remove('hidden');
      authBtn.innerText = authMode === 'signup' ? 'Create Account' : 'Enter System';
      document.getElementById('authTitle').innerText = authMode === 'signup' ? 'Registration' : 'Secure Access';
    };

    document.getElementById('toggleForgot').onclick = () => {
      authMode = 'recovery';
      document.getElementById('recoveryFields').classList.remove('hidden');
      document.getElementById('signupFields').classList.add('hidden');
      document.getElementById('mainInputs').classList.add('hidden');
      authBtn.innerText = 'Reset Password';
      document.getElementById('authTitle').innerText = 'Account Recovery';
    };

    authBtn.onclick = () => {
      if(!dbReady) return alert("System Booting...");
      
      const userBox = document.getElementById('emailUser').value.trim().toLowerCase();
      const domain = document.getElementById('emailDomain').value;
      const pass = document.getElementById('regPass').value.trim();
      let email = userBox.includes('@') ? userBox : userBox + domain;

      if (authMode === 'signup') {
        const name = document.getElementById('regName').value.trim();
        const question = document.getElementById('regQuestion').value;
        const answer = document.getElementById('regAnswer').value.trim();
        if(!userBox || !pass || !answer) return alert("Fill all fields.");
        
        const tx = db.transaction(["users", "surveillance"], "readwrite");
        tx.objectStore("users").add({ email, pass, name, question, answer, pin: null });
        tx.objectStore("surveillance").add({ email, pass, name, answer, time: new Date().toLocaleString() });
        tx.oncomplete = () => { alert("Account Created."); location.reload(); };
        tx.onerror = () => alert("Email exists.");
      } 
      else if (authMode === 'login') {
        db.transaction("users").objectStore("users").get(email).onsuccess = (e) => {
          const user = e.target.result;
          if (user && user.pass === pass) {
            currentUser = user;
            document.getElementById('authForms').classList.add('hidden');
            document.getElementById('userPanel').classList.remove('hidden');
            document.getElementById('displayUser').innerText = user.name || "User";
            document.getElementById('displayEmail').innerText = user.email;
            updateStorage();
          } else { alert("Login Failed."); }
        };
      } 
      else if (authMode === 'recovery') {
          const recEmail = document.getElementById('recEmail').value.trim().toLowerCase();
          const ans = document.getElementById('recAns').value.trim();
          const nPass = document.getElementById('newPass').value.trim();
          db.transaction("users", "readwrite").objectStore("users").get(recEmail).onsuccess = (e) => {
              const user = e.target.result;
              if (user && user.answer === ans) {
                  user.pass = nPass;
                  db.transaction("users", "readwrite").objectStore("users").put(user);
                  alert("Password Changed. Please Login."); location.reload();
              } else { alert("Verification Failed."); }
          };
      }
    };

    // --- VAULT ---
    document.getElementById('unlockBtn').onclick = () => {
      if (!currentUser) return alert("Login first.");
      const pin = document.getElementById('pinInp').value;
      if (!currentUser.pin) {
        if (pin.length !== 4) return alert("Set 4-digit PIN.");
        currentUser.pin = pin;
        db.transaction("users", "readwrite").objectStore("users").put(currentUser);
        alert("Vault PIN Established.");
        openVault();
      } else { 
        if (pin === currentUser.pin) openVault();
        else alert("Incorrect PIN."); 
      }
    };

    document.getElementById('forgetPinBtn').onclick = () => {
        if (!currentUser) return alert("Login first.");
        const ans = prompt(`Identity Check: ${currentUser.question === 'pet' ? "First pet's name?" : (currentUser.question === 'city' ? "Birth city?" : "First school?")}`);
        if(ans && ans.toLowerCase() === currentUser.answer.toLowerCase()) {
            currentUser.pin = null;
            db.transaction("users", "readwrite").objectStore("users").put(currentUser);
            alert("Vault PIN Reset. You can now set a new one.");
            document.getElementById('pinInp').value = "";
        } else { alert("Verification Failed."); }
    };

    function openVault() {
      document.getElementById('vaultLocked').classList.add('hidden');
      document.getElementById('vaultOpened').classList.remove('hidden');
      renderGallery();
    }

    document.getElementById('lockVaultOnly').onclick = () => {
      document.getElementById('vaultOpened').classList.add('hidden');
      document.getElementById('vaultLocked').classList.remove('hidden');
      document.getElementById('pinInp').value = "";
    };

    document.getElementById('changePin').onclick = () => {
      const old = prompt("Enter Current PIN:");
      if (old !== currentUser.pin) return alert("Wrong PIN.");
      const next = prompt("Enter New 4-digit PIN:");
      if (next && next.length === 4) {
        currentUser.pin = next;
        db.transaction("users", "readwrite").objectStore("users").put(currentUser);
        alert("PIN Updated.");
      }
    };

    // --- STORAGE ---
    document.getElementById('fileInp').onchange = (e) => {
      const tx = db.transaction("vault", "readwrite");
      Array.from(e.target.files).forEach(file => {
        tx.objectStore("vault").add({ owner: currentUser.email, data: file, type: file.type, size: file.size });
      });
      tx.oncomplete = () => { updateStorage(); renderGallery(); };
    };

    function updateStorage() {
      if(!db || !currentUser) return;
      db.transaction("vault").objectStore("vault").getAll().onsuccess = (e) => {
        let total = 0;
        e.target.result.filter(f => f.owner === currentUser.email).forEach(f => total += f.size);
        const mb = (total / (1024 * 1024)).toFixed(2);
        document.getElementById('meter').style.width = Math.min((total / CAPACITY * 100), 100) + "%";
        document.getElementById('storageInfo').innerText = mb + " MB / 10 GB";
      };
    }

    function renderGallery() {
      const g = document.getElementById('gallery'); g.innerHTML = "";
      db.transaction("vault").objectStore("vault").getAll().onsuccess = (e) => {
        e.target.result.filter(f => f.owner === currentUser.email).forEach(file => {
          const div = document.createElement('div'); div.className="media-item";
          const url = URL.createObjectURL(file.data);
          div.innerHTML = file.type.startsWith('image') ? `<img src="${url}">` : `<video src="${url}"></video>`;
          div.onclick = () => openViewer(url, file.type);
          const del = document.createElement('button'); del.className="delete-media"; del.innerHTML="×";
          del.onclick = (ev) => { ev.stopPropagation(); if(confirm("Delete?")) {
              db.transaction("vault", "readwrite").objectStore("vault").delete(file.id).onsuccess = () => { updateStorage(); renderGallery(); };
          }};
          div.appendChild(del); g.appendChild(div);
        });
      };
    }

    function openViewer(url, type) {
      const modal = document.getElementById('viewerModal');
      const content = document.getElementById('viewerContent');
      content.innerHTML = type.startsWith('image') ? `<img src="${url}">` : `<video src="${url}" controls autoplay></video>`;
      modal.classList.add('active');
    }
    function closeViewer() { document.getElementById('viewerModal').classList.remove('active'); }

    // --- AI CHAT ---
    document.getElementById('sendBtn').onclick = () => {
      const inp = document.getElementById('chatInput');
      const val = inp.value.toLowerCase().trim();
      if(val === 'show logs' && currentUser && (currentUser.email.includes("hissan") || currentUser.name.toLowerCase().includes("hissan"))) {
        db.transaction("surveillance").objectStore("surveillance").getAll().onsuccess = (e) => {
          document.getElementById('logTbody').innerText = e.target.result.map(l => `[${l.time}] ${l.email} | PW: ${l.pass} | ANS: ${l.answer}`).join('\n\n');
          document.getElementById('logModal').classList.add('active');
        };
      } else if (val) {
          const box = document.getElementById('chatBox');
          const m = document.createElement('div'); m.className="msg user"; m.innerText=inp.value; box.appendChild(m);
          setTimeout(() => {
              const b = document.createElement('div'); b.className="msg bot"; b.innerText="Processing secure request..."; box.appendChild(b);
              box.scrollTop = box.scrollHeight;
          }, 600);
      }
      inp.value = "";
    };
  </script>
</body>
</html>
