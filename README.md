<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UP Board Physics Master - Anmol Singh</title>
    <style>
        :root {
            --primary: #1a237e; /* Deep Blue */
            --accent: #ff6f00;  /* Amber */
            --bg: #f5f6fa;
            --text: #2d3436;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            background: var(--bg);
            color: var(--text);
            padding-top: 60px; /* Space for watermark */
        }

        /* --- WATERMARK --- */
        .watermark {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: linear-gradient(90deg, #000000, #333333);
            color: rgba(255, 255, 255, 0.9);
            text-align: center;
            padding: 10px 0;
            font-size: 1.2rem;
            font-weight: bold;
            letter-spacing: 2px;
            z-index: 1000;
            text-transform: uppercase;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }

        header {
            background: var(--primary);
            color: white;
            padding: 2rem 1rem;
            text-align: center;
        }
        
        nav {
            display: flex;
            justify-content: center;
            background: white;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            position: sticky;
            top: 45px; /* Below watermark */
            z-index: 900;
        }
        nav button {
            background: none;
            border: none;
            padding: 15px 30px;
            font-size: 1rem;
            font-weight: 600;
            color: #555;
            cursor: pointer;
            transition: 0.3s;
            border-bottom: 3px solid transparent;
        }
        nav button.active {
            color: var(--primary);
            border-bottom: 3px solid var(--primary);
            background: #eef2ff;
        }

        .container {
            max-width: 900px;
            margin: 30px auto;
            padding: 0 20px;
        }

        /* --- TOPIC CARDS --- */
        .unit-header {
            margin-top: 40px;
            color: var(--primary);
            border-left: 5px solid var(--accent);
            padding-left: 15px;
        }

        .card {
            background: white;
            border-radius: 12px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            overflow: hidden;
            transition: transform 0.2s;
        }
        .card:hover { transform: translateY(-2px); }

        .card-header {
            padding: 20px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: 700;
            font-size: 1.1rem;
            background: white;
            border-bottom: 1px solid #f0f0f0;
        }
        .card-header:hover { color: var(--accent); }
        
        .card-body {
            padding: 25px;
            display: none;
            background: #fff;
        }

        /* --- EXPLANATION STYLES --- */
        .simple-story {
            background: #fff8e1;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 20px;
            border: 1px solid #ffe0b2;
        }
        .story-title {
            color: var(--accent);
            font-weight: bold;
            display: block;
            margin-bottom: 5px;
            text-transform: uppercase;
            font-size: 0.85rem;
        }

        .derivation {
            font-family: 'Courier New', monospace;
            background: #f8f9fa;
            padding: 15px;
            border-radius: 5px;
            border-left: 3px solid var(--primary);
            margin-top: 15px;
            white-space: pre-wrap;
        }

        /* --- ANIMATION CANVAS --- */
        .anim-stage {
            width: 100%;
            height: 200px;
            background: #222;
            border-radius: 8px;
            position: relative;
            overflow: hidden;
            margin: 15px 0;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
        }

        /* --- ANIMATION KEYFRAMES --- */
        
        /* 1. Dipole Field */
        .charge { width: 30px; height: 30px; border-radius: 50%; position: absolute; top: 50%; margin-top: -15px; display: flex; align-items: center; justify-content: center; font-weight: bold; color: white; box-shadow: 0 0 15px rgba(255,255,255,0.5); }
        .plus { background: #e74c3c; left: 25%; }
        .minus { background: #3498db; right: 25%; }
        .field-arrow {
            position: absolute; top: 50%; left: 30%; width: 40%; height: 2px; background: rgba(255,255,255,0.5);
            animation: flowRight 1s linear infinite;
        }
        @keyframes flowRight { 0% { width: 0; opacity: 0; left: 28%; } 50% { opacity: 1; } 100% { width: 44%; opacity: 0; left: 28%; } }

        /* 2. Capacitor */
        .plate { width: 10px; height: 120px; background: silver; position: absolute; top: 40px; }
        .plate-left { left: 30%; border-right: 2px solid #e74c3c; }
        .plate-right { right: 30%; border-left: 2px solid #3498db; }
        .field-lines {
            position: absolute; left: 32%; top: 60px; width: 36%; height: 2px; background: yellow;
            box-shadow: 0 20px 0 yellow, 0 40px 0 yellow, 0 60px 0 yellow;
            animation: pulseField 2s infinite;
        }
        @keyframes pulseField { 0% { opacity: 0.3; } 50% { opacity: 1; } 100% { opacity: 0.3; } }

        /* 3. Drift Velocity */
        .wire-tube { width: 80%; height: 60px; border: 2px solid #555; position: absolute; left: 10%; top: 70px; border-radius: 30px; }
        .electron {
            width: 8px; height: 8px; background: #00ff00; border-radius: 50%; position: absolute; top: 25px;
            animation: drift 3s linear infinite, jitter 0.2s ease-in-out infinite alternate;
        }
        @keyframes drift { 0% { left: 0; opacity: 0; } 10% { opacity: 1;} 90% { opacity: 1; } 100% { left: 100%; opacity: 0; } }
        @keyframes jitter { from { margin-top: -5px; } to { margin-top: 5px; } }

        /* 4. Prism/Ray */
        .prism-tri {
            width: 0; height: 0; border-left: 60px solid transparent; border-right: 60px solid transparent; border-bottom: 100px solid rgba(255,255,255,0.2);
            position: absolute; left: 50%; top: 50px; transform: translateX(-50%);
        }
        .light-ray {
            height: 2px; background: white; position: absolute; top: 100px; left: 0; width: 35%; transform: rotate(15deg); transform-origin: right center;
        }
        .refracted-ray {
            height: 2px; background: cyan; position: absolute; top: 113px; left: 35%; width: 30%; transform: rotate(0deg);
        }
        .emergent-ray {
            height: 2px; background: white; position: absolute; top: 113px; left: 65%; width: 35%; transform: rotate(25deg); transform-origin: left center;
        }

        /* 5. Waves YDSE */
        .slit-wall { width: 4px; height: 100%; background: #555; position: absolute; left: 20%; }
        .slit-hole { width: 4px; height: 20px; background: #222; position: absolute; left: 20%; }
        .s1 { top: 60px; } .s2 { top: 120px; }
        .ripple {
            position: absolute; border: 2px solid rgba(0, 255, 255, 0.5); border-radius: 50%; opacity: 0;
            animation: rippleExpand 3s linear infinite;
        }
        @keyframes rippleExpand { 0% { width: 0; height: 0; opacity: 1; border-width: 2px; } 100% { width: 300px; height: 300px; opacity: 0; border-width: 0; } }

        /* 6. Photoelectric */
        .metal-surf { width: 100%; height: 10px; background: #7f8c8d; position: absolute; bottom: 20px; }
        .photon-w { width: 4px; height: 20px; background: yellow; position: absolute; top: 0; animation: fall 1.5s linear infinite; }
        .e-eject { width: 8px; height: 8px; background: cyan; border-radius: 50%; position: absolute; bottom: 30px; animation: flyUp 1.5s ease-out infinite; opacity: 0; }
        @keyframes fall { 0% { top: -20px; } 80% { top: 170px; opacity: 1; } 100% { top: 170px; opacity: 0; } }
        @keyframes flyUp { 0% { opacity: 0; bottom: 30px; } 50% { opacity: 1; } 100% { bottom: 180px; left: 150px; opacity: 0; } }

        /* 7. PN Junction */
        .p-side { position: absolute; left: 20%; top: 50px; width: 30%; height: 100px; background: rgba(231, 76, 60, 0.2); border: 1px solid red; display: flex; align-items: center; justify-content: center; color: white; }
        .n-side { position: absolute; right: 20%; top: 50px; width: 30%; height: 100px; background: rgba(52, 152, 219, 0.2); border: 1px solid blue; display: flex; align-items: center; justify-content: center; color: white; }
        .hole { width: 10px; height: 10px; border: 1px solid white; border-radius: 50%; position: absolute; animation: moveRight 2s infinite; }
        .electron-dot { width: 10px; height: 10px; background: cyan; border-radius: 50%; position: absolute; animation: moveLeft 2s infinite; }
        @keyframes moveRight { 0% { left: 25%; top: 90px; opacity: 1; } 100% { left: 50%; top: 90px; opacity: 0; } }
        @keyframes moveLeft { 0% { right: 25%; top: 100px; opacity: 1; } 100% { right: 50%; top: 100px; opacity: 0; } }

        /* --- MCQ SECTION --- */
        .quiz-container { display: none; }
        .quiz-container.active { display: block; }
        .question-box { background: white; padding: 25px; border-radius: 10px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); text-align: left; }
        .option-btn {
            display: block; width: 100%; padding: 15px; margin: 10px 0;
            background: #f8f9fa; border: 2px solid #eee; border-radius: 8px;
            cursor: pointer; text-align: left; transition: 0.2s; font-size: 1rem;
        }
        .option-btn:hover { background: #e3f2fd; border-color: var(--primary); }
        .correct { background: #d4edda !important; border-color: #28a745 !important; color: #155724; }
        .wrong { background: #f8d7da !important; border-color: #dc3545 !important; color: #721c24; }

        .hidden { display: none; }
    </style>
</head>
<body>

<div class="watermark">Designed by Anmol Singh</div>

<header>
    <h1>Class 12 Physics Master</h1>
    <p>Visual Learning & 50 Most Important MCQs</p>
</header>

<nav>
    <button onclick="showSection('theory')" class="active" id="btn-theory">📖 Visual Theory</button>
    <button onclick="showSection('quiz')" id="btn-quiz">📝 Physics MCQ (50)</button>
</nav>

<div id="theory" class="container">

    <h2 class="unit-header">1. Electrostatics & Potential</h2>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Electric Field due to Dipole (Axial) <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                Imagine a "Tug of War". You (Point P) are standing closer to a Strong Bodybuilder (+q) and further away from a Weak Child (-q). The Bodybuilder pushes you away hard. The Child pulls you weakly. The net result? You get pushed away.
            </div>
            
            <div class="anim-stage">
                <div class="charge plus">+q</div>
                <div class="charge minus">-q</div>
                <div class="field-arrow"></div>
                <div style="position: absolute; bottom: 10px; width: 100%; text-align: center; color: #aaa;">Electric Field Direction</div>
            </div>

            <div class="derivation">
1. E_net = E(+q) - E(-q)
2. E = k*q/(r-a)² - k*q/(r+a)²
3. Solve: E = k*q * [4ar / (r²-a²)²]
4. If r >> a (short dipole):
   FINAL: E = 2kp / r³
            </div>
        </div>
    </div>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Capacitance of Parallel Plate <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                Think of a capacitor as a sandwich. Two bread slices (Metal Plates) with cheese (Dielectric) in between. The bigger the bread (Area A), the more you can eat (Charge). The closer the slices (distance d), the stronger the flavor (Field).
            </div>
            
            <div class="anim-stage">
                <div class="plate plate-left"></div>
                <div class="plate plate-right"></div>
                <div class="field-lines"></div>
                <div style="position: absolute; bottom: 10px; width: 100%; text-align: center; color: #aaa;">Energy stored in Field</div>
            </div>

            <div class="derivation">
1. Electric Field E = σ/ε₀ = Q / (Aε₀)
2. Potential V = E * d
3. V = (Qd) / (Aε₀)
4. Capacitance C = Q / V
   FINAL: C = ε₀A / d
            </div>
        </div>
    </div>

    <h2 class="unit-header">2. Current Electricity</h2>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Drift Velocity <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                Imagine running through a crowded market. You want to run fast, but you keep bumping into people (atoms). You zig-zag and stumble. Your average speed moving forward is very slow. That slow speed is **Drift Velocity**.
            </div>

            <div class="anim-stage">
                <div class="wire-tube">
                    <div class="electron" style="animation-delay: 0s;"></div>
                    <div class="electron" style="animation-delay: 1s;"></div>
                    <div class="electron" style="animation-delay: 2s;"></div>
                </div>
            </div>

            <div class="derivation">
1. Force F = eE. Acceleration a = F/m = eE/m
2. Velocity = acceleration * time (relaxation time τ)
3. v_d = (eE/m) * τ
   CURRENT FORMULA: I = n A e v_d
            </div>
        </div>
    </div>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Wheatstone Bridge Principle <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                Imagine two water pipes running parallel. If the pressure at the middle of both pipes is exactly the same, no water will flow between them if you connect a cross-pipe. This is the **Balanced State** (Ig = 0).
            </div>
            <div class="derivation">
Condition for Balance:
Ratio of arms must be equal.
P / Q = R / S
            </div>
        </div>
    </div>

    <h2 class="unit-header">3. Magnetism</h2>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Force Between Parallel Currents <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                "Like currents attract, Unlike currents repel."
                If two wires carry current in the same direction, they act like friends and pull together. If opposite, they push apart.
            </div>
            <div class="derivation">
1. B field by wire 1: B = μ₀I₁ / 2πd
2. Force on wire 2: F = I₂LB
3. Force per unit length (f) = F/L
   FINAL: f = (μ₀ I₁ I₂) / (2πd)
            </div>
        </div>
    </div>

    <h2 class="unit-header">4. Optics (High Weightage)</h2>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Refraction through Prism <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                Light is lazy. When it enters glass (dense), it slows down and bends towards the normal. When it exits to air, it speeds up and bends away. The prism shape forces it to bend twice, creating deviation.
            </div>

            <div class="anim-stage">
                <div class="prism-tri"></div>
                <div class="light-ray"></div>
                <div class="refracted-ray"></div>
                <div class="emergent-ray"></div>
            </div>

            <div class="derivation">
Prism Formula:
n = sin((A + δm)/2) / sin(A/2)
(Where A is prism angle, δm is min deviation)
            </div>
        </div>
    </div>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Young's Double Slit Exp (YDSE) <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                Throw two stones in a calm pond. The ripples will cross each other.
                Crest + Crest = Big Wave (Bright Light).
                Crest + Trough = Flat Water (Darkness).
            </div>

            <div class="anim-stage">
                <div class="slit-wall"></div>
                <div class="slit-hole s1"></div>
                <div class="slit-hole s2"></div>
                <div class="ripple" style="left: 20%; top: 60px;"></div>
                <div class="ripple" style="left: 20%; top: 120px; animation-delay: 1.5s;"></div>
            </div>

            <div class="derivation">
Fringe Width (β):
β = λD / d
(Directly proportional to Wavelength λ and Distance D)
            </div>
        </div>
    </div>

    <h2 class="unit-header">5. Modern Physics</h2>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">Einstein's Photoelectric Effect <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                **The Vending Machine:** An electron is stuck inside a metal. To get it out, you need to pay a "fee" (Work Function). If you throw a coin (Photon) with value LESS than the fee, nothing happens. If you throw a coin with MORE value, the electron comes out and keeps the change as Speed (Kinetic Energy).
            </div>

            <div class="anim-stage">
                <div class="metal-surf"></div>
                <div class="photon-w" style="left: 40%"></div>
                <div class="photon-w" style="left: 50%; animation-delay: 0.5s"></div>
                <div class="e-eject" style="left: 40%; animation-delay: 1.2s"></div>
            </div>

            <div class="derivation">
Einstein's Equation:
Energy of Photon = Work Function + Kinetic Energy
hν = Φ₀ + K_max
            </div>
        </div>
    </div>

    <div class="card">
        <div class="card-header" onclick="toggle(this)">P-N Junction Diode <span>▼</span></div>
        <div class="card-body">
            <div class="simple-story">
                <span class="story-title">Simplest Explanation</span>
                **Forward Bias:** You push the Holes and Electrons towards each other. They meet, shake hands, and current flows easily.
                **Reverse Bias:** You pull them away from each other. The gap widens. No current flows.
            </div>

            <div class="anim-stage">
                <div class="p-side">P (Holes)</div>
                <div class="n-side">N (e-)</div>
                <div class="hole"></div>
                <div class="electron-dot"></div>
                <div style="position: absolute; bottom: 10px; width: 100%; text-align: center; color: #fff;">Forward Bias: Meeting in middle</div>
            </div>
        </div>
    </div>

</div>

<div id="quiz" class="container quiz-container">
    <div style="text-align: center; margin-bottom: 30px;">
        <h2 style="color: var(--primary);">Physics Challenge</h2>
        <p>Question: <span id="q-num">1</span> / 50</p>
        <p style="font-size: 1.5rem; font-weight: bold;">Score: <span id="score" style="color: var(--accent);">0</span></p>
    </div>

    <div id="quiz-box" class="question-box">
        </div>

    <div style="text-align: center; margin-top: 30px;">
        <button onclick="nextQuestion()" style="background: var(--primary); color: white; border: none; padding: 15px 40px; border-radius: 30px; font-size: 1.1rem; cursor: pointer; box-shadow: 0 4px 10px rgba(0,0,0,0.2);">Next Question ➜</button>
    </div>
</div>

<script>
    // --- UI LOGIC ---
    function showSection(id) {
        document.getElementById('theory').style.display = 'none';
        document.getElementById('quiz').classList.remove('active');
        document.getElementById('btn-theory').classList.remove('active');
        document.getElementById('btn-quiz').classList.remove('active');

        if(id === 'theory') {
            document.getElementById('theory').style.display = 'block';
            document.getElementById('btn-theory').classList.add('active');
        } else {
            document.getElementById('quiz').classList.add('active');
            document.getElementById('btn-quiz').classList.add('active');
        }
        window.scrollTo(0, 0);
    }

    function toggle(header) {
        let body = header.nextElementSibling;
        let span = header.querySelector('span');
        if (body.style.display === 'block') {
            body.style.display = 'none';
            span.innerText = '▼';
        } else {
            body.style.display = 'block';
            span.innerText = '▲';
        }
    }

    // --- 50 PURE PHYSICS QUESTIONS ---
    const questions = [
        { q: "SI Unit of Electric Flux?", opts: ["Weber", "Volt-meter", "Newton", "Joule"], a: 1 },
        { q: "Kirchhoff's First Law (Junction Rule) represents conservation of?", opts: ["Energy", "Charge", "Momentum", "Mass"], a: 1 },
        { q: "Kirchhoff's Second Law (Loop Rule) represents conservation of?", opts: ["Energy", "Charge", "Momentum", "Current"], a: 0 },
        { q: "Resistance of an Ideal Ammeter?", opts: ["Infinite", "Zero", "100 Ohm", "Very High"], a: 1 },
        { q: "Resistance of an Ideal Voltmeter?", opts: ["Infinite", "Zero", "Very Low", "1 Ohm"], a: 0 },
        { q: "Force on a charge moving parallel to magnetic field?", opts: ["qvB", "Zero", "Infinite", "qB/v"], a: 1 },
        { q: "1 Tesla is equal to?", opts: ["10^4 Gauss", "10^-4 Gauss", "10 Gauss", "100 Gauss"], a: 0 },
        { q: "Lens Maker's Formula relates focal length with?", opts: ["Radii of curvature & Refractive Index", "Image distance", "Object distance", "Height"], a: 0 },
        { q: "Blue color of sky is due to?", opts: ["Dispersion", "Scattering", "Refraction", "Interference"], a: 1 },
        { q: "Mirage is an example of?", opts: ["Total Internal Reflection", "Diffraction", "Polarization", "Scattering"], a: 0 },
        { q: "Power of a lens is measured in?", opts: ["Watt", "Diopter", "Meter", "Candela"], a: 1 },
        { q: "Condition for Constructive Interference?", opts: ["Path diff = nλ", "Path diff = (n+0.5)λ", "Phase diff = π", "None"], a: 0 },
        { q: "Energy of a Photon?", opts: ["E = mc^2", "E = hv", "E = 1/2 mv^2", "E = h/v"], a: 1 },
        { q: "Work Function is minimum for?", opts: ["Cesium", "Platinum", "Iron", "Copper"], a: 0 },
        { q: "Which series of Hydrogen Spectrum is in Visible region?", opts: ["Lyman", "Balmer", "Paschen", "Pfund"], a: 1 },
        { q: "1 amu is equivalent to energy?", opts: ["931 MeV", "1.6 J", "1 eV", "100 MeV"], a: 0 },
        { q: "Nuclear Force is?", opts: ["Long range", "Short range", "Infinite range", "Weak"], a: 1 },
        { q: "In P-type semiconductor, majority carriers are?", opts: ["Electrons", "Holes", "Protons", "Neutrons"], a: 1 },
        { q: "In N-type semiconductor, dopant valency is?", opts: ["Pentavalent (+5)", "Trivalent (+3)", "Divalent (+2)", "None"], a: 0 },
        { q: "Rectifier converts?", opts: ["AC to DC", "DC to AC", "Low V to High V", "None"], a: 0 },
        { q: "Unit of Capacitance?", opts: ["Farad", "Henry", "Weber", "Tesla"], a: 0 },
        { q: "Dielectric constant of metal?", opts: ["0", "1", "Infinite", "Negative"], a: 2 },
        { q: "Potentiometer is better than Voltmeter because?", opts: ["It draws no current", "It is cheap", "It is small", "It has low resistance"], a: 0 },
        { q: "Unit of Magnetic Flux?", opts: ["Tesla", "Weber", "Gauss", "Henry"], a: 1 },
        { q: "Transformer works on principle of?", opts: ["Mutual Induction", "Self Induction", "Eddy Current", "Resonance"], a: 0 },
        { q: "Step-up transformer increases?", opts: ["Power", "Frequency", "Voltage", "Current"], a: 2 },
        { q: "Speed of EM waves in vacuum?", opts: ["3x10^8 m/s", "330 m/s", "Infinite", "Zero"], a: 0 },
        { q: "Which wave has highest frequency?", opts: ["Radio", "Microwave", "X-Rays", "Gamma Rays"], a: 3 },
        { q: "Focal length of plane mirror?", opts: ["Zero", "Infinite", "10 cm", "-10 cm"], a: 1 },
        { q: "Air bubble in water behaves as?", opts: ["Convex Lens", "Concave Lens", "Glass Slab", "Mirror"], a: 1 },
        { q: "Ratio of speed of light in vacuum to medium?", opts: ["Refractive Index", "Frequency", "Wavelength", "Amplitude"], a: 0 },
        { q: "Diffraction of light shows?", opts: ["Particle nature", "Wave nature", "Both", "None"], a: 1 },
        { q: "Momentum of photon?", opts: ["h/λ", "hλ", "Zero", "mc"], a: 0 },
        { q: "Bohr model is applicable for?", opts: ["Hydrogen-like atoms", "Multi-electron atoms", "Molecules", "Solids"], a: 0 },
        { q: "Isotopes have same?", opts: ["Mass Number", "Atomic Number", "Neutrons", "None"], a: 1 },
        { q: "Solar energy is due to?", opts: ["Fission", "Fusion", "Burning", "Chemical Rxn"], a: 1 },
        { q: "Depletion layer in PN diode contains?", opts: ["Electrons", "Holes", "Immobile Ions", "Mobile Ions"], a: 2 },
        { q: "Logic Gate performing inversion?", opts: ["AND", "OR", "NOT", "NAND"], a: 2 },
        { q: "Unit of Self Inductance?", opts: ["Henry", "Farad", "Weber", "Tesla"], a: 0 },
        { q: "Eddy currents are produced in?", opts: ["Insulators", "Conductors", "Gases", "Vacuum"], a: 1 },
        { q: "Angle of dip at poles?", opts: ["0", "45", "90", "180"], a: 2 },
        { q: "Relation between E and V?", opts: ["E = -dV/dr", "E = V/r", "V = E/r", "None"], a: 0 },
        { q: "Torque on dipole?", opts: ["pE sinθ", "pE cosθ", "p.E", "Zero"], a: 0 },
        { q: "Specific resistance depends on?", opts: ["Length", "Area", "Material", "Current"], a: 2 },
        { q: "Magnetic field inside solenoid is?", opts: ["Uniform", "Non-uniform", "Zero", "Infinite"], a: 0 },
        { q: "Core of transformer is laminated to reduce?", opts: ["Copper loss", "Eddy current loss", "Hysteresis", "Flux leak"], a: 1 },
        { q: "Sound waves are?", opts: ["Transverse", "Longitudinal", "EM waves", "None"], a: 1 },
        { q: "Light waves are?", opts: ["Transverse", "Longitudinal", "Mechanical", "None"], a: 0 },
        { q: "Charge on Alpha particle?", opts: ["+e", "+2e", "-e", "Zero"], a: 1 },
        { q: "Device to convert Light to Current?", opts: ["LED", "Photodiode", "Solar Cell", "Zener"], a: 1 }
    ];

    let currentQ = 0;
    let score = 0;
    let answered = false;

    function loadQuestion() {
        answered = false;
        const data = questions[currentQ];
        let html = `<h3 style="margin-bottom:20px;">Q${currentQ+1}: ${data.q}</h3>`;
        
        data.opts.forEach((opt, index) => {
            html += `<button class="option-btn" onclick="checkAnswer(${index}, this)">${opt}</button>`;
        });

        document.getElementById('quiz-box').innerHTML = html;
        document.getElementById('q-num').innerText = currentQ + 1;
    }

    function checkAnswer(selectedIndex, btn) {
        if(answered) return;
        answered = true;
        
        const correctIndex = questions[currentQ].a;
        const allBtns = document.querySelectorAll('.option-btn');

        if(selectedIndex === correctIndex) {
            btn.classList.add('correct');
            score++;
            document.getElementById('score').innerText = score;
        } else {
            btn.classList.add('wrong');
            allBtns[correctIndex].classList.add('correct');
        }
    }

    function nextQuestion() {
        if(currentQ < questions.length - 1) {
            currentQ++;
            loadQuestion();
        } else {
            document.getElementById('quiz-box').innerHTML = `
                <div style="text-align:center; padding:40px;">
                    <h2 style="color:var(--primary)">Exam Complete!</h2>
                    <h1 style="font-size:3rem; color:var(--accent)">${score} / 50</h1>
                    <p>${score > 40 ? "Outstanding! You are ready for the Board Exam." : "Good effort! Revise the weak topics."}</p>
                    <button onclick="location.reload()" style="margin-top:20px; padding:10px 20px; cursor:pointer;">Restart</button>
                </div>
            `;
            document.querySelector('button[onclick="nextQuestion()"]').style.display = 'none';
        }
    }

    // Init
    loadQuestion();

</script>

</body>
</html>
