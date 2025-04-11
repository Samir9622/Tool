<div class="navigation">
  <a href="/Tools">Home</a> | 
  <a href="/index.html-2">Tool Version 1</a> | 
  <a href="/Tools-index.html-2">Tool Version 2</a>
</div><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Compression Tool | Reduce Image Size</title>
    <link rel="stylesheet" href="styles.css">
    <!-- CompressorJS library for actual image compression -->
    <script src="https://cdn.jsdelivr.net/npm/compressorjs@1.1.1/dist/compressor.min.js"></script>
    <!-- Main script with defer attribute to ensure it loads after HTML -->
    <script src="script.js" defer></script>
</head>
<body>
    <header>
        <div class="container">
            <nav>
                <a href="/" class="logo">Image Tools</a>
                <ul>
                    <li><a href="https://samir9622.github.io/Index.html">Home</a></li>
                    <li><a href="https://samir9622.github.io/Tools/" class="active">Tools</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <main class="container">
        <section class="hero">
            <h1>Image Compression Tool</h1>
            <p>Reduce image size without losing quality</p>
        </section>

        <section class="tool-section">
            <h2>Compress Your Images</h2>
            
            <div id="drop-area" class="drop-area">
                <div class="drop-icon">
                    <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
                        <polyline points="17 8 12 3 7 8"></polyline>
                        <line x1="12" y1="3" x2="12" y2="15"></line>
                    </svg>
                </div>
                <p>Drag & Drop Your Images Here</p>
                <p class="or-divider">Or</p>
                <button id="select-files-btn" class="btn primary">Select Files</button>
            </div>
            
            <div id="file-preview" class="file-preview hidden">
                <h3>Selected Images (<span id="file-count">0</span>)</h3>
                <div id="preview-container" class="preview-container"></div>
                <button id="clear-btn" class="btn secondary">Clear Selection</button>
            </div>

            <div class="compression-settings">
                <h3>Compression Settings</h3>
                
                <div class="setting-group">
                    <label for="compression-level">Compression Level: <span id="level-value">80%</span></label>
                    <div class="slider-container">
                        <input type="range" id="compression-level" min="0" max="100" value="80">
                        <div class="range-labels">
                            <span>Higher Quality</span>
                            <span>Smaller Size</span>
                        </div>
                    </div>
                </div>
                
                <div class="setting-group">
                    <label for="output-format">Output Format</label>
                    <select id="output-format" class="select-box">
                        <option value="jpeg">JPEG</option>
                        <option value="png">PNG</option>
                        <option value="webp">WebP</option>
                    </select>
                </div>
                
                <div class="setting-group checkbox">
                    <input type="checkbox" id="maintain-dimensions" checked>
                    <label for="maintain-dimensions">Maintain original dimensions</label>
                </div>
                
                <button id="compress-images-btn" class="btn primary large" disabled>Compress Images</button>
            </div>
        </section>
        
        <section class="results-section">
            <div id="compression-results" class="compression-results hidden">
                <h3>Compression Results</h3>
                <div id="results-container" class="results-container"></div>
                <button id="download-all-btn" class="btn primary">Download All</button>
            </div>
        </section>
        
        <section class="features">
            <div class="feature-card">
                <h3>Fast Processing</h3>
                <p>Our tool compresses your images in seconds using advanced algorithms to reduce file size without noticeable quality loss.</p>
            </div>
            <div class="feature-card">
                <h3>Secure & Private</h3>
                <p>All image processing happens in your browser. Your files never leave your device, ensuring complete privacy.</p>
            </div>
            <div class="feature-card">
                <h3>100% Free</h3>
                <p>No watermarks, no registration, no hidden fees. Compress as many images as you want, completely free.</p>
            </div>
        </section>
    </main>

    <footer>
        <div class="container">
            <p>&copy; 2025 Image Tools. All rights reserved.</p>
        </div>
    </footer>

    <!-- Loading spinner overlay -->
    <div id="loading-overlay" class="loading-overlay hidden">
        <div class="spinner"></div>
        <p>Processing images...</p>
    </div>
</body>
</html>
/* Base Styles */
:root {
    --primary-color: #3f51b5;
    --primary-dark: #303f9f;
    --primary-light: #7986cb;
    --secondary-color: #ff4081;
    --text-color: #333;
    --text-light: #666;
    --background-color: #f8f9fa;
    --card-background: #ffffff;
    --border-color: #e0e0e0;
    --success-color: #4caf50;
    --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    --border-radius: 8px;
    --transition: all 0.3s ease;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    line-height: 1.6;
    color: var(--text-color);
    background-color: var(--background-color);
}

.container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Header & Navigation */
header {
    background-color: var(--card-background);
    box-shadow: var(--shadow);
    position: sticky;
    top: 0;
    z-index: 100;
}

nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 0;
}

.logo {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--primary-color);
    text-decoration: none;
}

nav ul {
    display: flex;
    list-style: none;
}

nav ul li {
    margin-left: 20px;
}

nav ul li a {
    text-decoration: none;
    color: var(--text-color);
    transition: var(--transition);
    padding: 5px 10px;
    border-radius: 4px;
}

nav ul li a:hover,
nav ul li a.active {
    color: var(--primary-color);
    background-color: rgba(63, 81, 181, 0.1);
}

/* Main Content */
main {
    padding: 40px 0;
}

section {
    margin-bottom: 40px;
}

.hero {
    text-align: center;
    margin-bottom: 40px;
}

.hero h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    color: var(--primary-color);
}

.hero p {
    font-size: 1.2rem;
    color: var(--text-light);
}

/* Tool Section */
.tool-section {
    background-color: var(--card-background);
    border-radius: var(--border-radius);
    box-shadow: var(--shadow);
    padding: 30px;
    margin-bottom: 40px;
}

.tool-section h2 {
    text-align: center;
    margin-bottom: 30px;
    color: var(--primary-color);
}

/* Drop Area */
.drop-area {
    border: 2px dashed var(--primary-color);
    border-radius: var(--border-radius);
    padding: 40px;
    text-align: center;
    margin-bottom: 30px;
    transition: var(--transition);
    cursor: pointer;
}

.drop-area:hover {
    background-color: rgba(63, 81, 181, 0.05);
}

.drop-area.highlight {
    border-color: var(--success-color);
    background-color: rgba(76, 175, 80, 0.1);
}

.drop-icon {
    margin-bottom: 15px;
    color: var(--primary-color);
}

.or-divider {
    margin: 15px 0;
    color: var(--text-light);
    position: relative;
}

.or-divider:before,
.or-divider:after {
    content: "";
    display: inline-block;
    width: 40px;
    height: 1px;
    background-color: var(--border-color);
    margin: 0 10px;
    vertical-align: middle;
}

/* Buttons */
.btn {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 500;
    transition: var(--transition);
}

.btn.primary {
    background-color: var(--primary-color);
    color: white;
}

.btn.primary:hover {
    background-color: var(--primary-dark);
}

.btn.secondary {
    background-color: #f0f0f0;
    color: var(--text-color);
}

.btn.secondary:hover {
    background-color: #e0e0e0;
}

.btn.large {
    padding: 12px 24px;
    font-size: 1.1rem;
}

.btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

/* File Preview */
.file-preview {
    margin-bottom: 30px;
}

.file-preview h3 {
    margin-bottom: 15px;
}

.preview-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 15px;
    margin-bottom: 20px;
}

.preview-item {
    position: relative;
    border-radius: var(--border-radius);
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.preview-item img {
    width: 100%;
    height: 150px;
    object-fit: cover;
    display: block;
}

.preview-item .file-info {
    padding: 8px;
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
    font-size: 0.8rem;
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
}

.preview-item .remove-btn {
    position: absolute;
    top: 5px;
    right: 5px;
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
    border: none;
    border-radius: 50%;
    width: 24px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 14px;
}

/* Compression Settings */
.compression-settings {
    background-color: #f8f9fb;
    border-radius: var(--border-radius);
    padding: 25px;
    margin-bottom: 30px;
}

.compression-settings h3 {
    margin-bottom: 20px;
    color: var(--primary-color);
}

.setting-group {
    margin-bottom: 20px;
}

.setting-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: 500;
}

.slider-container {
    position: relative;
}

input[type="range"] {
    width: 100%;
    height: 5px;
    -webkit-appearance: none;
    background: #d3d3d3;
    outline: none;
    border-radius: 5px;
}

input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    background: var(--primary-color);
    cursor: pointer;
}

.range-labels {
    display: flex;
    justify-content: space-between;
    font-size: 0.8rem;
    color: var(--text-light);
    margin-top: 5px;
}

.select-box {
    width: 100%;
    padding: 10px;
    border: 1px solid var(--border-color);
    border-radius: 4px;
    background-color: white;
    font-size: 1rem;
}

.setting-group.checkbox {
    display: flex;
    align-items: center;
}

.setting-group.checkbox input {
    margin-right: 10px;
}

/* Results Section */
.results-section {
    margin-top: 30px;
}

.compression-results {
    background-color: var(--card-background);
    border-radius: var(--border-radius);
    box-shadow: var(--shadow);
    padding: 30px;
}

.compression-results h3 {
    margin-bottom: 20px;
    color: var(--primary-color);
}

.results-container {
    margin-bottom: 20px;
}

.result-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    border-bottom: 1px solid var(--border-color);
}

.result-item:last-child {
    border-bottom: none;
}

.result-info {
    flex: 1;
}

.result-name {
    font-weight: 500;
    margin-bottom: 5px;
}

.result-stats {
    font-size: 0.9rem;
    color: var(--text-light);
}

.result-stats .savings {
    color: var(--success-color);
    font-weight: 500;
}

.result-actions {
    display: flex;
    gap: 10px;
}

/* Features Section */
.features {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    margin-top: 50px;
}

.feature-card {
    background-color: var(--card-background);
    border-radius: var(--border-radius);
    box-shadow: var(--shadow);
    padding: 25px;
    transition: var(--transition);
}

.feature-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.feature-card h3 {
    margin-bottom: 15px;
    color: var(--primary-color);
}

/* Footer */
footer {
    background-color: var(--primary-color);
    color: white;
    padding: 20px 0;
    margin-top: 50px;
}

/* Loading Overlay */
.loading-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(255, 255, 255, 0.9);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.spinner {
    border: 5px solid rgba(0, 0, 0, 0.1);
    border-top: 5px solid var(--primary-color);
    border-radius: 50%;
    width: 50px;
    height: 50px;
    animation: spin 1s linear infinite;
    margin-bottom: 15px;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* Utility Classes */
.hidden {
    display: none;
}

/* Responsive Styles */
@media (max-width: 768px) {
    .hero h1 {
        font-size: 2rem;
    }
    
    .drop-area {
        padding: 30px 15px;
    }
    
    .features {
        grid-template-columns: 1fr;
    }
}<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Compression Tool</title>
    <link rel="stylesheet" href="styles.css">
    <!-- Important: Load CompressorJS before your script -->
    <script src="https://cdn.jsdelivr.net/npm/compressorjs@1.1.1/dist/compressor.min.js"></script>
    <script src="script.js" defer></script>
</head>
<body>
    <div class="container">
        <h1>Image Compression Tool</h1>
        <p>Reduce image size without losing quality</p>
        
        <div id="drop-area">
            <p>Drag & Drop Your Images Here</p>
            <p>Or</p>
            <button id="select-files-btn">Select Files</button>
        </div>
        
        <div id="preview" class="hidden"></div>
        
        <div class="settings">
            <h3>Compression Settings</h3>
            <label>
                Compression Level: <span id="level-value">80%</span>
                <input type="range" id="compression-level" min="0" max="100" value="80">
            </label>
            <button id="compress-btn" disabled>Compress Images</button>
        </div>
        
        <div id="results" class="hidden"></div>
    </div>
    
    <div id="loading" class="hidden">Processing...</div>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

h1 {
    text-align: center;
    color: #3f51b5;
}

#drop-area {
    border: 2px dashed #3f51b5;
    border-radius: 8px;
    padding: 40px;
    text-align: center;
    margin: 20px 0;
    cursor: pointer;
}

#drop-area.highlight {
    background-color: rgba(63, 81, 181, 0.1);
}

button {
    background-color: #3f51b5;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 10px 20px;
    cursor: pointer;
}

button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

.settings {
    margin: 20px 0;
    padding: 20px;
    background-color: #f5f5f5;
    border-radius: 8px;
}

.preview-item {
    display: inline-block;
    margin: 10px;
    position: relative;
}

.preview-item img {
    max-width: 150px;
    max-height: 150px;
    border-radius: 4px;
}

.remove-btn {
    position: absolute;
    top: 5px;
    right: 5px;
    background: rgba(0,0,0,0.7);
    color: white;
    border: none;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    line-height: 20px;
    text-align: center;
    padding: 0;
}

.result-item {
    margin: 10px 0;
    padding: 10px;
    border-bottom: 1px solid #ddd;
}

#loading {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255,255,255,0.8);
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    z-index: 1000;
}

.hidden {
    display: none;
}
document.addEventListener('DOMContentLoaded', function() {
    // Elements
    const dropArea = document.getElementById('drop-area');
    const selectBtn = document.getElementById('select-files-btn');
    const previewArea = document.getElementById('preview');
    const compressionLevel = document.getElementById('compression-level');
    const levelValue = document.getElementById('level-value');
    const compressBtn = document.getElementById('compress-btn');
    const resultsArea = document.getElementById('results');
    const loadingOverlay = document.getElementById('loading');
    
    // Create hidden file input
    const fileInput = document.createElement('input');
    fileInput.type = 'file';
    fileInput.multiple = true;
    fileInput.accept = 'image/*';
    fileInput.style.display = 'none';
    document.body.appendChild(fileInput);
    
    // State
    let selectedFiles = [];
    
    // Event listeners
    compressionLevel.addEventListener('input', function() {
        levelValue.textContent = this.value + '%';
    });
    
    // Drag and drop
    ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(event => {
        dropArea.addEventListener(event, preventDefaults, false);
    });
    
    function preventDefaults(e) {
        e.preventDefault();
        e.stopPropagation();
    }
    
    ['dragenter', 'dragover'].forEach(event => {
        dropArea.addEventListener(event, () => dropArea.classList.add('highlight'));
    });
    
    ['dragleave', 'drop'].forEach(event => {
        dropArea.addEventListener(event, () => dropArea.classList.remove('highlight'));
    });
    
    dropArea.addEventListener('drop', function(e) {
        handleFiles(e.dataTransfer.files);
    });
    
    // File selection
    selectBtn.addEventListener('click', () => fileInput.click());
    
    fileInput.addEventListener('change', function() {
        if (this.files.length > 0) {
            handleFiles(this.files);
        }
    });
    
    // Process files
    function handleFiles(files) {
        selectedFiles = Array.from(files).filter(file => file.type.startsWith('image/'));
        
        if (selectedFiles.length === 0) {
            alert('Please select valid image files.');
            return;
        }
        
        updatePreview();
        compressBtn.disabled = false;
    }
    
    function updatePreview() {
        previewArea.innerHTML = '';
        previewArea.classList.remove('hidden');
        
        selectedFiles.forEach((file, index) => {
            const reader = new FileReader();
            
            reader.onload = function(e) {
                const previewItem = document.createElement('div');
                previewItem.className = 'preview-item';
                
                const img = document.createElement('img');
                img.src = e.target.result;
                img.alt = file.name;
                
                const removeBtn = document.createElement('button');
                removeBtn.className = 'remove-btn';
                removeBtn.textContent = '×';
                removeBtn.onclick = function() {
                    selectedFiles.splice(index, 1);
                    updatePreview();
                    if (selectedFiles.length === 0) {
                        compressBtn.disabled = true;
                    }
                };
                
                previewItem.appendChild(img);
                previewItem.appendChild(removeBtn);
                previewArea.appendChild(previewItem);
            };
            
            reader.readAsDataURL(file);
        });
    }
    
    // Compression
    compressBtn.addEventListener('click', function() {
        if (selectedFiles.length === 0) return;
        
        loadingOverlay.classList.remove('hidden');
        resultsArea.innerHTML = '';
        resultsArea.classList.add('hidden');
        
        const quality = compressionLevel.value / 100;
        let processedCount = 0;
        const results = [];
        
        selectedFiles.forEach(file => {
            // Check if Compressor is available
            if (typeof Compressor !== 'function') {
                alert('Compression library not loaded. Please check your internet connection and try again.');
                loadingOverlay.classList.add('hidden');
                return;
            }
            
            new Compressor(file, {
                quality: quality,
                success(compressedFile) {
                    results.push({
                        original: file,
                        compressed: compressedFile,
                        name: file.name,
                        originalSize: file.size,
                        compressedSize: compressedFile.size
                    });
                    
                    processedCount++;
                    if (processedCount === selectedFiles.length) {
                        displayResults(results);
                    }
                },
                error(err) {
                    console.error(err);
                    alert(`Error compressing ${file.name}: ${err.message}`);
                    
                    processedCount++;
                    if (processedCount === selectedFiles.length) {
                        displayResults(results);
                    }
                }
            });
        });
    });
    
    function displayResults(results) {
        loadingOverlay.classList.add('hidden');
        resultsArea.classList.remove('hidden');
        
        results.forEach(result => {
            const savings = ((result.originalSize - result.compressedSize) / result.originalSize * 100).toFixed(1);
            
            const resultItem = document.createElement('div');
            resultItem.className = 'result-item';
            
            const resultInfo = document.createElement('div');
            resultInfo.innerHTML = `
                <strong>${result.name}</strong><br>
                Original: ${formatFileSize(result.originalSize)} → 
                New: ${formatFileSize(result.compressedSize)}
                (${savings}% smaller)
            `;
            
            const downloadBtn = document.createElement('button');
            downloadBtn.textContent = 'Download';
            downloadBtn.onclick = function() {
                const link = document.createElement('a');
                link.href = URL.createObjectURL(result.compressed);
                link.download = `compressed_${result.name}`;
                link.click();
                URL.revokeObjectURL(link.href);
            };
            
            resultItem.appendChild(resultInfo);
            resultItem.appendChild(downloadBtn);
            resultsArea.appendChild(resultItem);
        });
    }
    
    function formatFileSize(bytes) {
        if (bytes === 0) return '0 Bytes';
        
        const k = 1024;
        const sizes = ['Bytes', 'KB', 'MB', 'GB'];
        const i = Math.floor(Math.log(bytes) / Math.log(k));
        
        return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
    }
    
    // Log initialization for debugging
    console.log('Image Compression Tool initialized');
});

https://cdn.jsdelivr.net/npm/compressorjs@1.1.1/dist/compressor.min.js
document.addEventListener('DOMContentLoaded', () => {
    // DOM Elements
    const elements = {
        dropArea: document.getElementById('drop-area'),
        selectBtn: document.getElementById('select-files-btn'),
