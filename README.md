
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>在线文本加密工具</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-gradient-to-br from-blue-50 to-purple-50 min-h-screen">
    <div class="container mx-auto px-4 py-12">
        <header class="text-center mb-12">
            <h1 class="text-4xl font-bold text-indigo-700 mb-2">文本加密工具</h1>
            <p class="text-gray-600">支持凯撒加密和AES-256加密算法</p>
        </header>

        <div class="max-w-4xl mx-auto bg-white rounded-xl shadow-lg overflow-hidden">
            <div class="p-6">
                <div class="flex mb-6 space-x-4">
                    <button id="caesarTab" class="px-4 py-2 bg-indigo-600 text-white rounded-lg font-medium transition-all hover:bg-indigo-700 active:scale-95">凯撒加密</button>
                    <button id="aesTab" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-lg font-medium transition-all hover:bg-gray-300 active:scale-95">AES加密</button>
                </div>

                <!-- 凯撒加密面板 -->
                <div id="caesarPanel" class="space-y-4">
                    <div>
                        <label class="block text-gray-700 mb-2">偏移量 (1-25)</label>
                        <input type="number" id="caesarKey" min="1" max="25" value="3" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-gray-700 mb-2">原始文本</label>
                            <textarea id="caesarPlaintext" rows="10" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" placeholder="输入要加密的文本..."></textarea>
                            <button id="caesarEncryptBtn" class="mt-2 px-4 py-2 bg-indigo-600 text-white rounded-lg font-medium transition-all hover:bg-indigo-700 active:scale-95">加密 <i class="fas fa-lock ml-1"></i></button>
                        </div>
                        <div>
                            <label class="block text-gray-700 mb-2">加密结果</label>
                            <textarea id="caesarCiphertext" rows="10" readonly class="w-full px-4 py-2 border border-gray-300 rounded-lg bg-gray-50" placeholder="加密后的文本将显示在这里..."></textarea>
                            <button id="caesarDecryptBtn" class="mt-2 px-4 py-2 bg-green-600 text-white rounded-lg font-medium transition-all hover:bg-green-700 active:scale-95">解密 <i class="fas fa-unlock ml-1"></i></button>
                        </div>
                    </div>
                </div>

                <!-- AES加密面板 -->
                <div id="aesPanel" class="space-y-4 hidden">
                    <div>
                        <label class="block text-gray-700 mb-2">加密密钥</label>
                        <input type="password" id="aesKey" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" placeholder="输入16/24/32位密钥">
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-gray-700 mb-2">原始文本</label>
                            <textarea id="aesPlaintext" rows="10" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500" placeholder="输入要加密的文本..."></textarea>
                            <button id="aesEncryptBtn" class="mt-2 px-4 py-2 bg-indigo-600 text-white rounded-lg font-medium transition-all hover:bg-indigo-700 active:scale-95">加密 <i class="fas fa-lock ml-1"></i></button>
                        </div>
                        <div>
                            <label class="block text-gray-700 mb-2">加密结果</label>
                            <textarea id="aesCiphertext" rows="10" readonly class="w-full px-4 py-2 border border-gray-300 rounded-lg bg-gray-50" placeholder="加密后的文本将显示在这里..."></textarea>
                            <button id="aesDecryptBtn" class="mt-2 px-4 py-2 bg-green-600 text-white rounded-lg font-medium transition-all hover:bg-green-700 active:scale-95">解密 <i class="fas fa-unlock ml-1"></i></button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 凯撒加密函数
        function caesarEncrypt(text, shift) {
            return text.replace(/[a-zA-Z]/g, function(c) {
                const base = c < 'a' ? 65 : 97;
                return String.fromCharCode((c.charCodeAt(0) - base + shift) %
