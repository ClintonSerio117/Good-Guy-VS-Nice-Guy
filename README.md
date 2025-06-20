<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Good Guy Code - Fire Ceremony System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0a0a0a;
            color: #ffffff;
            overflow-x: hidden;
            position: relative;
        }

        /* Fire particle background */
        .fire-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: radial-gradient(circle at 50% 100%, rgba(255, 69, 0, 0.1) 0%, transparent 50%);
            pointer-events: none;
            z-index: -1;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            background: linear-gradient(135deg, #1a1a1a 0%, #2d1810 100%);
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><radialGradient id="fire" cx="50%" cy="50%"><stop offset="0%" stop-color="%23ff4500" stop-opacity="0.3"/><stop offset="100%" stop-color="transparent"/></radialGradient></defs><circle cx="50" cy="50" r="30" fill="url(%23fire)"/></svg>');
            animation: fireFlicker 3s infinite ease-in-out;
            opacity: 0.5;
        }

        @keyframes fireFlicker {
            0%, 100% { transform: scale(1) rotate(0deg); opacity: 0.3; }
            50% { transform: scale(1.1) rotate(5deg); opacity: 0.6; }
        }

        .hero-content h1 {
            font-size: clamp(2.5rem, 8vw, 6rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            background: linear-gradient(45deg, #ff6b35, #f7931e, #ff4500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 1rem;
            text-shadow: 0 0 30px rgba(255, 69, 0, 0.5);
        }

        .hero-tagline {
            font-size: clamp(1.2rem, 3vw, 2rem);
            margin-bottom: 2rem;
            font-style: italic;
            color: #cccccc;
        }

        .hero-subtitle {
            font-size: clamp(1rem, 2.5vw, 1.5rem);
            margin-bottom: 3rem;
            color: #888;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        /* Fire Button */
        .fire-btn {
            display: inline-block;
            padding: 20px 40px;
            background: linear-gradient(45deg, #ff4500, #ff6b35);
            border: none;
            border-radius: 50px;
            color: white;
            font-size: 1.2rem;
            font-weight: bold;
            text-decoration: none;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transform: perspective(1000px) translateZ(0);
            transition: all 0.3s ease;
            box-shadow: 
                0 10px 30px rgba(255, 69, 0, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
        }

        .fire-btn:hover {
            transform: perspective(1000px) translateZ(10px) translateY(-5px);
            box-shadow: 
                0 20px 40px rgba(255, 69, 0, 0.4),
                inset 0 1px 0 rgba(255, 255, 255, 0.3);
        }

        .fire-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .fire-btn:hover::before {
            left: 100%;
        }

        /* Ceremony Sections */
        .ceremony {
            min-height: 100vh;
            padding: 100px 0;
            position: relative;
            border-bottom: 1px solid rgba(255, 69, 0, 0.2);
        }

        .ceremony-header {
            text-align: center;
            margin-bottom: 80px;
        }

        .ceremony-number {
            font-size: 1.2rem;
            color: #ff6b35;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 0.2em;
            margin-bottom: 1rem;
        }

        .ceremony-title {
            font-size: clamp(2rem, 5vw, 4rem);
            font-weight: 900;
            margin-bottom: 1rem;
            background: linear-gradient(45deg, #ffffff, #cccccc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .ceremony-tagline {
            font-size: clamp(1rem, 2.5vw, 1.5rem);
            color: #ff6b35;
            font-style: italic;
            font-weight: bold;
        }

        /* 3D Cards */
        .ceremony-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
            margin-top: 60px;
        }

        .ceremony-card {
            background: linear-gradient(145deg, #1a1a1a, #2a2a2a);
            border-radius: 20px;
            padding: 40px;
            position: relative;
            transform: perspective(1000px) rotateX(0deg) rotateY(0deg);
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 69, 0, 0.2);
            box-shadow: 
                0 10px 30px rgba(0, 0, 0, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.1);
        }

        .ceremony-card:hover {
            transform: perspective(1000px) rotateX(5deg) rotateY(5deg) translateZ(20px);
            box-shadow: 
                0 20px 40px rgba(0, 0, 0, 0.4),
                0 0 20px rgba(255, 69, 0, 0.2),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
        }

        .card-icon {
            width: 80px;
            height: 80px;
            background: linear-gradient(45deg, #ff4500, #ff6b35);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 30px;
            font-size: 2rem;
            box-shadow: 0 10px 20px rgba(255, 69, 0, 0.3);
        }

        .card-title {
            font-size: 1.5rem;
            font-weight: bold;
            text-align: center;
            margin-bottom: 20px;
            color: #ffffff;
        }

        .card-description {
            color: #cccccc;
            line-height: 1.6;
            text-align: center;
            margin-bottom: 30px;
        }

        /* Lock/Unlock States */
        .ceremony.locked {
            opacity: 0.5;
            pointer-events: none;
        }

        .ceremony.locked .ceremony-card {
            background: linear-gradient(145deg, #0f0f0f, #1a1a1a);
            border-color: rgba(255, 255, 255, 0.1);
        }

        .lock-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 20px;
            backdrop-filter: blur(5px);
        }

        .lock-icon {
            font-size: 3rem;
            color: #666;
        }

        /* Unlock Button */
        .unlock-btn {
            background: linear-gradient(45deg, #ff4500, #ff6b35);
            border: none;
            border-radius: 15px;
            color: white;
            padding: 15px 30px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            transition: all 0.3s ease;
            width: 100%;
            transform: perspective(1000px) translateZ(0);
        }

        .unlock-btn:hover {
            transform: perspective(1000px) translateZ(5px);
            box-shadow: 0 10px 20px rgba(255, 69, 0, 0.3);
        }

        /* WhatsApp Integration */
        .whatsapp-prompt {
            background: linear-gradient(45deg, #25d366, #128c7e);
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            margin: 40px 0;
            transform: perspective(1000px) translateZ(0);
            transition: all 0.3s ease;
        }

        .whatsapp-prompt:hover {
            transform: perspective(1000px) translateZ(10px);
        }

        .whatsapp-btn {
            background: #ffffff;
            color: #25d366;
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-weight: bold;
            cursor: pointer;
            text-decoration: none;
            display: inline-block;
            margin-top: 15px;
            transition: all 0.3s ease;
        }

        .whatsapp-btn:hover {
            background: #f0f0f0;
            transform: scale(1.05);
        }

        /* Progress Bar */
        .progress-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: rgba(255, 255, 255, 0.1);
            z-index: 1000;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #ff4500, #ff6b35);
            width: 0%;
            transition: width 0.3s ease;
            box-shadow: 0 0 10px rgba(255, 69, 0, 0.5);
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .ceremony-grid {
                grid-template-columns: 1fr;
            }
            
            .ceremony {
                padding: 60px 0;
            }
            
            .ceremony-card {
                padding: 30px;
            }
        }

        /* Floating Elements */
        .floating-ember {
            position: fixed;
            width: 4px;
            height: 4px;
            background: #ff6b35;
            border-radius: 50%;
            pointer-events: none;
            z-index: -1;
            animation: float 8s infinite linear;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) translateX(0px) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) translateX(100px) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="fire-bg"></div>
    <div class="progress-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <div class="hero-content">
                <h1>The Good Guy Code</h1>
                <p class="hero-tagline">"Being liked is survival. Being true is resurrection."</p>
                <p class="hero-subtitle">Transform from people-pleasing nice guy to authentic good guy through 5 sacred fire ceremonies</p>
                <a href="#ceremony1" class="fire-btn">🔥 Begin The Fire Ceremonies</a>
            </div>
        </div>
    </section>

    <!-- Ceremony 1: The Mirror Breaks -->
    <section class="ceremony" id="ceremony1">
        <div class="container">
            <div class="ceremony-header">
                <div class="ceremony-number">Ceremony 1</div>
                <h2 class="ceremony-title">The Mirror Breaks</h2>
                <p class="ceremony-tagline">"The nice guy isn't kind. He's terrified."</p>
            </div>
            
            <div class="ceremony-grid">
                <div class="ceremony-card">
                    <div class="card-icon">🪞</div>
                    <h3 class="card-title">The Forced Smile</h3>
                    <p class="card-description">Recognize the performance you've been living. See the mask you wear to survive.</p>
                    <button class="unlock-btn" onclick="unlockCeremony(1)">🔥 Shatter The Mirror</button>
                </div>
                
                <div class="ceremony-card">
                    <div class="card-icon">💔</div>
                    <h3 class="card-title">The Root Scene</h3>
                    <p class="card-description">Discover the moment you learned to smile for survival instead of truth.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="card-icon">🕯️</div>
                    <h3 class="card-title">The Candle Ritual</h3>
                    <p class="card-description">Honor the boy who survived, awaken the man who will thrive.</p>
                </div>
            </div>
            
            <div class="whatsapp-prompt" id="whatsapp1" style="display: none;">
                <h3>🔥 Ready for Your First Fire Key?</h3>
                <p>Complete your ritual and receive your sacred fire image to unlock Ceremony 2</p>
                <a href="#" class="whatsapp-btn" onclick="sendFireKey(1)">📱 Send Me The Fire Key</a>
            </div>
        </div>
    </section>

    <!-- Ceremony 2: The Father Wound -->
    <section class="ceremony locked" id="ceremony2">
        <div class="container">
            <div class="ceremony-header">
                <div class="ceremony-number">Ceremony 2</div>
                <h2 class="ceremony-title">The Father Wound Exposed</h2>
                <p class="ceremony-tagline">"You're not fixing yourself. You're freeing yourself from his fear."</p>
            </div>
            
            <div class="ceremony-grid">
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">👨</div>
                    <h3 class="card-title">Inherited Patterns</h3>
                    <p class="card-description">Unpack the fear and shame passed down through generations.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">⛪</div>
                    <h3 class="card-title">Religious Programming</h3>
                    <p class="card-description">Separate authentic spirituality from toxic religious conditioning.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🔥</div>
                    <h3 class="card-title">Reclaim Your Fire</h3>
                    <p class="card-description">Burn the inherited shame and reclaim your masculine essence.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Ceremony 3: Identity Excavation -->
    <section class="ceremony locked" id="ceremony3">
        <div class="container">
            <div class="ceremony-header">
                <div class="ceremony-number">Ceremony 3</div>
                <h2 class="ceremony-title">The Identity Excavation</h2>
                <p class="ceremony-tagline">"If you weren't trying to be liked... who would you be?"</p>
            </div>
            
            <div class="ceremony-grid">
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🏛️</div>
                    <h3 class="card-title">The Stranger in the Mirror</h3>
                    <p class="card-description">Meet the authentic self beneath the performance identity.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🎭</div>
                    <h3 class="card-title">Burn the Performance</h3>
                    <p class="card-description">Release the identity built on others' expectations.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">💎</div>
                    <h3 class="card-title">Excavate Your Essence</h3>
                    <p class="card-description">Discover what you actually want vs. what you think you should want.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Ceremony 4: The Boundary Forge -->
    <section class="ceremony locked" id="ceremony4">
        <div class="container">
            <div class="ceremony-header">
                <div class="ceremony-number">Ceremony 4</div>
                <h2 class="ceremony-title">The Boundary Forge</h2>
                <p class="ceremony-tagline">"You're not a jerk. You're a lighthouse. Let them crash if they can't steer."</p>
            </div>
            
            <div class="ceremony-grid">
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🚫</div>
                    <h3 class="card-title">The Sacred NO</h3>
                    <p class="card-description">Learn the art of setting boundaries without destruction.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🛡️</div>
                    <h3 class="card-title">The 3-Style Blueprint</h3>
                    <p class="card-description">When to speak, when to walk, when to war.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">⚔️</div>
                    <h3 class="card-title">Forge Unshakeable Standards</h3>
                    <p class="card-description">Create intimacy through boundaries, not distance.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Ceremony 5: The Good Guy Rises -->
    <section class="ceremony locked" id="ceremony5">
        <div class="container">
            <div class="ceremony-header">
                <div class="ceremony-number">Ceremony 5</div>
                <h2 class="ceremony-title">The Good Guy Rises</h2>
                <p class="ceremony-tagline">"Kind, clear, and unfuckwithable."</p>
            </div>
            
            <div class="ceremony-grid">
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🌅</div>
                    <h3 class="card-title">The Real Smile</h3>
                    <p class="card-description">From survival performance to authentic presence.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🏰</div>
                    <h3 class="card-title">Integration Without Compromise</h3>
                    <p class="card-description">Still kind, never weak. Still gentle, never gutless.</p>
                </div>
                
                <div class="ceremony-card">
                    <div class="lock-overlay">
                        <div class="lock-icon">🔒</div>
                    </div>
                    <div class="card-icon">🏆</div>
                    <h3 class="card-title">Command Respect</h3>
                    <p class="card-description">Become respectable, automatically command respect.</p>
                </div>
            </div>
        </div>
    </section>

    <script>
        // Progress tracking
        let currentCeremony = 1;
        const totalCeremonies = 5;

        function updateProgress() {
            const progress = (currentCeremony / totalCeremonies) * 100;
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function unlockCeremony(ceremonyNumber) {
            // Show WhatsApp prompt for current ceremony
            document.getElementById('whatsapp' + ceremonyNumber).style.display = 'block';
            
            // Simulate ceremony completion animation
            const button = event.target;
            button.innerHTML = '✅ Ceremony Complete';
            button.style.background = 'linear-gradient(45deg, #28a745, #20c997)';
            
            setTimeout(() => {
                // Unlock next ceremony
                if (ceremonyNumber < totalCeremonies) {
                    const nextCeremony = document.getElementById('ceremony' + (ceremonyNumber + 1));
                    nextCeremony.classList.remove('locked');
                    currentCeremony = ceremonyNumber + 1;
                    updateProgress();
                }
            }, 2000);
        }

        function sendFireKey(ceremonyNumber) {
            // Simulate WhatsApp integration
            alert(`🔥 Fire Key for Ceremony ${ceremonyNumber + 1} has been sent to your WhatsApp!\n\nCheck your messages for your sacred fire image and unlock code.`);
            
            // In real implementation, this would trigger WhatsApp API
            // For now, we'll auto-unlock the next ceremony after a delay
            setTimeout(() => {
                if (ceremonyNumber < totalCeremonies) {
                    const nextCeremony = document.getElementById('ceremony' + (ceremonyNumber + 1));
                    nextCeremony.classList.remove('locked');
                    currentCeremony = ceremonyNumber + 1;
                    updateProgress();
                    
                    // Scroll to next ceremony
                    nextCeremony.scrollIntoView({ behavior: 'smooth' });
                }
            }, 3000);
        }

        // Floating embers animation
        function createEmber() {
            const ember = document.createElement('div');
            ember.className = 'floating-ember';
            ember.style.left = Math.random() * 100 + '%';
            ember.style.animationDelay = Math.random() * 8 + 's';
            ember.style.animationDuration = (Math.random() * 3 + 5) + 's';
            document.body.appendChild(ember);
            
            setTimeout(() => {
                ember.remove();
            }, 8000);
        }

        // Create embers periodically
        setInterval(createEmber, 2000);

        // Initialize progress
        updateProgress();

        // Smooth scrolling for fire button
        document.querySelector('.fire-btn').addEventListener('click', function(e) {
            e.preventDefault();
            document.querySelector('#ceremony1').scrollIntoView({ 
                behavior: 'smooth' 
            });
        });

        // Add scroll-triggered animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        // Observe all ceremony cards
        document.querySelectorAll('.ceremony-card').forEach(card => {
            card.style.opacity = '0';
            card.style.transform = 'translateY(50px)';
            card.style.transition = 'all 0.6s ease';
            observer.observe(card);
        });
    </script>
</body>
</html>
