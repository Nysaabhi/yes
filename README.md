<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Nysa Chatbot</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
:root {
    --primary-color: #FFD700;
    --secondary-color: #FDB931;
    --background-dark: #1a1a1f;
    --text-light: #ffffff;
    --text-dark: #000000;
    --accent-gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Poppins', sans-serif;
    background-color: var(--background-dark);
    color: var(--text-light);
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
}

/* Header Styles */
.header {
    padding: 8px 16px;
    background: rgba(26, 26, 31, 0.95);
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 1000;
    border-bottom: 2px solid var(--primary-color);
    backdrop-filter: blur(10px);
    height: 60px;
}

.header-content {
    max-width: 1400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100%;
}

.logo {
    font-size: 1.8em;
    font-weight: 900;
    background: var(--accent-gradient);
    -webkit-background-clip: text;
    color: transparent;
    letter-spacing: 1.2px;
}

.connect-wallet {
    padding: 10px 20px;
    background: var(--accent-gradient);
    border: none;
    border-radius: 50px;
    color: var(--text-dark);
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 0.95em;
    letter-spacing: 0.5px;
}

.connect-wallet:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(255, 215, 0, 0.2);
}

/* Chatbot Container */
.chatbot-container {
    position: absolute;
    top: 70px;
    left: 0;
    right: 0;
    height: calc(100vh - 70px);
    background: rgba(26, 26, 31, 0.95);
    display: flex;
    flex-direction: column;
    z-index: 999;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 215, 0, 0.1);
}

/* Chat Header */
.chat-header {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    width: 100%;
    padding: 15px;
    background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(253, 185, 49, 0.1));
    border-bottom: 1px solid rgba(255, 215, 0, 0.2);
    display: flex;
    justify-content: space-between;
    align-items: center;
    z-index: 2;
}

.chat-status {
    display: flex;
    align-items: center;
    color: var(--primary-color);
    font-weight: 600;
    font-size: 0.95em;
}

.status-dot {
    width: 8px;
    height: 8px;
    background: var(--primary-color);
    border-radius: 50%;
    margin-right: 8px;
    animation: pulse 2s infinite;
}

/* Chat Messages */
.chat-messages {
    margin-top: 60px;
    margin-bottom: 70px;
    height: calc(100% - 130px);
    overflow-y: auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    scrollbar-width: thin;
    scrollbar-color: var(--primary-color) transparent;
}

.chat-messages::-webkit-scrollbar {
    width: 6px;
}

.chat-messages::-webkit-scrollbar-track {
    background: transparent;
}

.chat-messages::-webkit-scrollbar-thumb {
    background-color: var(--primary-color);
    border-radius: 3px;
}

.message {
    display: flex;
    gap: 12px;
    max-width: 85%;
    animation: messageSlide 0.3s ease-out;
}

.bot-message {
    align-self: flex-start;
}

.user-message {
    align-self: flex-end;
    flex-direction: row-reverse;
}

.message-avatar {
    width: 36px;
    height: 36px;
    background: rgba(255, 215, 0, 0.1);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--primary-color);
}

.message-content {
    background: rgba(255, 255, 255, 0.05);
    padding: 12px 16px;
    border-radius: 16px;
    color: var(--text-light);
    font-size: 0.95em;
}

.user-message .message-content {
    background: rgba(255, 215, 0, 0.1);
}

/* Chat Input */
.chat-input-container {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 16px;
    border-top: 1px solid rgba(255, 215, 0, 0.1);
    display: flex;
    gap: 12px;
    align-items: center;
    background: rgba(26, 26, 31, 0.95);
    z-index: 2;
}

#chatInput {
    flex: 1;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 215, 0, 0.2);
    border-radius: 12px;
    padding: 12px 16px;
    color: var(--text-light);
    font-size: 0.95em;
    transition: all 0.3s ease;
}

#chatInput:focus {
    outline: none;
    border-color: var(--primary-color);
    background: rgba(255, 255, 255, 0.08);
}

.input-actions {
    display: flex;
    gap: 8px;
}

.input-actions button {
    background: none;
    border: none;
    color: rgba(255, 215, 0, 0.7);
    cursor: pointer;
    padding: 8px;
    border-radius: 50%;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
}

.input-actions button:hover {
    color: var(--primary-color);
    background: rgba(255, 215, 0, 0.1);
}

/* Bottom Navigation */
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(26, 26, 31, 0.95);
    padding: 8px 0;
    backdrop-filter: blur(10px);
    border-top: 1px solid rgba(255, 215, 0, 0.2);
    z-index: 1000;
    height: 60px;
}

.nav-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    max-width: 600px;
    margin: 0 auto;
    height: 100%;
}

.nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-decoration: none;
    color: var(--text-light);
    transition: all 0.3s ease;
    padding: 5px;
    cursor: pointer;
}

.nav-item i {
    font-size: 20px;
    margin-bottom: 4px;
}

.nav-item span {
    font-size: 12px;
}

.nav-item.active {
    color: #FFD700;
}

.nav-item:hover {
    color: #FFD700;
    transform: translateY(-2px);
}

/* Animations */
@keyframes pulse {
    0% { opacity: 1; }
    50% { opacity: 0.5; }
    100% { opacity: 1; }
}

@keyframes messageSlide {
    from {
        opacity: 0;
        transform: translateY(10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* Responsive Styles */
@media (max-width: 768px) {
    .chatbot-container {
        height: calc(100vh - 60px);
        top: 60px;
    }

    .chat-messages {
        margin-bottom: 130px;
    }

    .chat-input-container {
        bottom: 60px;
    }

    .connect-wallet {
        padding: 8px 16px;
        font-size: 0.9em;
    }
}

@media (max-width: 480px) {
    .header {
        padding: 8px 12px;
    }

    .logo {
        font-size: 1.5em;
    }

    .connect-wallet {
        padding: 8px 14px;
        font-size: 0.85em;
    }

    .chat-messages {
        padding: 15px;
    }

    .message {
        max-width: 90%;
    }

    .message-content {
        font-size: 0.9em;
    }

    .nav-item i {
        font-size: 18px;
    }

    .nav-item span {
        font-size: 11px;
    }
}

/* Dark mode optimization */
@media (prefers-color-scheme: dark) {
    .chatbot-container {
        background: rgba(26, 26, 31, 0.98);
    }
    
    .chat-input-container,
    .header,
    .bottom-nav {
        background: rgba(26, 26, 31, 0.98);
    }
}

/* Ensure proper spacing for messages near the bottom */
.chat-messages .message:last-child {
    margin-bottom: 10px;
}
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="header-content">
            <div class="logo">Nysa</div>
            <button class="connect-wallet">
                <i class="fas fa-wallet"></i>
                Connect
            </button>
        </div>
    </header>

    <!-- Chatbot -->
    <div class="chatbot-container">
        <div class="chat-header">
            <div class="chat-status">
                <span class="status-dot"></span>
                Nysa AI Assistant
            </div>
            <div class="chat-actions">
            </div>
        </div>
        <div class="chat-messages" id="chatMessages">
            <div class="message bot-message">
                <div class="message-avatar">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="message-content">
                    <p>Hello! I'm your Web3 assistant. How can I help you explore the blockchain universe today?</p>
                </div>
            </div>
        </div>
        <div class="chat-input-container">
            <input type="text" id="chatInput" placeholder="Ask about Web3, NFTs, or blockchain..." />
            <div class="input-actions">
                <button class="voice-input">
                    <i class="fas fa-microphone"></i>
                </button>
                <button class="send-message">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

<!-- Bottom Navigation -->
<nav class="bottom-nav">
    <div class="nav-container">
        <div class="nav-item active" data-page="home">
            <a href="https://nysaabhi.github.io/chat">
                <i class="fas fa-home"></i>
            </a>
            <span>Home</span>
        </div>
        <div class="nav-item" data-page="tournament">
            <a href="https://nysaabhi.github.io/mymom">
                <i class="fas fa-trophy"></i>
            </a>
            <span>Tournament</span>
        </div>
        <div class="nav-item" data-page="gallery">
            <a href="gallery.html">
                <i class="fas fa-vr-cardboard"></i>
            </a>
            <span>Gallery</span>
        </div>
        <div class="nav-item" data-page="location">
            <a href="location.html">
                <i class="fas fa-map"></i>
            </a>
            <span>Location</span>
        </div>
        <div class="nav-item" data-page="listings">
            <a href="listings.html">
                <i class="fas fa-list"></i>
            </a>
            <span>Listings</span>
        </div>
    </div>
</nav>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // DOM Elements
            const chatInput = document.getElementById('chatInput');
            const chatMessages = document.getElementById('chatMessages');
            const sendButton = document.querySelector('.send-message');
            const minimizeButton = document.querySelector('.minimize-chat');
            const clearButton = document.querySelector('.clear-chat');
            const chatContainer = document.querySelector('.chatbot-container');
            const voiceButton = document.querySelector('.voice-input');
            const searchInput = document.querySelector('.search-input');
            const searchButton = document.querySelector('.search-button');
            const navItems = document.querySelectorAll('.nav-item');
            const connectWalletBtn = document.querySelector('.connect-wallet');

            // Chatbot functionality
            const generateResponse = (message) => {
                const responses = {
                    nft: [
                        "NFTs (Non-Fungible Tokens) are unique digital assets stored on the blockchain. They can represent art, music, videos, and more.",
                        "Popular NFT marketplaces include OpenSea, Rarible, and Foundation.",
                        "Always verify the authenticity of NFT collections before making a purchase."
                    ],
                    blockchain: [
                        "Blockchain is a distributed ledger technology that ensures transparency and security.",
                        "Popular blockchain networks include Ethereum, Solana, and Binance Smart Chain.",
                        "Smart contracts are self-executing contracts with terms directly written into code."
                    ],
                    defi: [
                        "DeFi (Decentralized Finance) offers financial services without traditional intermediaries.",
                        "Common DeFi activities include lending, borrowing, and yield farming.",
                        "Always research protocols thoroughly and be aware of the risks involved."
                    ],
                    wallet: [
                        "Crypto wallets are essential for storing and managing your digital assets.",
                        "Popular wallets include MetaMask, Trust Wallet, and Phantom.",
                        "Never share your private keys or seed phrase with anyone."
                    ],
                    default: [
                        "I'm here to help you explore the Web3 space. Feel free to ask about NFTs, blockchain, DeFi, or crypto wallets.",
                        "That's an interesting question. Let me help you understand this aspect of Web3.",
                        "I'd be happy to explain more about this topic in the context of blockchain technology."
                    ]
                };

                const topic = Object.keys(responses).find(key => 
                    message.toLowerCase().includes(key)
                ) || 'default';

                return responses[topic][Math.floor(Math.random() * responses[topic].length)];
            };

            const addMessage = (text, sender) => {
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${sender}-message`;
                
                const avatar = document.createElement('div');
                avatar.className = 'message-avatar';
                avatar.innerHTML = `<i class="fas fa-${sender === 'bot' ? 'robot' : 'user'}"></i>`;

                const content = document.createElement('div');
                content.className = 'message-content';
                content.innerHTML = `
                    <p>${text}</p>
                    <span class="message-time">${new Date().toLocaleTimeString()}</span>
                `;

                if (sender === 'user') {
                    messageDiv.appendChild(content);
                    messageDiv.appendChild(avatar);
                } else {
                    messageDiv.appendChild(avatar);
                    messageDiv.appendChild(content);
                }

                chatMessages.appendChild(messageDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            };

            const sendMessage = () => {
                const message = chatInput.value.trim();
                if (!message) return;

                addMessage(message, 'user');
                chatInput.value = '';

                // Simulate typing indicator
                const typingDiv = document.createElement('div');
                typingDiv.className = 'message bot-message typing';
                typingDiv.innerHTML = '<div class="message-avatar"><i class="fas fa-robot"></i></div><div class="message-content"><p>typing...</p></div>';
                chatMessages.appendChild(typingDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;

                // Simulate bot response with delay
                setTimeout(() => {
                    chatMessages.removeChild(typingDiv);
                    const response = generateResponse(message);
                    addMessage(response, 'bot');
                }, 1500);
            };

            // Voice input functionality
            const startVoiceInput = () => {
                if ('webkitSpeechRecognition' in window) {
                    const recognition = new webkitSpeechRecognition();
                    recognition.continuous = false;
                    recognition.interimResults = false;

                    recognition.onstart = () => {
                        voiceButton.style.color = 'var(--primary-color)';
                    };

                    recognition.onresult = (event) => {
                        const text = event.results[0][0].transcript;
                        chatInput.value = text;
                    };

                    recognition.onend = () => {
                        voiceButton.style.color = 'rgba(255, 215, 0, 0.7)';
                    };

                    recognition.start();
                }
            };

            // Search functionality
            const performSearch = () => {
                const query = searchInput.value.trim();
                if (!query) return;

                // Add search animation
                searchButton.innerHTML = '<i class="fas fa-spinner fa-spin"></i>';
                
                // Simulate search delay
                setTimeout(() => {
                    searchButton.innerHTML = '<i class="fas fa-search"></i>';
                    // Here you would typically handle the actual search
                    addMessage(`Searching for: ${query}`, 'user');
                    addMessage('Here are some relevant results from the Web3 universe...', 'bot');
                }, 1000);
            };

            // Wallet connection
            const connectWallet = async () => {
                if (typeof window.ethereum !== 'undefined') {
                    try {
                        const accounts = await window.ethereum.request({ 
                            method: 'eth_requestAccounts' 
                        });
                        connectWalletBtn.innerHTML = `
                            <i class="fas fa-check-circle"></i>
                            ${accounts[0].slice(0, 6)}...${accounts[0].slice(-4)}
                        `;
                        addMessage('Wallet connected successfully!', 'bot');
                    } catch (error) {
                        addMessage('Failed to connect wallet. Please try again.', 'bot');
                    }
                } else {
                    addMessage('Please install MetaMask or another Web3 wallet.', 'bot');
                }
            };

            // Event listeners
            sendButton.addEventListener('click', sendMessage);
            chatInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') sendMessage();
            });

            minimizeButton.addEventListener('click', () => {
                chatContainer.style.display = 
                    chatContainer.style.display === 'none' ? 'flex' : 'none';
            });

            clearButton.addEventListener('click', () => {
                const firstMessage = chatMessages.firstElementChild;
                chatMessages.innerHTML = '';
                chatMessages.appendChild(firstMessage);
            });

            voiceButton.addEventListener('click', startVoiceInput);

            searchButton.addEventListener('click', performSearch);
            searchInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') performSearch();
            });

            connectWalletBtn.addEventListener('click', connectWallet);

            navItems.forEach(item => {
                item.addEventListener('click', () => {
                    navItems.forEach(i => i.classList.remove('active'));
                    item.classList.add('active');
                });
            });

            // Handle metamask events
            if (typeof window.ethereum !== 'undefined') {
                window.ethereum.on('accountsChanged', (accounts) => {
                    if (accounts.length === 0) {
                        connectWalletBtn.innerHTML = `
                            <i class="fas fa-wallet"></i>
                            Connect Wallet
                        `;
                    }
                });
            }
        });
    </script>
</body>
