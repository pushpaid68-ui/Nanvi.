
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nanvi - Your Personal AI Assistant</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 40px 20px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }

        .header .pulse {
            width: 20px;
            height: 20px;
            background: #4ade80;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(0.95); opacity: 0.7; }
            50% { transform: scale(1.1); opacity: 1; }
            100% { transform: scale(0.95); opacity: 0.7; }
        }

        .main-content {
            padding: 40px;
        }

        .assistant-container {
            background: #f8fafc;
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            border: 2px solid #e2e8f0;
        }

        .voice-controls {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin-bottom: 30px;
        }

        .mic-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 20px 40px;
            font-size: 1.2em;
            border-radius: 50px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            transition: all 0.3s ease;
            margin: 0 auto;
        }

        .mic-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.4);
        }

        .mic-button.listening {
            background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
            animation: listening 1.5s infinite;
        }

        @keyframes listening {
            0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.7); }
            70% { box-shadow: 0 0 0 20px rgba(239, 68, 68, 0); }
            100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); }
        }

        .status {
            text-align: center;
            color: #64748b;
            font-size: 1.1em;
            min-height: 30px;
        }

        .chat-container {
            background: white;
            border-radius: 10px;
            padding: 20px;
            height: 300px;
            overflow-y: auto;
            margin-bottom: 20px;
            border: 1px solid #e2e8f0;
        }

        .message {
            margin-bottom: 15px;
            padding: 12px 18px;
            border-radius: 18px;
            max-width: 80%;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .user-message {
            background: #667eea;
            color: white;
            margin-left: auto;
        }

        .nanvi-message {
            background: #f1f5f9;
            color: #334155;
            margin-right: auto;
        }

        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }

        .feature-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .feature-card:hover {
            transform: translateY(-5px);
        }

        .feature-card h3 {
            color: #667eea;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .commands {
            background: #f8fafc;
            padding: 25px;
            border-radius: 15px;
            margin-top: 30px;
        }

        .commands h3 {
            color: #667eea;
            margin-bottom: 15px;
        }

        .command-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 10px;
            list-style: none;
        }

        .command-list li {
            background: white;
            padding: 10px 15px;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        footer {
            text-align: center;
            padding: 20px;
            color: #64748b;
            border-top: 1px solid #e2e8f0;
        }

        @media (max-width: 600px) {
            .container {
                margin: 10px;
                border-radius: 15px;
            }
            
            .main-content {
                padding: 20px;
            }
            
            .mic-button {
                padding: 15px 30px;
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>
                <span class="pulse"></span>
                Nanvi AI Assistant
                <span class="pulse"></span>
            </h1>
            <p>Your intelligent voice companion ready to help</p>
        </div>

        <div class="main-content">
            <div class="assistant-container">
                <div class="chat-container" id="chatContainer">
                    <div class="message nanvi-message">
                        Hello! I'm Nanvi, your personal AI assistant. How can I help you today?
                    </div>
                </div>

                <div class="voice-controls">
                    <button class="mic-button" id="micButton">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                            <path d="M12 1C11.2044 1 10.4413 1.31607 9.87868 1.87868C9.31607 2.44129 9 3.20435 9 4V12C9 12.7956 9.31607 13.5587 9.87868 14.1213C10.4413 14.6839 11.2044 15 12 15C12.7956 15 13.5587 14.6839 14.1213 14.1213C14.6839 13.5587 15 12.7956 15 12V4C15 3.20435 14.6839 2.44129 14.1213 1.87868C13.5587 1.31607 12.7956 1 12 1Z" fill="currentColor"/>
                            <path d="M19 12C19 12.74 18.9 13.47 18.71 14.17L20.79 16.25C21.24 15.1 21.5 13.88 21.5 12.6V12C21.5 11.45 21.05 11 20.5 11C19.95 11 19.5 11.45 19.5 12C19.5 12.33 19.5 12.67 19.5 13H19C19 12.67 19 12.33 19 12Z" fill="currentColor"/>
                            <path d="M4.5 12C4.5 12.33 4.5 12.67 4.5 13H4C4 12.67 4 12.33 4 12C4 11.45 3.55 11 3 11C2.45 11 2 11.45 2 12C2 14.76 3.28 17.26 5.29 19.04L6.71 17.62C5.06 16.19 4 14.21 4 12H4.5Z" fill="currentColor"/>
                            <path d="M16.5 12C16.5 9.79 15.21 8 13.5 8H10.5C8.79 8 7.5 9.79 7.5 12V14C7.5 16.21 8.79 18 10.5 18H13.5C15.21 18 16.5 16.21 16.5 14V12Z" fill="currentColor"/>
                        </svg>
                        Click to Speak
                    </button>
                    <div class="status" id="status">
                        Click the microphone button and start speaking
                    </div>
                </div>
            </div>

            <div class="features">
                <div class="feature-card">
                    <h3>🎤 Voice Commands</h3>
                    <p>Control everything with your voice. Just say "Hey Nanvi" followed by your command.</p>
                </div>
                <div class="feature-card">
                    <h3>🤖 Smart AI</h3>
                    <p>Powered by advanced AI to understand context and provide intelligent responses.</p>
                </div>
                <div class="feature-card">
                    <h3>🌐 Web Integration</h3>
                    <p>Access information, set reminders, and control smart devices through voice commands.</p>
                </div>
            </div>

            <div class="commands">
                <h3>Try These Commands:</h3>
                <ul class="command-list">
                    <li>"What's the time?"</li>
                    <li>"Tell me a joke"</li>
                    <li>"Set a reminder"</li>
                    <li>"What's the weather?"</li>
                    <li>"Open YouTube"</li>
                    <li>"Search for..."</li>
                    <li>"Play music"</li>
                    <li>"Send email"</li>
                </ul>
            </div>
        </div>

        <footer>
            <p>Nanvi AI Assistant • Version 1.0 • Always here to help you</p>
        </footer>
    </div>

    <script>
        // Speech Recognition Setup
        const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
        const micButton = document.getElementById('micButton');
        const status = document.getElementById('status');
        const chatContainer = document.getElementById('chatContainer');
        
        let recognition;
        let isListening = false;

        if (SpeechRecognition) {
            recognition = new SpeechRecognition();
            recognition.continuous = false;
            recognition.interimResults = false;
            recognition.lang = 'en-US';

            recognition.onstart = () => {
                isListening = true;
                micButton.classList.add('listening');
                status.textContent = "Listening... Speak now!";
            };

            recognition.onresult = (event) => {
                const transcript = event.results[0][0].transcript.toLowerCase();
                addMessage(transcript, 'user');
                processCommand(transcript);
            };

            recognition.onerror = (event) => {
                console.error('Speech recognition error:', event.error);
                status.textContent = "Error occurred. Please try again.";
                isListening = false;
                micButton.classList.remove('listening');
            };

            recognition.onend = () => {
                isListening = false;
                micButton.classList.remove('listening');
                status.textContent = "Click the microphone button to speak";
            };
        } else {
            status.textContent = "Speech recognition not supported in this browser. Please use Chrome or Edge.";
            micButton.disabled = true;
        }

        // Toggle listening
        micButton.addEventListener('click', () => {
            if (!recognition) return;
            
            if (!isListening) {
                recognition.start();
            } else {
                recognition.stop();
            }
        });

        // Add message to chat
        function addMessage(text, sender) {
            const messageDiv = document.createElement('div');
            messageDiv.classList.add('message');
            messageDiv.classList.add(sender === 'user' ? 'user-message' : 'nanvi-message');
            messageDiv.textContent = text;
            chatContainer.appendChild(messageDiv);
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }

        // Process voice commands
        function processCommand(command) {
            status.textContent = "Processing your request...";
            
            // Simulate AI processing delay
            setTimeout(() => {
                let response = "I'm here to help!";
                
                if (command.includes('hello') || command.includes('hi')) {
                    response = "Hello there! How can I assist you today?";
                } else if (command.includes('time')) {
                    const now = new Date();
                    response = `The current time is ${now.toLocaleTimeString()}`;
                } else if (command.includes('date')) {
                    const today = new Date();
                    response = `Today is ${today.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}`;
                } else if (command.includes('joke')) {
                    const jokes = [
                        "Why don't scientists trust atoms? Because they make up everything!",
                        "Why did the scarecrow win an award? He was outstanding in his field!",
                        "What do you call a bear with no teeth? A gummy bear!"
                    ];
                    response = jokes[Math.floor(Math.random() * jokes.length)];
                } else if (command.includes('weather')) {
                    response = "I can check the weather for you. For accurate weather information, I recommend checking a dedicated weather service.";
                } else if (command.includes('remind')) {
                    response = "I'll help you set a reminder. Please tell me what you want to be reminded about and when.";
                    } else if (command.includes('your name')) {
                    response = "I'm Nanvi, your personal AI assistant!";
                } else if (command.includes('how are you')) {
                    response = "I'm doing great! Ready to help you with anything you need.";
                } else if (command.includes('thank')) {
                    response = "You're welcome! Is there anything else I can help you with?";
                } else if (command.includes('bye') || command.includes('goodbye')) {
                    response = "Goodbye! Have a wonderful day!";
                } else if (command.includes('search') || command.includes('find')) {
                    const query = command.replace(/(search|find) (for)?/, '').trim();
                    response = `I found information about "${query}". Here's what I discovered...`;
                } else if (command.includes('play') && command.includes('music')) {
                    response = "Playing your favorite music now!";
                }
                
                // Add voice synthesis response
                speakResponse(response);
                addMessage(response, 'nanvi');
                status.textContent = "Ready for next command";
            }, 1000);
        }

        // Text-to-Speech function
        function speakResponse(text) {
            if ('speechSynthesis' in window) {
                const utterance = new SpeechSynthesisUtterance(text);
                utterance.rate = 1.0;
                utterance.pitch = 1.0;
                utterance.volume = 1.0;
                window.speechSynthesis.speak(utterance);
            }
        }

        // Initialize with welcome message
        window.addEventListener('load', () => {
            setTimeout(() => {
                speakResponse("Hello! I'm Nanvi, your personal AI assistant. How can I help you today?");
            }, 500);
        });
    </script>
</body>
</html>
