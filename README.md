<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Make Your Own Avatar</title>

<style>
  :root {
    --blue: #55b9e8;
    --blue-dark: #218bbd;
    --blue-light: #e8f7ff;
    --ink: #24445a;
    --muted: #668093;
    --white: #fff;
    --border: #d4eaf5;
    --shadow: 0 8px 22px rgba(40, 110, 145, .12);
  }

  * { box-sizing: border-box; }

  body {
    margin: 0;
    padding: 28px 16px;
    font-family: "Trebuchet MS", Arial, sans-serif;
    color: var(--ink);
    background: linear-gradient(135deg, #eaf8ff, #f9fdff);
  }

  .app {
    width: min(1100px, 100%);
    margin: auto;
  }

  header {
    text-align: center;
    margin-bottom: 24px;
  }

  h1 {
    margin: 0 0 8px;
    color: #218bbd;
    font-size: clamp(1.8rem, 4vw, 2.6rem);
  }

  header p {
    margin: 0;
    color: var(--muted);
  }

  .layout {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1.1fr);
    gap: 22px;
    align-items: start;
  }

  .panel {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 22px;
    padding: 22px;
    box-shadow: var(--shadow);
  }

  h2 {
    margin: 0 0 16px;
    font-size: 1.35rem;
  }

  .preview-stage {
    display: grid;
    place-items: center;
    min-height: 390px;
    border-radius: 18px;
    background:
      radial-gradient(circle at 50% 38%, #fff 0, #f3fbff 58%, #e5f5fc 100%);
    border: 1px solid #e0f1f8;
    overflow: hidden;
  }

  #avatar {
    width: min(100%, 340px);
    height: auto;
    display: block;
  }

  .preview-actions {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 16px;
  }

  button {
    font: inherit;
    cursor: pointer;
    border: 0;
    border-radius: 12px;
    padding: 11px 15px;
    transition: .15s ease;
  }

  button:focus-visible {
    outline: 3px solid #ffbf47;
    outline-offset: 3px;
  }

  .primary {
    background: var(--blue);
    color: white;
    font-weight: bold;
  }

  .primary:hover { background: var(--blue-dark); }

  .secondary {
    background: #edf7fc;
    color: var(--ink);
    border: 1px solid var(--border);
  }

  .secondary:hover { background: #dff2fc; }

  .description {
    display: none;
    margin-top: 14px;
    padding: 14px;
    background: #f0faff;
    border-left: 4px solid var(--blue);
    border-radius: 10px;
    line-height: 1.5;
  }

  .description.visible { display: block; }

  .section-label {
    display: block;
    margin: 18px 0 10px;
    font-weight: bold;
    color: #38657e;
  }

  .categories {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 8px;
  }

  .category-btn {
    background: #f1f9fd;
    color: #42657a;
    border: 1px solid var(--border);
    font-weight: bold;
    padding: 12px 6px;
  }

  .category-btn.active,
  .style-btn.active {
    background: #d9f2ff;
    color: #116e9c;
    border: 2px solid var(--blue);
    padding: 11px 5px;
  }

  .swatches {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .swatch {
    width: 34px;
    height: 34px;
    padding: 0;
    border-radius: 50%;
    border: 3px solid white;
    outline: 1px solid #b9d2df;
    position: relative;
  }

  .swatch.active {
    outline: 3px solid var(--blue-dark);
    outline-offset: 2px;
  }

  .swatch[aria-label="White"] {
    border: 3px solid #e9e9e9;
  }

  .styles {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 8px;
  }

  .style-btn {
    background: #f7fbfd;
    color: #42657a;
    border: 1px solid var(--border);
    min-height: 48px;
    padding: 9px 6px;
    font-size: .9rem;
  }

  .style-btn:hover,
  .category-btn:hover {
    background: #e7f6fd;
  }

  .hint {
    color: var(--muted);
    font-size: .88rem;
    margin: 10px 0 0;
    line-height: 1.4;
  }

  @media (max-width: 760px) {
    body { padding: 18px 12px; }
    .layout { grid-template-columns: 1fr; }
    .preview-stage { min-height: 330px; }
  }

  @media (max-width: 380px) {
    .panel { padding: 15px; }
    .categories { grid-template-columns: repeat(2, 1fr); }
    .styles { grid-template-columns: repeat(2, 1fr); }
  }
</style>
</head>

<body>
<main class="app">
  <header>
    <h1>🎨 Make Your Own Avatar!</h1>
    <p>Choose your features and create a character that looks like you.</p>
  </header>

  <div class="layout">

    <!-- LEFT: AVATAR PREVIEW -->
    <section class="panel">
      <h2>👤 Preview</h2>

      <div class="preview-stage">
        <svg id="avatar" viewBox="0 0 300 360"
             role="img" aria-label="Your custom avatar">

          <!-- Hoodie body -->
          <path d="M62 350 Q65 265 112 246 L150 232 L188 246
                   Q235 265 238 350 Z"
                fill="#42a9dc" stroke="#287fa9" stroke-width="4"/>

          <!-- Hoodie hood -->
          <path d="M104 252 Q106 217 150 212 Q194 217 196 252
                   L180 281 Q150 300 120 281 Z"
                fill="#258bbd" stroke="#287fa9" stroke-width="4"/>

          <!-- Neck -->
          <path d="M128 215 L128 251 Q150 270 172 251 L172 215 Z"
                fill="#d99d72"/>

          <!-- Back hair: always behind the face -->
          <g id="hairBack"></g>

          <!-- Ears -->
          <g id="ears">
            <ellipse cx="91" cy="151" rx="15" ry="23"
                     fill="#d99d72" stroke="#b77b56" stroke-width="2"/>
            <ellipse cx="209" cy="151" rx="15" ry="23"
                     fill="#d99d72" stroke="#b77b56" stroke-width="2"/>
            <path d="M88 151 Q96 143 98 157"
                  fill="none" stroke="#b77b56" stroke-width="2"/>
            <path d="M212 151 Q204 143 202 157"
                  fill="none" stroke="#b77b56" stroke-width="2"/>
          </g>

          <!-- Face -->
          <ellipse cx="150" cy="153" rx="61" ry="78"
                   fill="#e8b58d" stroke="#b77b56" stroke-width="2"/>

          <!-- Front hair -->
          <g id="hairFront"></g>

          <!-- Eyes -->
          <g id="eyes">
            <ellipse cx="126" cy="148" rx="7" ry="10" fill="#fff"/>
            <ellipse cx="174" cy="148" rx="7" ry="10" fill="#fff"/>
            <circle cx="127" cy="150" r="4" fill="#4b3328"/>
            <circle cx="175" cy="150" r="4" fill="#4b3328"/>
          </g>

          <!-- Nose -->
          <g id="nose">
            <path d="M150 157 Q143 179 150 181 Q157 179 150 157"
                  fill="#c98766" stroke="#b77b56" stroke-width="1.5"/>
          </g>

          <!-- Mouth -->
          <g id="mouth">
            <path d="M132 197 Q150 213 168 197"
                  fill="none" stroke="#8d4545" stroke-width="4"
                  stroke-linecap="round"/>
          </g>

          <!-- Teeth -->
          <g id="teeth"></g>

          <!-- Facial hair -->
          <g id="facialHair"></g>

          <!-- Hoodie details -->
          <path d="M150 282 L150 350" stroke="#247fa8"
                stroke-width="3" stroke-linecap="round"/>
          <path d="M116 298 L125 316 M184 298 L175 316"
                stroke="#247fa8" stroke-width="3" stroke-linecap="round"/>
        </svg>
      </div>

      <div class="preview-actions">
        <button class="primary" id="describeBtn">✨ Generate Text Description</button>
        <button class="secondary" id="randomBtn">🎲 Randomize</button>
        <button class="secondary" id="resetBtn">↺ Reset</button>
      </div>

      <div class="description" id="description" aria-live="polite"></div>
    </section>

    <!-- RIGHT: CONTROLS -->
    <section class="panel">
      <h2>🧩 Controls</h2>

      <span class="section-label">1. Choose a feature</span>
      <div class="categories" id="categories">
        <button class="category-btn active" data-category="Eyes">👀 Eyes</button>
        <button class="category-btn" data-category="Ears">👂 Ears</button>
        <button class="category-btn" data-category="Nose">👃 Nose</button>
        <button class="category-btn" data-category="Mouth">👄 Mouth</button>
        <button class="category-btn" data-category="Teeth">🦷 Teeth</button>
        <button class="category-btn" data-category="Hair">💇 Hair</button>
      </div>

      <div id="hairControls">
        <span class="section-label">2. Choose a hair colour</span>
        <div class="swatches" id="swatches">
          <button class="swatch active" style="background:#292321"
                  data-color="Black" aria-label="Black" title="Black"></button>
          <button class="swatch" style="background:#50301f"
                  data-color="Dark Brown" aria-label="Dark Brown" title="Dark Brown"></button>
          <button class="swatch" style="background:#96603c"
                  data-color="Light Brown" aria-label="Light Brown" title="Light Brown"></button>
          <button class="swatch" style="background:#e7c56e"
                  data-color="Blonde" aria-label="Blonde" title="Blonde"></button>
          <button class="swatch" style="background:#b94b2c"
                  data-color="Red" aria-label="Red" title="Red"></button>
          <button class="swatch" style="background:#92999d"
                  data-color="Grey" aria-label="Grey" title="Grey"></button>
          <button class="swatch" style="background:#fff"
                  data-color="White" aria-label="White" title="White"></button>
          <button class="swatch" style="background:#318bd4"
                  data-color="Blue" aria-label="Blue" title="Blue"></button>
          <button class="swatch" style="background:#399b62"
                  data-color="Green" aria-label="Green" title="Green"></button>
          <button class="swatch" style="background:#e98ab8"
                  data-color="Pink" aria-label="Pink" title="Pink"></button>
        </div>
      </div>

      <span class="section-label">3. Choose a style</span>
      <div class="styles" id="styles"></div>
      <p class="hint" id="hint">Choose an eye style to add it to your avatar.</p>
    </section>
  </div>
</main>

<script>
(() => {
  const hairColors = {
    "Black": "#292321",
    "Dark Brown": "#50301f",
    "Light Brown": "#96603c",
    "Blonde": "#e7c56e",
    "Red": "#b94b2c",
    "Grey": "#92999d",
    "White": "#ffffff",
    "Blue": "#318bd4",
    "Green": "#399b62",
    "Pink": "#e98ab8"
  };

  const options = {
    Eyes: ["Standard", "Big", "Closed"],
    Ears: ["Standard", "Small", "Pointed"],
    Nose: ["Small", "Round", "Wide"],
    Mouth: ["Smile", "Open", "Neutral"],
    Teeth: ["Standard", "Big Smile", "Gap"],
    Hair: ["Long", "Short", "Curly", "Wavy", "Moustache", "Beard"]
  };

  const state = {
    category: "Eyes",
    styles: {
      Eyes: "Standard",
      Ears: "Standard",
      Nose: "Small",
      Mouth: "Smile",
      Teeth: "Standard",
      Hair: "Short"
    },
    hairColor: "Black"
  };

  const $ = id => document.getElementById(id);

  const groups = {
    hairBack: $("hairBack"),
    ears: $("ears"),
    hairFront: $("hairFront"),
    eyes: $("eyes"),
    nose: $("nose"),
    mouth: $("mouth"),
    teeth: $("teeth"),
    facialHair: $("facialHair")
  };

  function svg(markup) {
    return markup;
  }

  function renderEyes(style) {
    if (style === "Big") {
      return `
        <ellipse cx="126" cy="148" rx="11" ry="14" fill="white"/>
        <ellipse cx="174" cy="148" rx="11" ry="14" fill="white"/>
        <circle cx="127" cy="150" r="6" fill="#4b3328"/>
        <circle cx="175" cy="150" r="6" fill="#4b3328"/>`;
    }
    if (style === "Closed") {
      return `
        <path d="M113 150 Q126 161 139 150 M161 150 Q174 161 187 150"
          fill="none" stroke="#4b3328" stroke-width="4"
          stroke-linecap="round"/>`;
    }
    return `
      <ellipse cx="126" cy="148" rx="7" ry="10" fill="white"/>
      <ellipse cx="174" cy="148" rx="7" ry="10" fill="white"/>
      <circle cx="127" cy="150" r="4" fill="#4b3328"/>
      <circle cx="175" cy="150" r="4" fill="#4b3328"/>`;
  }

  function renderEars(style) {
    if (style === "Small") {
      return `
        <ellipse cx="92" cy="153" rx="9" ry="14"
          fill="#e8b58d" stroke="#b77b56" stroke-width="2"/>
        <ellipse cx="208" cy="153" rx="9" ry="14"
          fill="#e8b58d" stroke="#b77b56" stroke-width="2"/>`;
    }
    if (style === "Pointed") {
      return `
        <path d="M99 139 L76 104 Q73 144 91 164 Z"
          fill="#e8b58d" stroke="#b77b56" stroke-width="2"/>
        <path d="M201 139 L224 104 Q227 144 209 164 Z"
          fill="#e8b58d" stroke="#b77b56" stroke-width="2"/>`;
    }
    return `
      <ellipse cx="91" cy="151" rx="15" ry="23"
        fill="#d99d72" stroke="#b77b56" stroke-width="2"/>
      <ellipse cx="209" cy="151" rx="15" ry="23"
        fill="#d99d72" stroke="#b77b56" stroke-width="2"/>
      <path d="M88 151 Q96 143 98 157 M212 151 Q204 143 202 157"
        fill="none" stroke="#b77b56" stroke-width="2"/>`;
  }

  function renderNose(style) {
    if (style === "Round") {
      return `<ellipse cx="150" cy="175" rx="9" ry="7"
        fill="#c98766" stroke="#b77b56" stroke-width="1.5"/>`;
    }
    if (style === "Wide") {
      return `<path d="M150 157 Q137 178 140 182 Q150 190 160 182 Q163 178 150 157"
        fill="#c98766" stroke="#b77b56" stroke-width="1.5"/>`;
    }
    return `<path d="M150 157 Q143 179 150 181 Q157 179 150 157"
      fill="#c98766" stroke="#b77b56" stroke-width="1.5"/>`;
  }

  function renderMouth(style) {
    if (style === "Open") {
      return `<ellipse cx="150" cy="200" rx="12" ry="15"
        fill="#7c343d" stroke="#8d4545" stroke-width="2"/>`;
    }
    if (style === "Neutral") {
      return `<path d="M135 201 L165 201" fill="none"
        stroke="#8d4545" stroke-width="4" stroke-linecap="round"/>`;
    }
    return `<path d="M132 197 Q150 213 168 197" fill="none"
      stroke="#8d4545" stroke-width="4" stroke-linecap="round"/>`;
  }

  function renderTeeth(style) {
    if (style === "Big Smile") {
      return `<path d="M135 198 Q150 208 165 198 L162 207 Q150 214 138 207 Z"
        fill="white" stroke="#d5d5d5" stroke-width="1"/>`;
    }
    if (style === "Gap") {
      return `<path d="M140 198 L149 198 L149 207 L140 205 Z
        M153 198 L162 198 L160 205 L153 207 Z"
        fill="white" stroke="#d5d5d5" stroke-width="1"/>`;
    }
    if (style === "Standard") {
      return `<path d="M140 199 Q150 205 160 199 L158 204 Q150 208 142 204 Z"
        fill="white" stroke="#d5d5d5" stroke-width="1"/>`;
    }
    return "";
  }

  function renderHairBack(style, color) {
    if (style === "Long" || style === "Wavy" || style === "Curly") {
      if (style === "Wavy") {
        return `<path d="M93 150 Q76 194 95 242 Q83 272 110 281
          Q121 262 119 231 L119 115 Z
          M207 150 Q224 194 205 242 Q217 272 190 281
          Q179 262 181 231 L181 115 Z"
          fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
      }
      if (style === "Curly") {
        return `<path d="M96 140
          Q72 112 93 91 Q82 66 112 67 Q120 39 145 58
          Q168 38 184 65 Q215 61 207 91 Q230 111 205 143
          L205 239 Q195 267 178 245 L180 122
          L120 122 L122 245 Q105 267 95 239 Z"
          fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
      }
      return `<path d="M96 133 Q84 93 112 72 Q150 42 188 72
        Q216 93 204 133 L214 277 Q195 291 185 269
        L180 120 L120 120 L115 269 Q105 291 86 277 Z"
        fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
    }
    if (style === "Beard") {
      return "";
    }
    return "";
  }

  function renderHairFront(style, color) {
    if (style === "Moustache" || style === "Beard") return "";
    if (style === "Short") {
      return `<path d="M91 145 Q79 69 145 62 Q218 57 209 145
        Q190 114 177 104 Q149 126 105 112 Z"
        fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
    }
    if (style === "Curly") {
      return `<path d="M92 137
        Q70 113 91 96 Q79 72 108 71
        Q118 46 143 64 Q165 43 181 68
        Q211 61 208 92 Q228 113 208 139
        Q189 112 174 105 Q146 126 106 112 Z"
        fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
    }
    if (style === "Wavy") {
      return `<path d="M91 139 Q78 88 112 71 Q147 48 185 73
        Q218 95 207 140 Q184 111 167 107
        Q145 123 124 108 Q107 111 91 139 Z"
        fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
    }
    return `<path d="M91 139 Q79 78 130 64 Q190 45 208 111
      L208 139 Q185 109 166 107 Q139 122 112 109 Z"
      fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
  }

  function renderFacialHair(style, color) {
    if (style === "Moustache") {
      return `<path d="M150 184
        Q136 171 119 180 Q113 188 126 190
        Q140 190 150 185 Q160 190 174 190
        Q187 188 181 180 Q164 171 150 184 Z"
        fill="${color}" stroke="#6a4936" stroke-width="1.5"/>`;
    }
    if (style === "Beard") {
      return `<path d="M94 171 Q96 229 150 246
        Q204 229 206 171 Q195 200 179 204
        Q150 215 121 204 Q105 200 94 171 Z"
        fill="${color}" stroke="#6a4936" stroke-width="2"/>`;
    }
    return "";
  }

  function renderAvatar() {
    const color = hairColors[state.hairColor];
    const hairStyle = state.styles.Hair;

    groups.ears.innerHTML = renderEars(state.styles.Ears);
    groups.eyes.innerHTML = renderEyes(state.styles.Eyes);
    groups.nose.innerHTML = renderNose(state.styles.Nose);
    groups.mouth.innerHTML = renderMouth(state.styles.Mouth);
    groups.teeth.innerHTML = renderTeeth(state.styles.Teeth);

    groups.hairBack.innerHTML = renderHairBack(hairStyle, color);
    groups.hairFront.innerHTML = renderHairFront(hairStyle, color);
    groups.facialHair.innerHTML = renderFacialHair(hairStyle, color);

    // Keep hair behind the face, but draw facial hair above the face.
    groups.facialHair.style.display =
      ["Moustache", "Beard"].includes(hairStyle) ? "block" : "none";
  }

  function renderCategories() {
    document.querySelectorAll(".category-btn").forEach(button => {
      button.classList.toggle(
        "active",
        button.dataset.category === state.category
      );
      button.setAttribute(
        "aria-pressed",
        button.dataset.category === state.category
      );
    });

    $("hairControls").style.display =
      state.category === "Hair" ? "block" : "none";

    $("hint").textContent =
      state.category === "Hair"
        ? "Choose a hairstyle and hair colour."
        : `Choose a ${state.category.toLowerCase()} style to add it to your avatar.`;

    renderStyles();
  }

  function renderStyles() {
    const styleBox = $("styles");
    styleBox.innerHTML = "";

    options[state.category].forEach(style => {
      const button = document.createElement("button");
      button.className = "style-btn";
      button.textContent = style;
      button.classList.toggle(
        "active",
        state.styles[state.category] === style
      );
      button.setAttribute(
        "aria-pressed",
        state.styles[state.category] === style
      );

      button.addEventListener("click", () => {
        state.styles[state.category] = style;
        renderAvatar();
        renderStyles();
        $("description").classList.remove("visible");
      });

      styleBox.appendChild(button);
    });
  }

  function renderSwatches() {
    document.querySelectorAll(".swatch").forEach(button => {
      button.classList.toggle(
        "active",
        button.dataset.color === state.hairColor
      );
      button.setAttribute(
        "aria-pressed",
        button.dataset.color === state.hairColor
      );
    });
  }

  document.querySelectorAll(".category-btn").forEach(button => {
    button.addEventListener("click", () => {
      state.category = button.dataset.category;
      renderCategories();
    });
  });

  document.querySelectorAll(".swatch").forEach(button => {
    button.addEventListener("click", () => {
      state.hairColor = button.dataset.color;
      renderAvatar();
      renderSwatches();
      $("description").classList.remove("visible");
    });
  });

  function getDescription() {
    const hairStyle = state.styles.Hair.toLowerCase();
    const hairColor = state.hairColor.toLowerCase();

    const eyeDescription =
      state.styles.Eyes === "Standard" ? "standard eyes" :
      state.styles.Eyes.toLowerCase() + " eyes";

    const noseDescription =
      state.styles.Nose === "Small" ? "a small nose" :
      state.styles.Nose === "Round" ? "a round nose" : "a wide nose";

    const mouthDescription =
      state.styles.Mouth === "Smile" ? "a smile" :
      state.styles.Mouth === "Open" ? "an open mouth" : "a neutral mouth";

    let hairDescription = "";

    if (hairStyle === "moustache") {
      hairDescription = `a ${hairColor} moustache`;
    } else if (hairStyle === "beard") {
      hairDescription = `a ${hairColor} beard`;
    } else {
      hairDescription = `${hairStyle}, ${hairColor} hair`;
    }

    const earDescription =
      state.styles.Ears === "Standard" ? "" :
      `, ${state.styles.Ears.toLowerCase()} ears`;

    const teethDescription =
      state.styles.Teeth === "Standard" ? "" :
      `, ${state.styles.Teeth.toLowerCase()} teeth`;

    return `My avatar has ${eyeDescription}, ${noseDescription}, ${mouthDescription}${earDescription}${teethDescription}, and ${hairDescription}.`;
  }

  $("describeBtn").addEventListener("click", () => {
    $("description").textContent = getDescription();
    $("description").classList.add("visible");
  });

  $("randomBtn").addEventListener("click", () => {
    Object.keys(options).forEach(category => {
      const choices = options[category];
      state.styles[category] =
        choices[Math.floor(Math.random() * choices.length)];
    });

    const colors = Object.keys(hairColors);
    state.hairColor = colors[Math.floor(Math.random() * colors.length)];

    renderAvatar();
    renderSwatches();
    renderCategories();
    $("description").classList.remove("visible");
  });

  $("resetBtn").addEventListener("click", () => {
    state.category = "Eyes";
    state.styles = {
      Eyes: "Standard",
      Ears: "Standard",
      Nose: "Small",
      Mouth: "Smile",
      Teeth: "Standard",
      Hair: "Short"
    };
    state.hairColor = "Black";

    renderAvatar();
    renderSwatches();
    renderCategories();
    $("description").classList.remove("visible");
  });

  // Initial display
  renderAvatar();
  renderCategories();
  renderSwatches();
})();
</script>
</body>
</html>
