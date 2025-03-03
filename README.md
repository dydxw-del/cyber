<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CyberChallenge CTF</title>
    <style>
        :root {
            --primary: #00ff00;
            --dark: #1a1a1a;
            --light: #f0f0f0;
            --background: var(--dark);
            --text: var(--light);
            --card-bg: #2a2a2a;
            --navbar-bg: #000;
            --success: #4caf50;
            --error: #f44336;
        }

        [data-theme="light"] {
            --background: #f0f0f0;
            --text: #1a1a1a;
            --card-bg: #ffffff;
            --navbar-bg: #ffffff;
            --primary: #007bff;
        }

        body {
            margin: 0;
            font-family: 'Courier New', monospace;
            background-color: var(--background);
            color: var(--text);
            transition: background-color 0.3s, color 0.3s;
        }

        .navbar {
            background-color: var(--navbar-bg);
            padding: 1rem;
            position: sticky;
            top: 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .navbar ul {
            list-style: none;
            display: flex;
            margin: 0;
            padding: 0;
        }

        .navbar ul li {
            margin: 0 1rem;
        }

        .navbar a {
            color: var(--primary);
            text-decoration: none;
            font-weight: bold;
            transition: opacity 0.3s;
        }

        .navbar a:hover {
            opacity: 0.8;
        }

        .theme-toggle {
            background: none;
            border: none;
            color: var(--primary);
            cursor: pointer;
            font-size: 1.2rem;
        }

        .hero {
            text-align: center;
            padding: 6rem 2rem;
            background: linear-gradient(45deg, #000, var(--dark));
            color: var(--light);
        }

        .hero h1 {
            color: var(--primary);
            font-size: 4rem;
            margin-bottom: 1rem;
            animation: fadeIn 2s ease-in-out;
        }

        .hero p {
            font-size: 1.2rem;
            animation: fadeIn 3s ease-in-out;
        }

        .container {
            padding: 2rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .challenge-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .challenge-card {
            background: var(--card-bg);
            border: 1px solid var(--primary);
            padding: 1.5rem;
            border-radius: 8px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .challenge-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 20px rgba(0, 255, 0, 0.2);
        }

        .challenge-card h3 {
            color: var(--primary);
            margin-top: 0;
        }

        .badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            background: var(--primary);
            color: var(--background);
            border-radius: 15px;
            font-size: 0.9rem;
            margin-right: 0.5rem;
        }

        .terminal {
            background: #000;
            padding: 1rem;
            border-radius: 4px;
            margin-top: 1rem;
            font-family: monospace;
            position: relative;
            overflow-x: auto;
        }

        .terminal pre {
            margin: 0;
            color: var(--primary);
            white-space: pre-wrap;
        }

        .terminal::after {
            content: ">";
            position: absolute;
            right: 1rem;
            bottom: 1rem;
            color: var(--primary);
            animation: blink 1s infinite;
        }

        .btn {
            background: var(--primary);
            color: var(--background);
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: opacity 0.3s ease, transform 0.3s ease;
            text-decoration: none;
            display: inline-block;
            margin-top: 1rem;
        }

        .btn:hover {
            opacity: 0.9;
            transform: scale(1.05);
        }

        .scoreboard {
            background: var(--card-bg);
            padding: 2rem;
            margin-top: 2rem;
            border-radius: 8px;
            overflow-x: auto;
        }

        .scoreboard table {
            width: 100%;
            border-collapse: collapse;
        }

        .scoreboard th, .scoreboard td {
            padding: 1rem;
            text-align: left;
            border-bottom: 1px solid #444;
        }

        .resources-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .resource-card {
            background: var(--card-bg);
            border: 1px solid var(--primary);
            padding: 1.5rem;
            border-radius: 8px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .resource-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 20px rgba(0, 255, 0, 0.2);
        }

        .resource-card h3 {
            color: var(--primary);
            margin-top: 0;
        }

        footer {
            text-align: center;
            padding: 2rem;
            background: var(--navbar-bg);
            margin-top: 4rem;
            color: var(--text);
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1001;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            overflow-y: auto;
            padding: 2rem 0;
        }

        .modal-content {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: 8px;
            width: 90%;
            max-width: 600px;
            position: relative;
            margin: auto;
        }

        .close-modal {
            position: absolute;
            right: 1rem;
            top: 1rem;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--primary);
        }

        .close-modal:hover {
            opacity: 0.8;
        }

        .hint {
            margin: 1.5rem 0;
            padding: 0.8rem;
            background: rgba(0, 255, 0, 0.1);
            border-left: 3px solid var(--primary);
            border-radius: 4px;
        }

        .input-group {
            margin: 1.5rem 0;
        }

        .flag-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--primary);
            border-radius: 4px;
            background: var(--background);
            color: var(--text);
            margin-bottom: 0.5rem;
            box-sizing: border-box;
        }

        .file-download {
            display: inline-block;
            margin: 1rem 0;
            color: var(--primary);
            text-decoration: none;
            font-weight: bold;
        }

        .file-download:hover {
            text-decoration: underline;
        }

        .success-message, .error-message {
            padding: 0.75rem;
            border-radius: 4px;
            margin-top: 1rem;
            display: none;
        }

        .success-message {
            background: rgba(76, 175, 80, 0.2);
            border: 1px solid var(--success);
            color: var(--success);
        }

        .error-message {
            background: rgba(244, 67, 54, 0.2);
            border: 1px solid var(--error);
            color: var(--error);
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2.5rem;
            }
            
            .navbar ul {
                flex-wrap: wrap;
            }
            
            .navbar ul li {
                margin: 0.5rem;
            }
        }
    </style>
</head>
<body data-theme="dark">
    <nav class="navbar">
        <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#challenges">Challenges</a></li>
            <li><a href="#scoreboard">Scoreboard</a></li>
            <li><a href="#resources">Resources</a></li>
        </ul>
        <button class="theme-toggle" onclick="toggleTheme()">🌓</button>
    </nav>

    <!-- Home Page -->
    <section id="home">
        <div class="hero">
            <h1>CyberChallenge CTF</h1>
            <p>Test your cybersecurity skills with our ethical hacking challenges</p>
            <button class="btn" id="startTraining">Start Training</button>
        </div>
    </section>

    <!-- Challenges Page -->
    <section id="challenges" class="container">
        <h2>Active Challenges</h2>
        <div class="challenge-grid" id="challengeGrid">
            <!-- Challenges will be dynamically loaded here -->
        </div>
    </section>

    <!-- Scoreboard Page -->
    <section id="scoreboard" class="container">
        <h2>Top Players</h2>
        <div class="scoreboard">
            <table id="leaderboard">
                <thead>
                    <tr>
                        <th>Rank</th>
                        <th>Player</th>
                        <th>Points</th>
                        <th>Challenges Solved</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Leaderboard data will be dynamically loaded here -->
                </tbody>
            </table>
        </div>
    </section>

    <!-- Resources Page --> 
    <section id="resources" class="container">
        <h2>Cybersecurity Resources</h2>
        <div class="resources-grid" id="resourcesGrid">
            <!-- Resources will be dynamically loaded here -->
        </div>
    </section>

    <footer>
        <p>Created for educational purposes only. Practice ethical hacking responsibly.</p>
        <p>&copy; 2025 CyberChallenge CTF</p>
    </footer>

    <!-- Challenge Modals -->
    <div id="cookie-monster-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('cookie-monster-modal')">&times;</span>
            <h2>Cookie Monster Challenge</h2>
            <p>You've discovered a website that uses cookies to authenticate users. Your mission is to analyze the cookies and find a way to access the admin panel.</p>
            
            <div class="terminal">
                <pre>$ curl -I http://challenge.local
Host: challenge.local
Date: Sat, 01 Mar 2025 10:00:00 GMT
Set-Cookie: session=dXNlcl9pZD0xMjM0NTY7cm9sZT11c2Vy; Path=/

$ curl http://challenge.local/admin
Access Denied! Only administrators are allowed.</pre>
            </div>
            
            <div class="hint">
                <p><strong>Hint:</strong> The cookie might be using base64 encoding. What happens if you decode it and modify the values?</p>
            </div>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="cookie-monster-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('cookie-monster')">Submit Flag</button>
            </div>
            
            <div id="cookie-monster-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="cookie-monster-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <div id="caesars-secret-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('caesars-secret-modal')">&times;</span>
            <h2>Caesar's Secret Challenge</h2>
            <p>You've intercepted an encrypted message that was encrypted using a variation of the Caesar cipher. Decode the message to retrieve the flag.</p>
            
            <div class="terminal">
                <pre>PBATENGHYNGVBAF_LBH_PENPXRQ_VG</pre>
            </div>
            
            <div class="hint">
                <p><strong>Hint:</strong> The Caesar cipher works by shifting each letter in the alphabet. Try different shift values. The underscore characters are not shifted.</p>
            </div>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="caesars-secret-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('caesars-secret')">Submit Flag</button>
            </div>
            
            <div id="caesars-secret-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="caesars-secret-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <div id="digital-detective-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('digital-detective-modal')">&times;</span>
            <h2>Digital Detective Challenge</h2>
            <p>You've been given a corrupted disk image containing deleted files. Your task is to recover the hidden flag from the image.</p>
            
            <div class="terminal">
                <pre>$ file mystery.img
mystery.img: DOS/MBR boot sector

$ strings mystery.img | grep -i deleted
Several files were deleted at 2025-02-28 15:43:22
Check the hidden sectors for important data</pre>
            </div>
            
            <a href="#" class="file-download">Download mystery.img (10.2 MB)</a>
            
            <div class="hint">
                <p><strong>Hint:</strong> Try using forensic tools like 'foremost' or 'scalpel' to recover deleted files. Look for text files or image files that might contain hidden data.</p>
            </div>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="digital-detective-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('digital-detective')">Submit Flag</button>
            </div>
            
            <div id="digital-detective-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="digital-detective-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <!-- New Challenge Modals -->
    <div id="sql-injection-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('sql-injection-modal')">&times;</span>
            <h2>SQL Injection Challenge</h2>
            <p>You've found a login page that might be vulnerable to SQL injection. Can you bypass the authentication?</p>
            
            <div class="terminal">
                <pre>$ curl https://vulnerable-site.com/login
&lt;form action="/login" method="POST"&gt;
  Username: &lt;input type="text" name="username"&gt;
  Password: &lt;input type="password" name="password"&gt;
  &lt;button type="submit"&gt;Login&lt;/button&gt;
&lt;/form&gt;

$ curl -X POST https://vulnerable-site.com/login -d "username=admin&password=test"
Invalid credentials</pre>
            </div>
            
            <div class="hint">
                <p><strong>Hint:</strong> Try common SQL injection techniques to bypass the authentication. What happens if you use special characters in the username field?</p>
            </div>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="sql-injection-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('sql-injection')">Submit Flag</button>
            </div>
            
            <div id="sql-injection-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="sql-injection-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <div id="hidden-in-plain-sight-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('hidden-in-plain-sight-modal')">&times;</span>
            <h2>Hidden in Plain Sight Challenge</h2>
            <p>This image appears normal, but it contains hidden data. Extract the secret message using steganography techniques.</p>
            
            <img src="/api/placeholder/400/300" alt="Steganography challenge image" style="width: 100%; margin: 1rem 0;">
            
            <div class="hint">
                <p><strong>Hint:</strong> Try using tools like 'steghide' or 'zsteg' to analyze the image. The password might be related to the image content.</p>
            </div>
            
            <a href="#" class="file-download">Download secret.jpg (1.8 MB)</a>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="hidden-in-plain-sight-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('hidden-in-plain-sight')">Submit Flag</button>
            </div>
            
            <div id="hidden-in-plain-sight-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="hidden-in-plain-sight-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <div id="broken-hash-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('broken-hash-modal')">&times;</span>
            <h2>Broken Hash Challenge</h2>
            <p>You've intercepted a SHA-1 hash from a legacy system. Crack it to find the original password.</p>
            
            <div class="terminal">
                <pre>$ cat intercepted_hash.txt
5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8

$ cat note.txt
The password follows the pattern: lowercase word + 2 digits
Common dictionary words are used.</pre>
            </div>
            
            <div class="hint">
                <p><strong>Hint:</strong> Use a tool like 'hashcat' or an online hash cracker with a dictionary attack. The hash is SHA-1, and the password follows a specific pattern.</p>
            </div>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="broken-hash-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('broken-hash')">Submit Flag</button>
            </div>
            
            <div id="broken-hash-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="broken-hash-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <div id="packet-inspector-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeModal('packet-inspector-modal')">&times;</span>
            <h2>Packet Inspector Challenge</h2>
            <p>Analyze this network capture file to find suspicious communications and extract the flag.</p>
            
            <div class="terminal">
                <pre>$ file capture.pcap
capture.pcap: tcpdump capture file - version 2.4 (Ethernet, 96-bit encapsulation)

$ tcpdump -r capture.pcap | head -5
reading from file capture.pcap, link-type EN10MB
13:45:22.123456 IP 192.168.1.100.49152 > 203.0.113.37.80: TCP 74 [...]
13:45:22.234567 IP 203.0.113.37.80 > 192.168.1.100.49152: TCP 60 [...]
13:45:22.345678 IP 192.168.1.100.49152 > 203.0.113.37.80: HTTP GET /secret_area
13:45:22.456789 IP 203.0.113.37.80 > 192.168.1.100.49152: HTTP 401 Unauthorized</pre>
            </div>
            
            <a href="#" class="file-download">Download capture.pcap (3.4 MB)</a>
            
            <div class="hint">
                <p><strong>Hint:</strong> Look for HTTP or DNS traffic that might contain encoded data. Pay special attention to traffic with unusual patterns or destinations.</p>
            </div>
            
            <div class="input-group">
                <input type="text" class="flag-input" id="packet-inspector-flag" placeholder="Enter flag: flag{...}">
                <button class="btn submit-flag" onclick="checkFlag('packet-inspector')">Submit Flag</button>
            </div>
            
            <div id="packet-inspector-success" class="success-message">
                Congratulations! You've solved the challenge!
            </div>
            
            <div id="packet-inspector-error" class="error-message">
                Incorrect flag. Try again!
            </div>
        </div>
    </div>

    <script>
        // Set initial theme
        document.body.setAttribute('data-theme', 'dark');

        // Theme Toggle
        const toggleTheme = () => {
            const body = document.body;
            const currentTheme = body.getAttribute('data-theme') || 'dark';
            const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            body.setAttribute('data-theme', newTheme);
        };

        // Dynamic Challenge Loading
        const challenges = [
            {
                id: "cookie-monster",
                category: "Web",
                points: 100,
                title: "Cookie Monster",
                description: "Can you figure out what's stored in these cookies?",
                terminal: "$ curl -I http://challenge.local\nSet-Cookie: session=dXNlcl9pZD0xMjM0NTY7cm9sZT11c2Vy"
            },
            {
                id: "caesars-secret",
                category: "Crypto",
                points: 200,
                title: "Caesar's Secret",
                description: "Ancient encryption with a modern twist.",
                terminal: "PBATENGHYNGVBAF_LBH_PENPXRQ_VG"
            },
            {
                id: "digital-detective",
                category: "Forensics",
                points: 300,
                title: "Digital Detective",
                description: "Recover deleted files from this disk image.",
                terminal: "$ file mystery.img\nmystery.img: DOS/MBR boot sector"
            },
            {
                id: "sql-injection",
                category: "Web",
                points: 150,
                title: "SQL Injection",
                description: "Bypass authentication using SQL injection techniques.",
                terminal: "$ curl -X POST https://vulnerable-site.com/login -d \"username=admin&password=test\"\nInvalid credentials"
            },
            {
                id: "hidden-in-plain-sight",
                category: "Steganography",
                points: 250,
                title: "Hidden in Plain Sight",
                description: "Extract the secret message hidden in this innocent-looking image.",
                terminal: "$ file secret.jpg\nsecret.jpg: JPEG image data, JFIF standard 1.01"
            },
            {
                id: "broken-hash",
                category: "Crypto",
                points: 200,
                title: "Broken Hash",
                description: "Crack this SHA-1 hash to find the original password.",
                terminal: "5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8"
            },
            {
                id: "packet-inspector",
                category: "Network",
                points: 350,
                title: "Packet Inspector",
                description: "Analyze this network capture file to find suspicious communications.",
                terminal: "$ tcpdump -r capture.pcap | head -3\nreading from file capture.pcap, link-type EN10MB\n13:45:22.123456 IP 192.168.1.100.49152 > 203.0.113.37.80: TCP 74 [...]"
            }
        ];

        const challengeGrid = document.getElementById('challengeGrid');
        challenges.forEach(challenge => {
            const card = document.createElement('div');
            card.className = 'challenge-card';
            card.innerHTML = `
                <span class="badge">${challenge.category}</span>
                <span class="badge">${challenge.points} pts</span>
                <h3>${challenge.title}</h3>
                <p>${challenge.description}</p>
                <div class="terminal">
                    <pre>${challenge.terminal}</pre>
                </div>
                <button class="btn" onclick="openModal('${challenge.id}-modal')">Solve Challenge</button>
            `;
            challengeGrid.appendChild(card);
        });

        // Leaderboard Data
        const leaderboardData = [
            { rank: 1, player: "CyberNinja", points: 2500, solved: 12 },
            { rank: 2, player: "ByteMaster", points: 2100, solved: 10 },
            { rank: 3, player: "SecurityPro", points: 1800, solved: 8 },
            { rank: 4, player: "H4ckerGirl", points: 1650, solved: 7 },
            { rank: 5, player: "CodeBreaker", points: 1500, solved: 6 }
        ];

        const leaderboard = document.getElementById('leaderboard').getElementsByTagName('tbody')[0];
        leaderboardData.forEach(entry => {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${entry.rank}</td>
                <td>${entry.player}</td>
                <td>${entry.points}</td>
                <td>${entry.solved}</td>
            `;
            leaderboard.appendChild(row);
        });

        // Resources Data
        const resources = [
            {
                title: "Kali Linux",
                description: "The ultimate penetration testing platform with hundreds of built-in security tools.",
                link: "https://www.kali.org/"
            },
            {
                title: "OWASP",
                description: "Open Web Application Security Project - resources for secure application development.",
                link: "https://owasp.org/"
            },
            {
                title: "Hack The Box",
                description: "An online platform to test and advance your cybersecurity skills through challenges.",
                link: "https://www.hackthebox.com/"
            },
            {
                title: "TryHackMe",
                description: "Learn cybersecurity through hands-on exercises and challenges.",
                link: "https://tryhackme.com/"
            },
            {
                title: "CyberChef",
                description: "A web app for encryption, encoding, compression and data analysis.",
                link: "https://gchq.github.io/CyberChef/"
            },
            {
                title: "PortSwigger Web Security Academy",
                description: "Free online training on web security vulnerabilities.",
                link: "https://portswigger.net/web-security"
            }
        ];

        const resourcesGrid = document.getElementById('resourcesGrid');
        resources.forEach(resource => {
            const card = document.createElement('div');
            card.className = 'resource-card';
            card.innerHTML = `
                <h3>${resource.title}</h3>
                <p>${resource.description}</p>
                <a href="${resource.link}" target="_blank" class="btn">Visit Resource</a>
            `;
            resourcesGrid.appendChild(card);
        });

        // Smooth Scroll
        document.getElementById('startTraining').addEventListener('click', () => {
            document.querySelector('#challenges').scrollIntoView({ behavior: 'smooth' });
        });

        // Modal Functions
        const openModal = (modalId) => {
            document.getElementById(modalId).style.display = 'flex';
        };

        const closeModal = (modalId) => {
            document.getElementById(modalId).style.display = 'none';
            
            // Reset messages
            const modalElement = document.getElementById(modalId);
            if (modalElement) {
              const successMessage = modalElement.querySelector('.success-message');
              const errorMessage = modalElement.querySelector('.error-message');
              
              if (successMessage) successMessage.style.display = 'none';
              if (errorMessage) errorMessage.style.display = 'none';
            }
          };
        </script>
      </body>
      </html>
      <script>
        // Flag Submission
        const checkFlag = (challengeId) => {
          const flagInput = document.getElementById(`${challengeId}-flag`);
          const successMessage = document.getElementById(`${challengeId}-success`);
          const errorMessage = document.getElementById(`${challengeId}-error`);

          // Dummy flag validation logic
          const correctFlags = {
            "cookie-monster": "flag{cookie_monster}",
            "caesars-secret": "flag{caesars_secret}",
            "digital-detective": "flag{digital_detective}",
            "sql-injection": "flag{sql_injection}",
            "hidden-in-plain-sight": "flag{hidden_in_plain_sight}",
            "broken-hash": "flag{broken_hash}",
            "packet-inspector": "flag{packet_inspector}"
          };

          if (flagInput.value === correctFlags[challengeId]) {
            successMessage.style.display = 'block';
            errorMessage.style.display = 'none';
          } else {
            successMessage.style.display = 'none';
            errorMessage.style.display = 'block';
          }
        };
      </script>
