<!DOCTYPE html>
<html>
<head>
<title>For You 🌙</title>

<style>
/* 🌌 BODY & RESET */
body {
  margin: 0;
  padding: 0;
  font-family: 'Courier New', monospace; /* Classic typewriter font */
  overflow: hidden;
  background-color: #000; /* Black base for fading */
  color: #cce6ff;
}

/* 🎆 DYNAMIC WALLPAPER LAYER */
/* This sits behind everything else to handle the smooth slideshow */
#wallpaper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  z-index: 1; /* Lowest layer */
  transition: opacity 1.5s ease-in-out; /* The Smooth Fade Magic */
  opacity: 0.4; /* Slightly dim to make text readable */
}

/* 🔐 LOCK SCREEN */
#lockScreen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 100; /* Top layer */
  
  /* LOCK SCREEN SPECIFIC BACKGROUND */
  background: url('https://images.unsplash.com/photo-1518066000714-58c45f1a2c0a?q=80&w=2070&auto=format&fit=crop') no-repeat center center;
  background-size: cover;
  
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: opacity 1s ease;
}

/* LOCK SCREEN BOX STYLING */
.lock-box {
  background: rgba(0, 0, 0, 0.6);
  padding: 40px;
  border-radius: 20px;
  backdrop-filter: blur(5px);
  box-shadow: 0 0 30px rgba(0, 100, 255, 0.5);
  text-align: center;
}

#notif {
  display: none;
  margin-top: 15px;
  color: #ff6b6b;
  font-weight: bold;
}

/* 💙 MAIN CONTENT CONTAINER */
#mainContent {
  display: none; /* Hidden until password entered */
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* TRUE CENTERING */
  
  width: 85%;
  max-width: 900px;
  background: rgba(0, 10, 30, 0.65); /* Dark semi-transparent box */
  padding: 40px;
  border-radius: 20px;
  box-shadow: 0 0 40px rgba(0, 150, 255, 0.4);
  z-index: 50;
  
  /* 3D Opening Animation */
  opacity: 0;
  transition: opacity 2s ease;
}

#mainContent.show {
  opacity: 1;
}

/* 🖼 CONTENT LAYOUT */
.content-wrapper {
  display: flex;
  align-items: center;
  justify-content: center; /* Center items horizontally */
  flex-wrap: wrap; /* Wraps on mobile */
  gap: 50px;
}

/* IMAGE STYLE */
.polaroid {
  width: 280px;
  height: auto;
  border: 10px solid white;
  border-bottom: 40px solid white;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
  transform: rotate(-3deg); /* Cute tilt */
}

/* LETTER STYLE */
#letter {
  flex: 1;
  min-width: 300px;
  white-space: pre-wrap;
  font-size: 1.1rem;
  line-height: 1.6;
  text-shadow: 0 2px 4px rgba(0,0,0,0.8);
  text-align: left; /* Keep text left aligned for reading */
}

/* CONTROLS */
input {
  padding: 12px;
  border-radius: 30px;
  border: none;
  outline: none;
  text-align: center;
  font-family: inherit;
  margin-bottom: 10px;
}
button {
  padding: 10px 25px;
  border-radius: 30px;
  border: none;
  background: #0066cc;
  color: white;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.3s;
}
button:hover { background: #0099ff; }

</style>
</head>

<body>

<div id="wallpaper"></div>

<div id="lockScreen">
  <div class="lock-box">
    <h2>Enter Our Anniversary 🌙</h2>
    <p style="font-size: 0.8em; opacity: 0.8;">Hint: MMDD</p>
    <input type="password" id="password" placeholder="****">
    <br>
    <button onclick="checkPassword()">Open Heart</button>
    <div id="notif">Wrong date 💔 Try again!</div>
  </div>
</div>

<div id="mainContent">
  <div class="content-wrapper">
    <img class="polaroid" src="https://i.postimg.cc/xdtdTfTV/att-Qo-I8v1bz-9hex4Mg-K9w0e-BVgi-Ht-GFvspc-FQgv60Sm0-jpg.jpg  .jpg">

    <div id="letter"></div>
  </div>

  <audio id="music" src="YOUR_MUSIC_LINK_HERE.mp3" loop></audio>
</div>

<script>
// 🔁 BACKGROUND CONFIGURATION
// Add your background image URLs here for the slideshow
const backgrounds = [
  "https://i.postimg.cc/jSCGpRw1/bef756289cb149328698f763e120545c.jpg",
  "https://i.postimg.cc/pT9rrw63/att-g-HXoqj9Se-Jn9Qwdrho-Cmvgqnw0Y21d6Mt-XKVfnk1Pg-E-jpg.jpg",
  "https://i.postimg.cc/xdtdTfTV/att-Qo-I8v1bz-9hex4Mg-K9w0e-BVgi-Ht-GFvspc-FQgv60Sm0-jpg.jpg"
];

let bgIndex = 0;
const wallpaper = document.getElementById("wallpaper");

function startSlideshow() {
  // Initial set
  wallpaper.style.backgroundImage = `url('${backgrounds[0]}')`;
  
  setInterval(() => {
    // 1. Fade Out
    wallpaper.style.opacity = "0";
    
    setTimeout(() => {
      // 2. Change Image (while invisible)
      bgIndex = (bgIndex + 1) % backgrounds.length;
      wallpaper.style.backgroundImage = `url('${backgrounds[bgIndex]}')`;
      
      // 3. Fade In
      wallpaper.style.opacity = "0.4"; // Back to target opacity
    }, 1500); // Wait for fade out to finish (matches CSS transition)
    
  }, 5000); // Change every 8 seconds
}

// 💙 PASSWORD CHECK
function checkPassword() {
  const input = document.getElementById("password").value;
  const lockScreen = document.getElementById("lockScreen");
  const mainContent = document.getElementById("mainContent");
  const music = document.getElementById("music");

  if(input === "0214") { // CHANGE DATE HERE
    // 1. Fade out lock screen
    lockScreen.style.opacity = "0";
    setTimeout(() => { lockScreen.style.display = "none"; }, 1000);

    // 2. Show Main Content
    mainContent.style.display = "block";
    setTimeout(() => { mainContent.classList.add("show"); }, 100);

    // 3. Start Features
    music.play().catch(e => console.log("Audio requires interaction"));
    startSlideshow(); // Start the background fade loop
    typeLetter();     // Start typing text
  } else {
    const notif = document.getElementById("notif");
    notif.style.display = "block";
    setTimeout(()=>{ notif.style.display = "none"; }, 2000);
  }
}

// ⌨️ TYPING EFFECT
const text = "Hi love...\n\nUnder this same night sky,\nI just want you to know\nthat meeting you\nwas my favorite coincidence.\n\nYou are my calm.\nMy light.\nMy always.\n\nHappy Anniversary 🌙💙";
let charIndex = 0;

function typeLetter() {
  if (charIndex < text.length) {
    document.getElementById("letter").innerHTML += text.charAt(charIndex);
    charIndex++;
    setTimeout(typeLetter, 50);
  }
}
</script>
</body>
</html>
