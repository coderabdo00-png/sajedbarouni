<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sajad Barmasi - Video Editor</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: #0a0a0f;
            color: #ffffff;
            overflow-x: hidden;
            cursor: none;
        }

        .nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            padding: 1.5rem 4rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            background: rgba(10, 10, 15, 0.8);
            backdrop-filter: blur(10px);
        }

        .logo {
            font-size: 1.2rem;
            font-weight: 600;
            color: #a855f7;
        }

        .nav-menu {
            display: flex;
            gap: 2.5rem;
            align-items: center;
            list-style: none;
        }

        .nav-menu a {
            color: #ffffff;
            text-decoration: none;
            font-size: 0.95rem;
            transition: color 0.3s ease;
        }

        .nav-menu a:hover {
            color: #a855f7;
        }

        .nav-btn {
            background: #a855f7;
            color: #ffffff;
            padding: 0.6rem 1.5rem;
            border-radius: 25px;
            text-decoration: none;
            font-size: 0.9rem;
            font-weight: 600;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .nav-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(168, 85, 247, 0.4);
            background: #9333ea;
        }

        /* Custom Cursor */
        .cursor {
            position: fixed;
            width: 12px;
            height: 12px;
            background: #a855f7;
            border-radius: 50%;
            pointer-events: none;
            z-index: 10000;
            transition: transform 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            transform: translate(-50%, -50%);
        }

        .cursor-follower {
            position: fixed;
            width: 40px;
            height: 40px;
            border: 2px solid #a855f7;
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1), height 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            transform: translate(-50%, -50%);
            opacity: 0.6;
        }

        .cursor-follower.clicking {
            width: 60px;
            height: 60px;
            animation: clickPulse 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        @keyframes clickPulse {
            0% {
                width: 40px;
                height: 40px;
                opacity: 0.6;
            }
            50% {
                width: 70px;
                height: 70px;
                opacity: 0.3;
                border-width: 3px;
            }
            100% {
                width: 40px;
                height: 40px;
                opacity: 0.6;
            }
        }

        a, button {
            cursor: none;
        }

        .hero {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 8rem 2rem 4rem;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, rgba(168, 85, 247, 0.15) 0%, transparent 70%);
            border-radius: 50%;
            filter: blur(80px);
            animation: pulse 8s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: translate(-50%, -50%) scale(1); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
        }

        .hero-tag {
            color: #9ca3af;
            font-size: 0.9rem;
            margin-bottom: 1rem;
            letter-spacing: 0.5px;
        }

        .hero h1 {
            font-size: 4rem;
            font-weight: 800;
            line-height: 1.2;
            margin-bottom: 2rem;
            position: relative;
            z-index: 1;
        }

        .hero h1 .gradient-text {
            background: linear-gradient(135deg, #a855f7 0%, #9333ea 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero h1 .italic-text {
            font-style: italic;
            font-weight: 300;
        }

        .hero-buttons {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            position: relative;
            z-index: 1;
        }

        .btn {
            padding: 0.9rem 2rem;
            border-radius: 30px;
            font-size: 1rem;
            font-weight: 600;
            text-decoration: none;
            transition: all 0.3s ease;
            border: none;
            cursor: pointer;
        }

        .btn-primary {
            background: #a855f7;
            color: #ffffff;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(168, 85, 247, 0.4);
        }

        .btn-secondary {
            background: #ffffff;
            color: #0a0a0f;
        }

        .btn-secondary:hover {
            background: #f3f4f6;
            transform: translateY(-3px);
        }

        .phone-mockup {
            width: 280px;
            height: 560px;
            background: linear-gradient(135deg, #1e1b4b 0%, #7c3aed 50%, #a855f7 100%);
            border-radius: 40px;
            padding: 12px;
            box-shadow: 0 25px 60px rgba(168, 85, 247, 0.4);
            position: relative;
            z-index: 1;
        }

        .phone-screen {
            width: 100%;
            height: 100%;
            background: #1e1b4b;
            border-radius: 32px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .phone-notch {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 120px;
            height: 25px;
            background: #0a0a0f;
            border-radius: 0 0 20px 20px;
        }

        .play-icon {
            width: 60px;
            height: 60px;
            background: rgba(168, 85, 247, 0.3);
            border: 2px solid #a855f7;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: none;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .play-icon:hover {
            background: rgba(168, 85, 247, 0.5);
            transform: scale(1.15);
            box-shadow: 0 10px 30px rgba(168, 85, 247, 0.5);
        }

        .play-icon::after {
            content: '';
            width: 0;
            height: 0;
            border-left: 15px solid #a855f7;
            border-top: 10px solid transparent;
            border-bottom: 10px solid transparent;
            margin-left: 4px;
        }

        .section {
            padding: 6rem 2rem;
            position: relative;
        }

        .section-tag {
            text-align: center;
            color: #a855f7;
            font-size: 0.85rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 1rem;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 1rem;
        }

        .section-subtitle {
            text-align: center;
            color: #9ca3af;
            font-size: 1.1rem;
            margin-bottom: 4rem;
        }

        .content-section {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
        }

        .content-text h3 {
            font-size: 2rem;
            margin-bottom: 1.5rem;
        }

        .content-text h4 {
            color: #a855f7;
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 1rem;
        }

        .content-text p {
            color: #9ca3af;
            line-height: 1.8;
            margin-bottom: 1rem;
        }

        .features-grid {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .feature-card {
            background: rgba(168, 85, 247, 0.05);
            border: 1px solid rgba(168, 85, 247, 0.2);
            border-radius: 20px;
            padding: 2.5rem;
            transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .feature-card:hover {
            background: rgba(168, 85, 247, 0.1);
            border-color: rgba(168, 85, 247, 0.5);
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 20px 40px rgba(168, 85, 247, 0.3);
        }

        .feature-icon {
            width: 50px;
            height: 50px;
            background: #a855f7;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 1.5rem;
            font-size: 1.5rem;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .feature-card:hover .feature-icon {
            transform: scale(1.1) rotate(5deg);
            box-shadow: 0 10px 25px rgba(168, 85, 247, 0.4);
        }

        .feature-card h3 {
            font-size: 1.3rem;
            margin-bottom: 1rem;
        }

        .feature-card p {
            color: #9ca3af;
            line-height: 1.6;
        }

        .benefits-grid {
            max-width: 900px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 3rem;
        }

        .benefit-item {
            text-align: center;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .benefit-item:hover {
            transform: translateY(-8px);
        }

        .benefit-icon {
            width: 70px;
            height: 70px;
            background: #a855f7;
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1.5rem;
            font-size: 2rem;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .benefit-item:hover .benefit-icon {
            transform: scale(1.15) rotate(-5deg);
            box-shadow: 0 15px 35px rgba(168, 85, 247, 0.5);
        }

        .benefit-item p {
            color: #9ca3af;
            line-height: 1.6;
        }

        .pricing-section {
            max-width: 500px;
            margin: 0 auto;
        }

        .pricing-card {
            background: linear-gradient(135deg, rgba(168, 85, 247, 0.2) 0%, rgba(147, 51, 234, 0.2) 100%);
            border-radius: 25px;
            padding: 3rem;
            position: relative;
            overflow: hidden;
        }

        .pricing-header {
            margin-bottom: 2rem;
        }

        .pricing-title {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
        }

        .pricing-subtitle {
            color: #9ca3af;
            font-size: 0.9rem;
        }

        .pricing-price {
            font-size: 3.5rem;
            font-weight: 700;
            margin-bottom: 2rem;
        }

        .pricing-details {
            background: rgba(168, 85, 247, 0.1);
            border-radius: 15px;
            padding: 1.5rem;
            margin-bottom: 2rem;
        }

        .pricing-details p {
            color: #9ca3af;
            font-size: 0.9rem;
            margin-bottom: 0.5rem;
        }

        .pricing-features {
            list-style: none;
            margin-bottom: 2rem;
        }

        .pricing-features li {
            padding: 0.8rem 0;
            border-bottom: 1px solid rgba(168, 85, 247, 0.2);
            color: #9ca3af;
        }

        .pricing-features li:last-child {
            border-bottom: none;
        }

        .pricing-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
        }

        .footer {
            text-align: center;
            padding: 3rem 2rem;
            border-top: 1px solid rgba(168, 85, 247, 0.2);
            margin-top: 4rem;
        }

        .footer p {
            color: #9ca3af;
            font-size: 0.9rem;
            margin-bottom: 0.5rem;
        }

        @media (max-width: 768px) {
            .nav {
                padding: 1rem 1.5rem;
            }

            .nav-menu {
                gap: 1.5rem;
            }

            .hero h1 {
                font-size: 2.5rem;
            }

            .content-section {
                grid-template-columns: 1fr;
            }

            .section-title {
                font-size: 2rem;
            }

            .pricing-buttons {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="cursor"></div>
    <div class="cursor-follower"></div>
    
    <nav class="nav">
        <div class="logo">Sajad Barmasi</div>
        <ul class="nav-menu">
            <li><a href="#home">Home</a></li>
            <li><a href="#process">Process</a></li>
            <li><a href="#benefits">Benefits</a></li>
            <li><a href="#pricing">Pricing</a></li>
            <li><a href="https://calendly.com/sajedbarouni/30min?month=2025-10" target="_blank" class="nav-btn">Book a call</a></li>
        </ul>
    </nav>

    <section class="hero">
        <p class="hero-tag">Say goodbye to flashy content that gets likes.</p>
        <p class="hero-tag">Hello to quiet systems that book calls.</p>
        <h1>
            I turn your raw footage<br>
            into a <span class="gradient-text">client-acquisition</span><br>
            <span class="italic-text">engine.</span>
        </h1>
        <div class="hero-buttons">
            <a href="https://calendly.com/sajedbarouni/30min?month=2025-10" target="_blank" class="btn btn-primary">Book a call</a>
            <a href="#" class="btn btn-secondary">See my work</a>
        </div>
    </section>

    <section class="section">
        <div class="content-section">
            <div class="content-text">
                <h4>THE PROBLEM</h4>
                <h3>Content chaos is costing you clients</h3>
                <p><strong>One release: Predictable growth</strong></p>
                <p>A proper release strategy.</p>
                <p>I edit clearly, attention and results.</p>
                <p>Your post back-to-business for $20k</p>
                <p>My focus is impact, not efforts.</p>
            </div>
            <div class="phone-mockup" style="margin: 0 auto;">
                <div class="phone-screen">
                    <div class="phone-notch"></div>
                    <div class="play-icon"></div>
                </div>
            </div>
        </div>
    </section>

    <section class="section">
        <p class="section-tag">PROCESS</p>
        <h2 class="section-title">You record. I handle the rest.</h2>
        <p class="section-subtitle">Three-step system that turns raw footage into<br>lead magnets. High-converting content.</p>
        <a href="https://calendly.com/sajedbarouni/30min?month=2025-10" target="_blank" class="btn btn-primary" style="display: block; width: fit-content; margin: 0 auto 4rem;">Book a Demo</a>
        
        <div class="features-grid">
            <div class="feature-card">
                <div class="feature-icon">📤</div>
                <h3>Upload</h3>
                <p>Drop your raw footage through our simple portal.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">✂️</div>
                <h3>Strategic Repurpose</h3>
                <p>We plan, polish and repurpose for placements.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">🎯</div>
                <h3>Get Sales</h3>
                <p>Your old content ready to post to hit your goals.</p>
            </div>
        </div>
    </section>

    <section class="section">
        <p class="section-tag">BENEFITS</p>
        <h2 class="section-title">Fast, quality & Results.</h2>
        <p class="section-subtitle">High quality edits delivered quickly. Crafted to make an impact.</p>
        
        <div class="features-grid" style="margin-bottom: 4rem;">
            <div class="feature-card">
                <div class="feature-icon">♾️</div>
                <h3>Infinite Revisions</h3>
                <p>Submit as many videos as you'd like in batches & projects. Unlimited requests to get you on point in results fast for the results.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">🎯</div>
                <h3>Strategic Approach</h3>
                <p>Titles, hooks, and narrative flow strategically crafted.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">📅</div>
                <h3>Rapid Turnaround</h3>
                <p>Your short video with a short turnaround time and whenever you need it.</p>
            </div>
            <div class="feature-card">
                <div class="feature-icon">💬</div>
                <h3>Communication</h3>
                <p>No middlemen, no confusion. We're directly with you under orders.</p>
            </div>
        </div>
    </section>

    <section class="section">
        <p class="section-tag">VALUE</p>
        <h2 class="section-title">Why Work With Me?</h2>
        <p class="section-subtitle">Great guarantee with the types I work well for everyone else again. Basically.</p>
        
        <div class="benefits-grid">
            <div class="benefit-item">
                <div class="benefit-icon">💰</div>
                <p>Been on economic Commerce (Monthly Agreement)</p>
            </div>
            <div class="benefit-item">
                <div class="benefit-icon">⏱️</div>
                <p>Receive your edits (not a year or more) in about as brief a few hours</p>
            </div>
            <div class="benefit-item">
                <div class="benefit-icon">📈</div>
                <p>I show your audience or less with huge impact views</p>
            </div>
        </div>
        
        <a href="https://calendly.com/sajedbarouni/30min?month=2025-10" target="_blank" class="btn btn-primary" style="display: block; width: fit-content; margin: 3rem auto 0;">Book a Demo</a>
    </section>

    <section class="section" id="pricing">
        <p class="section-tag">PRICING</p>
        <h2 class="section-title">Clear pricing, no Surprises.</h2>
        <p class="section-subtitle">Only plan. Everything you need.</p>
        
        <div class="pricing-section">
            <div class="pricing-card">
                <div class="pricing-header">
                    <h3 class="pricing-title">High-Impact Package</h3>
                    <p class="pricing-subtitle">What you get, for $599/m:</p>
                </div>
                
                <div class="pricing-price">$599</div>
                
                <div class="pricing-details">
                    <p>What makes it so special:</p>
                </div>
                
                <ul class="pricing-features">
                    <li>✓ Unlimited video editing requests</li>
                    <li>✓ Average 24h turnaround time</li>
                    <li>✓ Unlimited brands & clients</li>
                    <li>✓ Unlimited revisions</li>
                    <li>✓ Unlimited stock footage</li>
                    <li>✓ Easy credit-card payments</li>
                    <li>✓ Pause or cancel anytime</li>
                </ul>
                
                <div class="pricing-buttons">
                    <a href="#" class="btn btn-primary">See pricing</a>
                    <a href="https://calendly.com/sajedbarouni/30min?month=2025-10" target="_blank" class="btn btn-secondary">Book a call</a>
                </div>
            </div>
        </div>
    </section>

    <footer class="footer">
        <p>© 2024 Sajad Barmasi - All rights reserved.</p>
        <p>Turning raw footage into client conversion machines</p>
    </footer>

    <script>
        // Custom Cursor
        const cursor = document.querySelector('.cursor');
        const cursorFollower = document.querySelector('.cursor-follower');

        let mouseX = 0;
        let mouseY = 0;
        let followerX = 0;
        let followerY = 0;

        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
            
            cursor.style.left = mouseX + 'px';
            cursor.style.top = mouseY + 'px';
        });

        function animateFollower() {
            followerX += (mouseX - followerX) * 0.1;
            followerY += (mouseY - followerY) * 0.1;
            
            cursorFollower.style.left = followerX + 'px';
            cursorFollower.style.top = followerY + 'px';
            
            requestAnimationFrame(animateFollower);
        }
        animateFollower();

        document.addEventListener('mousedown', () => {
            cursorFollower.classList.add('clicking');
            cursor.style.transform = 'translate(-50%, -50%) scale(0.8)';
        });

        document.addEventListener('mouseup', () => {
            setTimeout(() => {
                cursorFollower.classList.remove('clicking');
            }, 400);
            cursor.style.transform = 'translate(-50%, -50%) scale(1)';
        });

        // Smooth scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // Intersection Observer for fade-in animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -100px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        document.querySelectorAll('.feature-card, .benefit-item, .content-section').forEach(el => {
            el.style.opacity = '0';
            el.style.transform = 'translateY(30px)';
            el.style.transition = 'opacity 0.8s ease, transform 0.8s ease';
            observer.observe(el);
        });
    </script>
</body>
</html>
