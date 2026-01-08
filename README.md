<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Zscaler Proxy Server</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            color: #333;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }
        
        header {
            background: #2c3e50;
            color: white;
            padding: 25px 30px;
            text-align: center;
        }
        
        .title {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .content {
            padding: 30px;
        }
        
        .proxy-form {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.05);
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2c3e50;
        }
        
        .url-input-container {
            display: flex;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .proxy-prefix {
            background: #3498db;
            color: white;
            padding: 12px 15px;
            font-weight: bold;
            display: flex;
            align-items: center;
        }
        
        #website-url {
            flex: 1;
            padding: 12px 15px;
            border: none;
            font-size: 16px;
            outline: none;
        }
        
        #access-btn {
            background: #27ae60;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 16px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 10px;
        }
        
        #access-btn:hover {
            background: #219653;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        
        .status {
            background: #e3f2fd;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 30px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
        }
        
        .status-item {
            flex: 1;
            min-width: 200px;
            padding: 10px;
        }
        
        .status-label {
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 5px;
        }
        
        .status-value {
            font-size: 1.1rem;
            font-weight: bold;
        }
        
        .status-active {
            color: #27ae60;
        }
        
        .status-inactive {
            color: #e74c3c;
        }
        
        .blocked-info {
            background: #fff8e1;
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid #ffc107;
            margin-top: 20px;
        }
        
        .blocked-info h2 {
            color: #e65100;
            margin-bottom: 15px;
        }
        
        .blocked-info ul {
            padding-left: 20px;
        }
        
        .blocked-info li {
            margin-bottom: 10px;
            line-height: 1.5;
        }
        
        .proxy-result {
            margin-top: 30px;
            padding: 20px;
            background: #f1f8e9;
            border-radius: 10px;
            display: none;
        }
        
        .proxy-result.active {
            display: block;
            animation: fadeIn 0.5s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .result-content {
            margin-top: 15px;
            padding: 15px;
            background: white;
            border-radius: 8px;
            border: 1px solid #ddd;
            min-height: 150px;
        }
        
        .loading {
            text-align: center;
            padding: 20px;
        }
        
        .spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top: 4px solid #3498db;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        footer {
            text-align: center;
            padding: 20px;
            color: #7f8c8d;
            font-size: 0.9rem;
            border-top: 1px solid #eee;
        }
        
        @media (max-width: 768px) {
            .status {
                flex-direction: column;
            }
            
            .status-item {
                margin-bottom: 15px;
            }
            
            .title {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1 class="title">Zscaler Proxy Server</h1>
            <p class="subtitle">Securely access blocked websites bypassing Zscaler restrictions</p>
        </header>
        
        <div class="content">
            <div class="proxy-form">
                <div class="form-group">
                    <label for="website-url">Enter Website URL:</label>
                    <div class="url-input-container">
                        <span class="proxy-prefix">https://proxy.zscaler.com/</span>
                        <input type="text" id="website-url" placeholder="Enter website URL (e.g., google.com)">
                    </div>
                </div>
                <button id="access-btn">Access Website</button>
            </div>
            
            <div class="status">
                <div class="status-item">
                    <div class="status-label">Proxy Status</div>
                    <div id="proxy-status" class="status-value status-active">Active</div>
                </div>
                <div class="status-item">
                    <div class="status-label">Last Access</div>
                    <div id="last-access" class="status-value">Never</div>
                </div>
                <div class="status-item">
                    <div class="status-label">Current Time</div>
                    <div id="currentTime" class="status-value">Loading...</div>
                </div>
            </div>
            
            <div class="proxy-result" id="proxy-result">
                <h2>Proxy Result</h2>
                <div class="loading" id="loading">
                    <div class="spinner"></div>
                    <p>Connecting to proxy server...</p>
                </div>
                <div class="result-content" id="result-content"></div>
            </div>
            
            <div class="blocked-info">
                <h2>                </ul>
            </div>
        </div>
        
        <footer>
            <p>Zscaler Proxy Server v1.0 | For educational purposes only</p>
        </footer>
    </div>

    <script>
        // Update current time
        function showTime() {
            document.getElementById('currentTime').innerHTML = new Date().toUTCString();
        }
        
        showTime();
        setInterval(showTime, 1000);
        
        // Simulate proxy functionality
        document.getElementById('access-btn').addEventListener('click', function() {
            const urlInput = document.getElementById('website-url');
            const url = urlInput.value.trim();
            
            if (!url) {
                alert('Please enter a website URL');
                return;
            }
            
            // Show loading state
            const resultDiv = document.getElementById('proxy-result');
            const loadingDiv = document.getElementById('loading');
            const contentDiv = document.getElementById('result-content');
            
            resultDiv.classList.add('active');
            loadingDiv.style.display = 'block';
            contentDiv.innerHTML = '';
            
            // Simulate proxy processing
            setTimeout(() => {
                loadingDiv.style.display = 'none';
                
                // Simulate different responses based on URL
                let content = '';
                if (url.includes('blocked')) {
                    content = `
                        <h3>Access Denied</h3>
                        <p>The website you are trying to access is currently blocked by Zscaler security policies.</p>
                        <p>Reason: Content filtering - This website is classified as restricted content.</p>
                        <p>Please contact your network administrator for access requests.</p>
                    `;
                } else if (url.includes('zscaler')) {
                    content = `
                        <h3>Proxy Server Information</h3>
                        <p>You are connected to the Zscaler proxy server.</p>
                        <p>Connection established successfully.</p>
                        <p>Proxy server: proxy.zscaler.com</p>
                        <p>Status: Secure connection</p>
                    `;
                } else {
                    content = `
                        <h3>Website Access Successful</h3>
                        <p>Successfully accessed: ${url}</p>
                        <p>Proxy server: proxy.zscaler.com</p>
                        <p>Connection: Secure (HTTPS)</p>
                        <p>Security Status: Clean</p>
                        <p>This website has been verified by our security filters.</p>
                    `;
                }
                
                contentDiv.innerHTML = content;
                
                // Update last access time
                const lastAccessElement = document.getElementById('last-access');
                lastAccessElement.textContent = new Date().toLocaleString();
            }, 2000);
        });
        
        // Add sample URLs to input field on page load
        window.addEventListener('load', function() {
            document.getElementById('website-url').value = 'google.com';
        });
    </script>
</body>
</html>
