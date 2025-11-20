# KIT
HUB

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>1B3T - Messenger</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
       
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: #000000;
            color: #ffffff;
            height: 100vh;
            overflow: hidden;
        }
       
        .container {
            display: flex;
            flex-direction: column;
            height: 100vh;
            max-width: 1400px;
            margin: 0 auto;
        }
       
        .header {
            background: #0a0a0a;
            border-bottom: 1px solid #1a1a1a;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
       
        .room-name {
            font-size: 1.1em;
            font-weight: 600;
            color: #ffffff;
        }
       
        .room-info {
            font-size: 0.8em;
            color: #888888;
            margin-top: 3px;
        }

        .media-button {
            padding: 8px 16px;
            background: #1a1a1a;
            border: 1px solid #333333;
            color: #ffffff;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.85em;
        }

        .media-button:hover {
            background: #252525;
        }
       
        .messages {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background: #000000;
        }
       
        .messages::-webkit-scrollbar {
            width: 6px;
        }
       
        .messages::-webkit-scrollbar-track {
            background: #000000;
        }
       
        .messages::-webkit-scrollbar-thumb {
            background: #1a1a1a;
            border-radius: 3px;
        }
       
        .message-group {
            display: flex;
            gap: 10px;
            margin-bottom: 16px;
            animation: fadeIn 0.3s ease-in;
        }
       
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
       
        .message-group.private {
            opacity: 0.6;
        }
       
        .avatar {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            background: #1a1a1a;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
        }
       
        .avatar svg {
            width: 24px;
            height: 24px;
        }
       
        .message-content-wrapper {
            flex: 1;
            min-width: 0;
        }
       
        .message-header {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 5px;
        }
       
        .username {
            color: #ffffff;
            font-size: 0.85em;
            font-weight: 600;
        }
       
        .timestamp {
            color: #666666;
            font-size: 0.75em;
        }
       
        .message-bubble {
            background: #1a1a1a;
            border-radius: 18px;
            padding: 10px 14px;
            display: inline-block;
            max-width: 70%;
            word-wrap: break-word;
            font-size: 0.95em;
            line-height: 1.5;
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
        }
       
        .message-group.private .message-bubble {
            border: 1px solid #3a3a0a;
            background: #1a1a0a;
        }
       
        .private-notice {
            font-size: 0.7em;
            color: #ffaa00;
            margin-top: 4px;
            margin-left: 14px;
        }
       
        .attachment-preview-area {
            background: #0a0a0a;
            border-top: 1px solid #1a1a1a;
            padding: 10px 20px;
            display: none;
        }

        .attachment-preview-area.show {
            display: block;
        }

        .attachment-preview-list {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .attachment-preview-item {
            position: relative;
            background: #1a1a1a;
            border-radius: 8px;
            padding: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.85em;
        }

        .attachment-preview-item img {
            width: 50px;
            height: 50px;
            object-fit: cover;
            border-radius: 4px;
        }

        .attachment-preview-name {
            max-width: 150px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            color: #ffffff;
        }

        .attachment-remove {
            background: #ff4444;
            color: #ffffff;
            border: none;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            line-height: 1;
            margin-left: 4px;
        }

        .attachment-remove:hover {
            background: #ff6666;
        }

        .input-area {
            background: #0a0a0a;
            border-top: 1px solid #1a1a1a;
            padding: 15px 20px;
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .attach-button {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #1a1a1a;
            color: #888888;
            border: none;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .attach-button:hover {
            background: #252525;
            color: #ffffff;
        }

        input[type="file"] {
            display: none;
        }
       
        .message-input {
            flex: 1;
            background: #1a1a1a;
            border: none;
            color: #ffffff;
            padding: 12px 16px;
            border-radius: 22px;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            font-size: 0.95em;
            outline: none;
            transition: background 0.2s;
        }
       
        .message-input:focus {
            background: #252525;
        }

        .message-input:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
       
        .send-button {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            background: #0a0a0a;
            color: #ffffff;
            border: 1px solid #1a1a1a;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }
       
        .send-button:hover {
            background: #1a1a1a;
            border-color: #333333;
        }
       
        .send-button:active {
            background: #00ff00;
            color: #000000;
            transform: scale(0.95);
        }

        .send-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .attachment {
            margin-top: 6px;
            padding: 8px 12px;
            background: #252525;
            border-radius: 12px;
            font-size: 0.85em;
            color: #888888;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            cursor: pointer;
        }

        .attachment:hover {
            background: #333333;
        }

        .attachment-image {
            margin-top: 6px;
            max-width: 300px;
            border-radius: 12px;
            cursor: pointer;
        }

        .error-notice {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: #ff4444;
            color: #ffffff;
            padding: 12px 20px;
            border-radius: 8px;
            font-size: 0.9em;
            z-index: 1000;
            animation: slideDown 0.3s ease-out;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translate(-50%, -20px);
            }
            to {
                opacity: 1;
                transform: translate(-50%, 0);
            }
        }
       
        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #666666;
            font-size: 0.9em;
        }

        .ban-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 9999;
        }

        .ban-overlay.show {
            display: flex;
        }

        .ban-message {
            background: #1a1a1a;
            border: 2px solid #ff4444;
            padding: 40px;
            border-radius: 12px;
            text-align: center;
        }

        .ban-message h2 {
            color: #ff4444;
            font-size: 2em;
            margin-bottom: 10px;
        }

        .ban-message p {
            color: #888888;
            font-size: 1em;
        }

        .media-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }

        .media-modal.show {
            display: flex;
        }

        .media-modal-content {
            background: #0a0a0a;
            border: 1px solid #1a1a1a;
            border-radius: 12px;
            width: 90%;
            max-width: 800px;
            max-height: 80vh;
            display: flex;
            flex-direction: column;
        }

        .media-modal-header {
            padding: 20px;
            border-bottom: 1px solid #1a1a1a;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .media-modal-header h3 {
            font-size: 1.1em;
        }

        .close-modal {
            background: none;
            border: none;
            color: #888888;
            font-size: 1.5em;
            cursor: pointer;
        }

        .close-modal:hover {
            color: #ffffff;
        }

        .media-modal-body {
            padding: 20px;
            overflow-y: auto;
        }

        .media-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 15px;
        }

        .media-item {
            background: #1a1a1a;
            border-radius: 8px;
            overflow: hidden;
            cursor: pointer;
            transition: transform 0.2s;
            animation: fadeIn 0.4s ease-in;
        }

        .media-item:hover {
            transform: scale(1.05);
        }

        .media-item img {
            width: 100%;
            height: 150px;
            object-fit: cover;
        }

        .media-item-file {
            padding: 20px;
            text-align: center;
            height: 150px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .media-item-file span {
            font-size: 2em;
            margin-bottom: 8px;
        }

        .media-item-name {
            font-size: 0.75em;
            color: #888888;
            padding: 8px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
    </style>
</head>
<body>
    <div class="ban-overlay" id="banOverlay">
        <div class="ban-message">
            <h2>BAN</h2>
            <p>You have been banned from this room</p>
        </div>
    </div>

    <div class="media-modal" id="mediaModal">
        <div class="media-modal-content">
            <div class="media-modal-header">
                <h3>Media & Files</h3>
                <button class="close-modal" onclick="closeMediaModal()">×</button>
            </div>
            <div class="media-modal-body">
                <div class="media-grid" id="mediaGrid"></div>
            </div>
        </div>
    </div>

    <div class="container">
        <div class="header">
            <div>
                <div class="room-name">1B3T</div>
                <div class="room-info">Anonymous Room • Messages expire after 1 hour</div>
            </div>
            <button class="media-button" onclick="openMediaModal()">Media & Files</button>
        </div>
       
        <div class="messages" id="messages">
            <div class="empty-state">No messages yet. Start the conversation.</div>
        </div>

        <div class="attachment-preview-area" id="attachmentPreview">
            <div class="attachment-preview-list" id="attachmentList"></div>
        </div>
       
        <div class="input-area">
            <button class="attach-button" onclick="document.getElementById('fileInput').click()">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M21.44 11.05l-9.19 9.19a6 6 0 0 1-8.49-8.49l9.19-9.19a4 4 0 0 1 5.66 5.66l-9.2 9.19a2 2 0 0 1-2.83-2.83l8.49-8.48"/>
                </svg>
            </button>
            <input type="file" id="fileInput" accept="image/*,video/*,.pdf,.doc,.docx,.txt" multiple>
            <input 
                type="text" 
                class="message-input" 
                id="messageInput" 
                placeholder="Message..."
                maxlength="300"
            >
            <button class="send-button" id="sendButton" onclick="sendMessage()">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M22 2L11 13M22 2l-7 20-4-9-9-4 20-7z"/>
                </svg>
            </button>
        </div>
    </div>

    <script>
        const _0x4a2b=['\x73\x71\x75\x61\x72\x65','\x23\x66\x66\x66\x66\x66\x66','\x74\x72\x69\x61\x6e\x67\x6c\x65','\x50\x68\x61\x6e\x74\x6f\x6d','\x53\x68\x61\x64\x6f\x77','\x47\x68\x6f\x73\x74','\x57\x72\x61\x69\x74\x68','\x53\x70\x65\x63\x74\x65\x72','\x43\x69\x70\x68\x65\x72','\x45\x6e\x69\x67\x6d\x61','\x4d\x69\x72\x61\x67\x65','\x4e\x65\x78\x75\x73','\x56\x6f\x72\x74\x65\x78','\x45\x63\x68\x6f','\x50\x75\x6c\x73\x65','\x47\x6c\x69\x74\x63\x68','\x4e\x6f\x76\x61','\x5a\x65\x72\x6f'];
        
        const shapes = [
            { type: _0x4a2b[0], color: _0x4a2b[1] },
            { type: _0x4a2b[2], color: _0x4a2b[1] }
        ];
        
        const names = [_0x4a2b[3],_0x4a2b[4],_0x4a2b[5],_0x4a2b[6],_0x4a2b[7],_0x4a2b[8],_0x4a2b[9],_0x4a2b[10],_0x4a2b[11],_0x4a2b[12],_0x4a2b[13],_0x4a2b[14],_0x4a2b[15],_0x4a2b[16],_0x4a2b[17]];
        
        let messages = [];
        let userProfile = getUserProfile();
        let pendingAttachments = [];
        let _0x3f1d = localStorage.getItem(atob('YmFubmVkVXNlcnM=')) ? JSON.parse(localStorage.getItem(atob('YmFubmVkVXNlcnM='))) : [];
        
        function getUserProfile() {
            let profile = localStorage.getItem('userProfile');
            if (profile) {
                return JSON.parse(profile);
            }
            
            const shape = shapes[Math.floor(Math.random() * shapes.length)];
            const name = names[Math.floor(Math.random() * names.length)];
            const userId = 'user_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
            
            profile = {
                userId: userId,
                name: name,
                shape: shape.type,
                color: shape.color
            };
            
            localStorage.setItem('userProfile', JSON.stringify(profile));
            return profile;
        }
        
        function createAvatar(shape, color) {
            if (shape === 'square') {
                return `<svg width="24" height="24" viewBox="0 0 24 24">
                    <rect x="6" y="6" width="12" height="12" fill="${color}" />
                </svg>`;
            } else {
                return `<svg width="24" height="24" viewBox="0 0 24 24">
                    <polygon points="12,5 20,19 4,19" fill="${color}" />
                </svg>`;
            }
        }
        
        window.addEventListener('load', () => {
            _0x2b4c();
            loadMessages();
            startMessageChecker();
            
            document.getElementById('messageInput').addEventListener('keypress', (e) => {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage();
                }
            });

            document.getElementById('fileInput').addEventListener('change', handleFileSelect);
        });

        function _0x2b4c() {
            if (_0x3f1d.includes(userProfile.userId)) {
                document.getElementById('banOverlay').classList.add('show');
                document.getElementById('messageInput').disabled = true;
                document.getElementById('sendButton').disabled = true;
                return true;
            }
            return false;
        }
        
        function loadMessages() {
            const saved = localStorage.getItem('testRoomMessages');
            if (saved) {
                messages = JSON.parse(saved).map(m => ({
                    ...m,
                    timestamp: new Date(m.timestamp)
                }));
                cleanExpiredMessages();
                displayMessages();
            }
        }
        
        function saveMessages() {
            localStorage.setItem('testRoomMessages', JSON.stringify(messages));
        }
        
        function sendMessage() {
            if (_0x2b4c()) return;
            
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            
            if (text.length > 300) {
                showError('메시지가 너무 깁니다 (최대 300자)');
                return;
            }
            
            // !Ban 명령어 체크
            if (text.toLowerCase().startsWith('!ban ')) {
                const targetName = text.substring(5).trim();
                const target = messages.find(m => m.name === targetName);
                
                if (target) {
                    _0x3f1d.push(target.userId);
                    localStorage.setItem('bannedUsers', JSON.stringify(_0x3f1d));
                    
                    const message = {
                        id: Date.now() + '_' + Math.random().toString(36).substr(2, 9),
                        userId: userProfile.userId,
                        name: userProfile.name,
                        shape: userProfile.shape,
                        color: userProfile.color,
                        text: '🚫 ' + targetName + ' has been banned',
                        timestamp: new Date(),
                        isCommand: true
                    };
                    
                    messages.push(message);
                    saveMessages();
                    displayMessages();
                    showError(targetName + ' has been banned');
                } else {
                    showError('User not found: ' + targetName);
                }
                
                input.value = '';
                return;
            }
            
            // !CANCEL ALL 명령어 체크
            if (text === '!CANCEL ALL' || text === '!cancel all') {
                messages = [];
                localStorage.removeItem('testRoomMessages');
                displayMessages();
                showError('All messages have been cleared');
                input.value = '';
                return;
            }
            
            if (!text && pendingAttachments.length === 0) return;
            
            const message = {
                id: Date.now() + '_' + Math.random().toString(36).substr(2, 9),
                userId: userProfile.userId,
                name: userProfile.name,
                shape: userProfile.shape,
                color: userProfile.color,
                text: text,
                attachments: [...pendingAttachments],
                timestamp: new Date()
            };
            
            messages.push(message);
            saveMessages();
            displayMessages();
            
            input.value = '';
            pendingAttachments = [];
            updateAttachmentPreview();
            playSound();
            
            const container = document.getElementById('messages');
            setTimeout(() => {
                container.scrollTop = container.scrollHeight;
            }, 100);
        }

        function handleFileSelect(e) {
            const files = Array.from(e.target.files);
            
            files.forEach(file => {
                if (file.size > 5 * 1024 * 1024) {
                    showError('파일 크기는 5MB를 초과할 수 없습니다: ' + file.name);
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = (event) => {
                    const attachment = {
                        id: Date.now() + '_' + Math.random().toString(36).substr(2, 9),
                        name: file.name,
                        type: file.type,
                        data: event.target.result,
                        isImage: file.type.startsWith('image/')
                    };
                    pendingAttachments.push(attachment);
                    updateAttachmentPreview();
                };
                reader.readAsDataURL(file);
            });
            
            e.target.value = '';
        }

        function updateAttachmentPreview() {
            const previewArea = document.getElementById('attachmentPreview');
            const previewList = document.getElementById('attachmentList');
            
            if (pendingAttachments.length === 0) {
                previewArea.classList.remove('show');
                return;
            }
            
            previewArea.classList.add('show');
            previewList.innerHTML = '';
            
            pendingAttachments.forEach(att => {
                const item = document.createElement('div');
                item.className = 'attachment-preview-item';
                
                if (att.isImage) {
                    item.innerHTML = `
                        <img src="${att.data}" alt="${att.name}">
                        <span class="attachment-preview-name">${escapeHtml(att.name)}</span>
                        <button class="attachment-remove" onclick="removeAttachment('${att.id}')">×</button>
                    `;
                } else {
                    item.innerHTML = `
                        <span>📎</span>
                        <span class="attachment-preview-name">${escapeHtml(att.name)}</span>
                        <button class="attachment-remove" onclick="removeAttachment('${att.id}')">×</button>
                    `;
                }
                
                previewList.appendChild(item);
            });
        }

        function removeAttachment(id) {
            pendingAttachments = pendingAttachments.filter(att => att.id !== id);
            updateAttachmentPreview();
        }

        function showError(message) {
            const errorDiv = document.createElement('div');
            errorDiv.className = 'error-notice';
            errorDiv.textContent = message;
            document.body.appendChild(errorDiv);
            
            setTimeout(() => {
                errorDiv.remove();
            }, 3000);
        }
        
        function playSound() {
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.frequency.value = 800;
            oscillator.type = 'sine';
            
            gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.1);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + 0.1);
        }
        
        function displayMessages() {
            const container = document.getElementById('messages');
            const now = new Date();
            
            if (messages.length === 0) {
                container.innerHTML = '<div class="empty-state">No messages yet. Start the conversation.</div>';
                return;
            }
            
            container.innerHTML = '';
            
            messages.forEach(msg => {
                const timeDiff = (now - new Date(msg.timestamp)) / 1000 / 60;
                const isPrivate = timeDiff >= 30 && msg.userId === userProfile.userId;
                const isOwn = msg.userId === userProfile.userId;
                
                if (timeDiff >= 30 && !isOwn) return;
                
                const div = document.createElement('div');
                div.className = 'message-group' + (isPrivate ? ' private' : '');
                
                const displayText = msg.isCommand ? msg.text : escapeHtml(msg.text);
                const attachmentsHtml = msg.attachments && msg.attachments.length > 0 ? msg.attachments.map(att => {
                    if (att.isImage) {
                        return `<img src="${att.data}" class="attachment-image" onclick="window.open('${att.data}')" alt="${att.name}">`;
                    } else {
                        return `<div class="attachment" onclick="downloadAttachment('${att.data}', '${escapeHtml(att.name)}')">📎 ${escapeHtml(att.name)}</div>`;
                    }
                }).join('') : '';
                
                div.innerHTML = `
                    <div class="avatar">
                        ${createAvatar(msg.shape, msg.color)}
                    </div>
                    <div class="message-content-wrapper">
                        <div class="message-header">
                            <span class="username">${escapeHtml(msg.name)}</span>
                            <span class="timestamp">${formatTime(msg.timestamp)}</span>
                        </div>
                        <div class="message-bubble">
                            ${displayText}
                            ${attachmentsHtml}
                        </div>
                        ${isPrivate ? '<div class="private-notice">Only visible to you</div>' : ''}
                    </div>
                `;
                
                container.appendChild(div);
            });
        }

        function downloadAttachment(data, filename) {
            const a = document.createElement('a');
            a.href = data;
            a.download = filename;
            a.click();
        }

        function openMediaModal() {
            const modal = document.getElementById('mediaModal');
            const grid = document.getElementById('mediaGrid');
            
            grid.innerHTML = '';
            
            const allAttachments = [];
            messages.forEach(msg => {
                if (msg.attachments && msg.attachments.length > 0) {
                    msg.attachments.forEach(att => {
                        allAttachments.push({
                            ...att,
                            messageName: msg.name,
                            messageTime: msg.timestamp
                        });
                    });
                }
            });
            
            if (allAttachments.length === 0) {
                grid.innerHTML = '<div class="empty-state">No media or files yet</div>';
            } else {
                allAttachments.reverse().forEach(att => {
                    const item = document.createElement('div');
                    item.className = 'media-item';
                    
                    if (att.isImage) {
                        item.innerHTML = `
                            <img src="${att.data}" alt="${att.name}" onclick="window.open('${att.data}')">
                            <div class="media-item-name">${escapeHtml(att.name)}</div>
                        `;
                    } else {
                        item.innerHTML = `
                            <div class="media-item-file" onclick="downloadAttachment('${att.data}', '${escapeHtml(att.name)}')">
                                <span>📎</span>
                                <div style="font-size: 0.85em; color: #ffffff;">${escapeHtml(att.name)}</div>
                            </div>
                            <div class="media-item-name">Click to download</div>
                        `;
                    }
                    
                    grid.appendChild(item);
                });
            }
            
            modal.classList.add('show');
        }

        function closeMediaModal() {
            document.getElementById('mediaModal').classList.remove('show');
        }

        function cleanExpiredMessages() {
            const now = new Date();
            messages = messages.filter(msg => {
                const timeDiff = (now - new Date(msg.timestamp)) / 1000 / 60;
                return timeDiff < 60;
            });
            saveMessages();
        }

        function startMessageChecker() {
            setInterval(() => {
                cleanExpiredMessages();
                displayMessages();
            }, 60000);
        }

        function formatTime(timestamp) {
            const date = new Date(timestamp);
            const hours = date.getHours().toString().padStart(2, '0');
            const minutes = date.getMinutes().toString().padStart(2, '0');
            return `${hours}:${minutes}`;
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // Close modal when clicking outside
        document.getElementById('mediaModal').addEventListener('click', (e) => {
            if (e.target.id === 'mediaModal') {
                closeMediaModal();
            }
        });
    </script>
</body>
</html>
