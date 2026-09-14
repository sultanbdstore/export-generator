<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Export Program & Transport Order Generator - Sultan (Store)</title>
    <style>
        :root {
            --bg-main: #0b0f19;
            --bg-card: #111827;
            --bg-card-sub: #0f172a;
            --bg-input: #090d16;
            --border-color: #1f2937;
            --border-focus: #10b981;
            --text-primary: #f9fafb;
            --text-secondary: #9ca3af;
            --accent-green: #10b981;
            --accent-green-hover: #059669;
            --accent-blue: #3b82f6;
            --accent-amber: #f59e0b;
            --accent-purple: #8b5cf6;
            --code-sms: #34d399;
            --code-email: #e2e8f0;
            --code-transport: #fbbf24;
            --code-air: #f43f5e;
            --radius: 12px;
            --font: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Courier New", monospace;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-primary);
            font-family: var(--font);
            font-size: 13.5px;
            line-height: 1.5;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            background-color: var(--bg-card);
            border-bottom: 1px solid var(--border-color);
            padding: 14px 28px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 50;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
        }

        .brand-title {
            display: flex;
            align-items: center;
            gap: 14px;
        }

        .brand-icon {
            background: linear-gradient(135deg, #10b981, #0284c7);
            color: white;
            padding: 10px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            box-shadow: 0 2px 8px rgba(16, 185, 129, 0.4);
        }

        .brand-text h1 {
            font-size: 17px;
            font-weight: 700;
            color: #ffffff;
        }

        .brand-text p {
            font-size: 11px;
            color: var(--text-secondary);
        }

        .header-actions {
            display: flex;
            gap: 10px;
        }

        .btn {
            background-color: var(--border-color);
            color: var(--text-primary);
            border: 1px solid transparent;
            padding: 8px 16px;
            border-radius: 8px;
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .btn:hover {
            opacity: 0.95;
            transform: translateY(-1px);
        }

        .btn-primary { background-color: var(--accent-blue); color: white; }
        .btn-success { background-color: var(--accent-green); color: white; }
        .btn-amber { background-color: var(--accent-amber); color: #0f172a; }
        .btn-purple { background-color: var(--accent-purple); color: white; }
        .btn-danger { background-color: #ef4444; color: white; }
        .btn-outline { background-color: transparent; border-color: var(--border-color); color: var(--text-secondary); }

        main {
            flex: 1;
            padding: 22px;
            max-width: 1750px;
            width: 100%;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 22px;
        }

        @media (max-width: 1200px) {
            main { grid-template-columns: 1fr; }
        }

        .card {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius);
            padding: 18px;
            display: flex;
            flex-direction: column;
            gap: 14px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.25);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 10px;
        }

        .card-title {
            font-size: 13px;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: #e2e8f0;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .badge {
            font-size: 10px;
            padding: 2px 8px;
            border-radius: 6px;
            background: rgba(16, 185, 129, 0.15);
            color: var(--accent-green);
            border: 1px solid rgba(16, 185, 129, 0.3);
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
            gap: 12px;
        }

        label {
            font-size: 11px;
            font-weight: 600;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 0.2px;
        }

        input, textarea, select {
            background-color: var(--bg-input);
            border: 1px solid var(--border-color);
            color: var(--text-primary);
            padding: 9px 12px;
            border-radius: 8px;
            font-size: 12.5px;
            font-family: inherit;
            outline: none;
            transition: all 0.2s ease;
            width: 100%;
        }

        input:focus, textarea:focus, select:focus {
            border-color: var(--border-focus);
            box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.15);
        }

        textarea { resize: vertical; }

        .output-box {
            position: relative;
            background-color: var(--bg-card-sub);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 14px;
            font-family: var(--mono);
            font-size: 12px;
            line-height: 1.65;
            white-space: pre-wrap;
            word-break: break-word;
            min-height: 80px;
            user-select: all;
        }

        .output-box.sms { color: var(--code-sms); }
        .output-box.transport { color: var(--code-transport); }
        .output-box.email { color: var(--code-email); font-family: var(--font); }
        .output-box.air { color: var(--code-air); }

        .chat-green-link {
            color: #059669 !important;
            font-weight: 700 !important;
            text-decoration: underline !important;
            background: rgba(16, 185, 129, 0.15);
            padding: 2px 8px;
            border-radius: 4px;
            border: 1px solid rgba(16, 185, 129, 0.3);
            transition: all 0.2s ease;
            display: inline-block;
        }

        .chat-green-link:hover {
            background: rgba(16, 185, 129, 0.3);
            color: #10b981 !important;
        }

        #toast {
            position: fixed;
            bottom: 24px;
            right: 24px;
            background-color: var(--accent-green);
            color: white;
            padding: 12px 22px;
            border-radius: 10px;
            font-size: 13px;
            font-weight: 600;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.6);
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            z-index: 100;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        #toast.show {
            transform: translateY(0);
            opacity: 1;
        }

        .fleet-badge-info {
            background: rgba(16, 185, 129, 0.08);
            border: 1px solid rgba(16, 185, 129, 0.25);
            color: #34d399;
            padding: 10px 14px;
            border-radius: 8px;
            font-size: 11.5px;
            line-height: 1.6;
        }

        /* Modal Settings */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0,0,0,0.75);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 200;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.2s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius);
            width: 90%;
            max-width: 550px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 16px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 10px;
        }

        .modal-header h2 {
            font-size: 15px;
            color: var(--text-primary);
        }

        .close-btn {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 18px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <header>
        <div class="brand-title">
            <div class="brand-icon">🚚</div>
            <div class="brand-text">
                <h1>Export Program & Transport Order Generator</h1>
                <p>Tailored for Sultan Sir (Store Dept) • CBM Feet Engine & Transporter Requisitions</p>
            </div>
        </div>
        <div class="header-actions">
            <button class="btn btn-amber" onclick="loadSampleData('sea')">⚡ Load Sea Sample</button>
            <button class="btn btn-purple" onclick="loadSampleData('air')">✈️ Load Air Sample</button>
            <button class="btn btn-outline" onclick="openSettings()">⚙️ Settings</button>
            <button class="btn btn-danger" onclick="resetForm()">🔄 Reset All</button>
        </div>
    </header>

    <main>
        <!-- LEFT COLUMN: Email Input & Parameters -->
        <div style="display: flex; flex-direction: column; gap: 20px;">
            
            <div class="card">
                <div class="card-header">
                    <div class="card-title">
                        <span>📥</span> 1. Paste Daily Shipment Email
                    </div>
                    <span id="parse-status" class="badge">Ready to Parse</span>
                </div>
                <div class="form-group">
                    <textarea id="raw-email" rows="8" placeholder="Paste full email from Sohan / Merchandising team here..."></textarea>
                </div>
                <button class="btn btn-primary" onclick="parseEmail()">
                    <span>✨</span> Auto-Extract & Calculate Fleet
                </button>
            </div>

            <div class="card">
                <div class="card-header">
                    <div class="card-title">
                        <span>⚙️</span> 2. Verified Shipment Parameters
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="f-recipient">Sender / Recipient</label>
                        <input type="text" id="f-recipient" oninput="updateOutputs()" placeholder="Md.Sohan Hossen">
                    </div>
                    <div class="form-group">
                        <label for="f-buyer">Buyer Name</label>
                        <input type="text" id="f-buyer" oninput="updateOutputs()" placeholder="TJX / Primark">
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="f-exfactory">Ex-Factory Date</label>
                        <input type="text" id="f-exfactory" oninput="updateOutputs()" placeholder="13-Sep-2026">
                    </div>
                    <div class="form-group">
                        <label for="f-handover">Hand Over Date</label>
                        <input type="text" id="f-handover" oninput="updateOutputs()" placeholder="14-Sep-2026">
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="f-depot">Depot</label>
                        <input type="text" id="f-depot" oninput="checkDepotAir(); updateOutputs();" placeholder="OCL / KDS / All Port ( Kamarpara-Tungi )">
                    </div>
                    <div class="form-group">
                        <label for="f-totalcbm">Total Volume (CBM)</label>
                        <input type="text" id="f-totalcbm" oninput="recalculateFleet(); updateOutputs();" placeholder="11.01 CBM">
                    </div>
                </div>

                <div class="fleet-badge-info">
                    📐 <strong>CBM to Feet Conversion Engine:</strong><br>
                    • 01 – 05 CBM = <strong>08 Feet</strong> Covered Van (Small)<br>
                    • 05.01 – 10 CBM = <strong>14 Feet</strong> Covered Van (Small)<br>
                    • 10.01 – 15 CBM = <strong>18 Feet</strong> Covered Van (Small)<br>
                    • 15.01 – 30 CBM = <strong>23 Feet</strong> Covered Van (Big - Shahjoki ~27 CBM target)
                </div>

                <div class="form-group">
                    <label for="f-erpbreakdown">ERP Breakdown (Line by line)</label>
                    <textarea id="f-erpbreakdown" rows="4" oninput="calculateCbmFromErp(); updateOutputs();" placeholder="294 = 5.69 CBM&#10;296 = 5.32 CBM"></textarea>
                </div>

                <div style="background: rgba(16, 185, 129, 0.05); border: 1px solid rgba(16, 185, 129, 0.2); padding: 12px; border-radius: 8px; display: flex; flex-direction: column; gap: 10px;">
                    <div style="display: flex; justify-content: space-between; align-items: center;">
                        <label style="color: #34d399; font-weight: 700;">🚛 Transporter Selection & Fleet Count</label>
                        <span class="badge" id="fleet-summary-badge">Small (18 Feet)</span>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="f-smalltransporter">Small Cargo Transporter</label>
                            <select id="f-smalltransporter" onchange="updateOutputs()">
                                <option value="New JS">New JS</option>
                                <option value="Shahjoki">Shahjoki</option>
                                <option value="AFL Own Cargo">AFL Own Cargo</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="f-smallcargocount">Small Cargo Count</label>
                            <input type="number" id="f-smallcargocount" min="0" value="1" oninput="updateOutputs()">
                        </div>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="f-bigtransporter">Big Cargo Transporter</label>
                            <select id="f-bigtransporter" onchange="updateOutputs()">
                                <option value="Shahjoki">Shahjoki</option>
                                <option value="New JS">New JS</option>
                                <option value="AFL Own Cargo">AFL Own Cargo</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="f-bigcargocount">Big Cargo Count</label>
                            <input type="number" id="f-bigcargocount" min="0" value="0" oninput="updateOutputs()">
                        </div>
                    </div>
                </div>

                <!-- AIR EXPORT EXTRA VEHICLE & DRIVER FIELDS -->
                <div style="background: rgba(244, 63, 94, 0.08); border: 1px solid rgba(244, 63, 94, 0.2); padding: 12px; border-radius: 8px; display: flex; flex-direction: column; gap: 10px;">
                    <label style="color: #f43f5e; font-weight: 700;">✈️ Air Export Details (Vehicle & Driver)</label>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="f-airtransporter">Air Cargo Source</label>
                            <select id="f-airtransporter" onchange="updateOutputs()">
                                <option value="AFL Own Cargo">AFL Own Cargo</option>
                                <option value="New JS">New JS</option>
                                <option value="Shahjoki">Shahjoki</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="f-van-no">Covered Van No.</label>
                            <input type="text" id="f-van-no" oninput="updateOutputs()" placeholder="11-3260">
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label for="f-driver-name">Driver Name</label>
                            <input type="text" id="f-driver-name" oninput="updateOutputs()" placeholder="Mr. Anwar">
                        </div>
                        <div class="form-group">
                            <label for="f-driver-contact">Driver Contact</label>
                            <input type="text" id="f-driver-contact" oninput="updateOutputs()" placeholder="01939-385175">
                        </div>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="f-merchandiser">Merchandiser</label>
                        <input type="text" id="f-merchandiser" oninput="updateOutputs()" placeholder="Mr. Salim Miah">
                    </div>
                    <div class="form-group">
                        <label for="f-commercial">Commercial</label>
                        <input type="text" id="f-commercial" oninput="updateOutputs()" placeholder="Mr. Rezul Karim">
                    </div>
                </div>

                <div class="form-group">
                    <label for="f-chatlink" style="color:#34d399;">🟢 Google Chat Room URL</label>
                    <input type="text" id="f-chatlink" oninput="updateOutputs()" value="https://chat.google.com/room/AAQAgt7BBAo?cls=7">
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="f-signature">My Signature</label>
                        <input type="text" id="f-signature" oninput="updateOutputs()" value="ѕυℓтαη">
                    </div>
                    <div class="form-group" style="display: flex; align-items: center; gap: 8px; margin-top: 18px;">
                        <input type="checkbox" id="f-isair" onchange="updateOutputs()" style="width: auto;">
                        <label for="f-isair" style="cursor: pointer; text-transform: none;">Force Air Export Format</label>
                    </div>
                </div>

            </div>
        </div>

        <!-- RIGHT COLUMN: Generated Output Cards -->
        <div style="display: flex; flex-direction: column; gap: 20px;">
            
            <!-- Output 1: Main Store Google Chat / SMS Format -->
            <div class="card" id="sea-sms-card">
                <div class="card-header">
                    <div class="card-title">
                        <span>📱</span> 1. Main Store Google Chat / SMS Format
                    </div>
                    <button class="btn btn-success" onclick="copyOutput('out-sms', 'Google Chat SMS copied!')">
                        📋 Copy Store SMS
                    </button>
                </div>
                <div id="out-sms" class="output-box sms"></div>
            </div>

            <!-- Output 2: SEPARATED TRANSPORTER SMS REQUISITIONS (NO CBM DETAILS) -->
            <div id="separated-transporter-container" style="display: flex; flex-direction: column; gap: 20px;"></div>

            <!-- Output 3: Email Reply Format (Rich Text Hyperlink) -->
            <div class="card">
                <div class="card-header">
                    <div class="card-title">
                        <span>✉️</span> 3. Professional Email Reply Format
                    </div>
                    <div style="display:flex; gap:8px;">
                        <button class="btn btn-success" onclick="copyRichTextEmail()">
                            📧 Copy Rich Text (Gmail/Outlook)
                        </button>
                        <button class="btn btn-primary" onclick="copyOutput('out-email-text', 'Plain text copied!')">
                            📋 Copy Plain Text
                        </button>
                    </div>
                </div>
                <div id="out-email-html" class="output-box email"></div>
                <div id="out-email-text" style="display:none;"></div>
            </div>

            <!-- Output 4: AIR EXPORT SPECIAL FORMAT (POSITIONED AT BOTTOM RIGHT) -->
            <div class="card" id="air-card" style="display: none;">
                <div class="card-header">
                    <div class="card-title">
                        <span>✈️</span> 4. Air Export SMS Format <span id="air-badge" class="badge" style="background:#f43f5e; color:white;">AIR PROGRAM ACTIVE</span>
                    </div>
                    <button class="btn btn-purple" onclick="copyOutput('out-air', 'Air Export SMS copied!')">
                        📋 Copy Air SMS
                    </button>
                </div>
                <div id="out-air" class="output-box air"></div>
            </div>

        </div>
    </main>

    <!-- Modal for Settings -->
    <div class="modal-overlay" id="settings-modal">
        <div class="modal">
            <div class="modal-header">
                <h2>⚙️ Application Settings</h2>
                <button class="close-btn" onclick="closeSettings()">&times;</button>
            </div>
            <div class="form-group">
                <label>Default Google Chat Room Link</label>
                <input type="text" id="cfg-chatlink" value="https://chat.google.com/room/AAQAgt7BBAo?cls=7">
            </div>
            <div class="form-group">
                <label>Default Signature</label>
                <input type="text" id="cfg-signature" value="ѕυℓтαη">
            </div>
            <div style="display: flex; justify-content: flex-end; gap: 10px; margin-top: 10px;">
                <button class="btn btn-outline" onclick="closeSettings()">Cancel</button>
                <button class="btn btn-success" onclick="saveSettings()">Save Preferences</button>
            </div>
        </div>
    </div>

    <div id="toast">
        <span>✅</span>
        <span id="toast-msg">Text copied to clipboard!</span>
    </div>

    <script>
        const sampleSeaEmail = `Dear Mr.Sultan Mahamud,

Buyer : TJX 

Erp No : 294  = 5.69 Cbm
Erp No : 296  = 5.32 Cbm

Ex-Factory Date: 13/09/2026               
Hand Over Date: 14/09/2026

Deport :  OCL
Total  Cbm =Actual 11.01 Cbm.

Today shipment plan for TJX
Please arrange the cargo for shipment Purpose.

(As per mersent Team Mr.Salim Miah
& Commercial Mr. Rezul Karim Confirmed me)
 
Thanks 
Md.Sohan Hossen`;

        const sampleAirEmail = `Dear Mr.Sultan Mahamud,

Buyer : Tudorknight (Next)

Erp No : 181 = 0.95 Cbm

Ex-Factory Date: 13/09/2026
Hand Over Date: 13/09/2026

Deport : All Port ( Kamarpara-Tungi )
Total Cbm = Actual 0.95 Cbm.

Vehicle: 11-3260
Driver: Mr. Anwar
Contact: 01939-385175

(As per mersent Team Mr. Fuad
& Commercial Mr. Shahin Confirmed me)

Thanks
Md.Sohan Hossen`;

        window.onload = function() {
            loadSampleData('sea');
        };

        function openSettings() {
            document.getElementById('settings-modal').classList.add('active');
        }

        function closeSettings() {
            document.getElementById('settings-modal').classList.remove('active');
        }

        function saveSettings() {
            const chatLink = document.getElementById('cfg-chatlink').value;
            const signature = document.getElementById('cfg-signature').value;
            if (chatLink) document.getElementById('f-chatlink').value = chatLink;
            if (signature) document.getElementById('f-signature').value = signature;
            updateOutputs();
            closeSettings();
            showToast('Settings saved!');
        }

        function numberToWord(num) {
            const words = ["Zero", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten"];
            let n = parseInt(num, 10);
            return words[n] || (n < 10 ? '0' + n : n.toString());
        }

        function formatDateString(dateStr) {
            if (!dateStr) return '';
            dateStr = dateStr.trim();
            const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

            let match = dateStr.match(/^(\d{1,2})[\/\.-](\d{1,2})[\/\.-](\d{2,4})/);
            if (match) {
                let day = match[1].padStart(2, '0');
                let monthIdx = parseInt(match[2], 10) - 1;
                let year = match[3];
                if (year.length === 2) year = '20' + year;
                if (monthIdx >= 0 && monthIdx < 12) {
                    return `${day}-${monthNames[monthIdx]}-${year}`;
                }
            }
            return dateStr;
        }

        // CBM to Feet Converter Engine
        function getFeetSizeFromCbm(cbm) {
            const val = parseFloat(cbm) || 0;
            if (val <= 5) return "08";
            if (val <= 10) return "14";
            if (val <= 15) return "18";
            return "23";
        }

        function loadSampleData(type) {
            if (type === 'air') {
                document.getElementById('raw-email').value = sampleAirEmail;
            } else {
                document.getElementById('raw-email').value = sampleSeaEmail;
            }
            parseEmail();
            showToast(type === 'air' ? 'Air export sample loaded!' : 'Sea export sample loaded!');
        }

        function resetForm() {
            document.getElementById('raw-email').value = '';
            document.getElementById('f-recipient').value = '';
            document.getElementById('f-buyer').value = '';
            document.getElementById('f-exfactory').value = '';
            document.getElementById('f-handover').value = '';
            document.getElementById('f-depot').value = '';
            document.getElementById('f-totalcbm').value = '';
            document.getElementById('f-erpbreakdown').value = '';
            document.getElementById('f-smallcargocount').value = '1';
            document.getElementById('f-bigcargocount').value = '0';
            document.getElementById('f-merchandiser').value = '';
            document.getElementById('f-commercial').value = '';
            document.getElementById('f-isair').checked = false;
            document.getElementById('f-van-no').value = '';
            document.getElementById('f-driver-name').value = '';
            document.getElementById('f-driver-contact').value = '';

            updateOutputs();
            showToast('Form cleared');
        }

        function parseEmail() {
            const text = document.getElementById('raw-email').value;
            if (!text.trim()) {
                showToast('Please paste an email body first');
                return;
            }

            const buyerMatch = text.match(/Buyer\s*:\s*([^\n\r]+)/i);
            if (buyerMatch) document.getElementById('f-buyer').value = buyerMatch[1].trim();

            const exFacMatch = text.match(/Ex-Factory\s*Date\s*:\s*([0-9\/\.-]+)/i);
            if (exFacMatch) document.getElementById('f-exfactory').value = formatDateString(exFacMatch[1]);

            const handMatch = text.match(/Hand\s*Over\s*Date\s*:\s*([0-9\/\.-]+)/i);
            if (handMatch) document.getElementById('f-handover').value = formatDateString(handMatch[1]);

            const depotMatch = text.match(/(?:Deport|Depot)\s*:\s*([^\n\r]+)/i);
            if (depotMatch) document.getElementById('f-depot').value = depotMatch[1].trim();

            const cbmMatch = text.match(/Total\s*Cbm\s*=\s*(?:Actual\s*)?([0-9\.]+\s*(?:Cbm|CBM)?)/i);
            if (cbmMatch) {
                let cbmVal = cbmMatch[1].trim();
                if (!/cbm/i.test(cbmVal)) cbmVal += ' CBM';
                document.getElementById('f-totalcbm').value = cbmVal;
            }

            const erpLines = [];
            const erpRegex = /(?:Erp\s*No|ERP|Style)\s*:\s*([^\n\r=]+)=\s*([0-9\.]+\s*(?:Cbm|CBM)?)/gi;
            let m;
            while ((m = erpRegex.exec(text)) !== null) {
                let erpNo = m[1].trim();
                let erpCbm = m[2].trim();
                if (!/cbm/i.test(erpCbm)) erpCbm += ' CBM';
                erpLines.push(`${erpNo} = ${erpCbm}`);
            }
            if (erpLines.length > 0) {
                document.getElementById('f-erpbreakdown').value = erpLines.join('\n');
            }

            const vanMatch = text.match(/(?:Vehicle|Van|Covered Van)\s*:\s*([^\n\r]+)/i);
            if (vanMatch) document.getElementById('f-van-no').value = vanMatch[1].trim();

            const driverMatch = text.match(/Driver\s*:\s*([^\n\r]+)/i);
            if (driverMatch) document.getElementById('f-driver-name').value = driverMatch[1].trim();

            const contactMatch = text.match(/(?:Contact|Phone|Mobile)\s*:\s*([^\n\r]+)/i);
            if (contactMatch) document.getElementById('f-driver-contact').value = contactMatch[1].trim();

            const merMatch = text.match(/(?:mersent\s*Team|Merchandiser)\s*([^\&\n\r]+)/i);
            if (merMatch) document.getElementById('f-merchandiser').value = merMatch[1].replace(/Confirmed.*$/i, '').trim();

            const comMatch = text.match(/Commercial\s*([^\n\r\)]+)/i);
            if (comMatch) document.getElementById('f-commercial').value = comMatch[1].replace(/Confirmed.*$/i, '').trim();

            const senderMatch = text.match(/(?:Thanks|Regards|Best Regards)[\s\n\r]+([^\n\r]+)/i);
            document.getElementById('f-recipient').value = senderMatch ? senderMatch[1].trim() : "Md.Sohan Hossen";

            recalculateFleet();
            checkDepotAir();
            updateOutputs();
            showToast('Email parsed successfully!');
        }

        function recalculateFleet() {
            const rawCbm = document.getElementById('f-totalcbm').value;
            const cbm = parseFloat(rawCbm) || 0;
            
            let smallCount = 0;
            let bigCount = 0;
            let feetStr = getFeetSizeFromCbm(cbm);
            let badgeSummary = '';

            if (cbm > 0) {
                if (cbm <= 15) {
                    smallCount = 1;
                    bigCount = 0;
                    badgeSummary = `Small (${feetStr} Feet)`;
                } else {
                    bigCount = Math.floor(cbm / 27);
                    let remCbm = cbm % 27;

                    if (bigCount === 0 && cbm > 15) {
                        bigCount = 1;
                        remCbm = 0;
                    }

                    if (remCbm > 0) {
                        smallCount = 1;
                        badgeSummary = `Big (23 Feet: ${bigCount}) + Small (${getFeetSizeFromCbm(remCbm)} Feet: 1)`;
                    } else {
                        smallCount = 0;
                        badgeSummary = `Big (23 Feet: ${bigCount})`;
                    }
                }
            }

            document.getElementById('f-smallcargocount').value = smallCount;
            document.getElementById('f-bigcargocount').value = bigCount;
            document.getElementById('fleet-summary-badge').textContent = badgeSummary || "Small (18 Feet)";
        }

        function calculateCbmFromErp() {
            const lines = document.getElementById('f-erpbreakdown').value.split('\n');
            let total = 0;
            lines.forEach(line => {
                const parts = line.split('=');
                if (parts.length > 1) {
                    const cbm = parseFloat(parts[1]);
                    if (!isNaN(cbm)) total += cbm;
                }
            });
            if (total > 0) {
                document.getElementById('f-totalcbm').value = total.toFixed(2) + ' CBM';
                recalculateFleet();
            }
        }

        function checkDepotAir() {
            const depotVal = document.getElementById('f-depot').value.toLowerCase();
            const isAirCheckbox = document.getElementById('f-isair');

            if (depotVal.includes('air') || depotVal.includes('cfs') || depotVal.includes('kamarpara') || depotVal.includes('tungi') || depotVal.includes('dac')) {
                isAirCheckbox.checked = true;
            } else {
                isAirCheckbox.checked = false;
            }
        }

        function updateOutputs() {
            const recipient = document.getElementById('f-recipient').value || 'Md.Sohan Hossen';
            const buyer = document.getElementById('f-buyer').value || 'TJX';
            const exFactory = document.getElementById('f-exfactory').value || '13-Sep-2026';
            const handover = document.getElementById('f-handover').value || '14-Sep-2026';
            const depot = document.getElementById('f-depot').value || 'OCL';
            const totalCbm = document.getElementById('f-totalcbm').value || '11.01 CBM';
            const erpBreakdown = document.getElementById('f-erpbreakdown').value || '294 = 5.69 CBM\n296 = 5.32 CBM';
            
            const smallTrans = document.getElementById('f-smalltransporter').value || "New JS";
            const bigTrans = document.getElementById('f-bigtransporter').value || "Shahjoki";
            const airTrans = document.getElementById('f-airtransporter').value || "AFL Own Cargo";
            
            const smallCount = parseInt(document.getElementById('f-smallcargocount').value, 10) || 0;
            const bigCount = parseInt(document.getElementById('f-bigcargocount').value, 10) || 0;
            const totalCargosNum = smallCount + bigCount;
            const totalCargosStr = totalCargosNum < 10 ? `0${totalCargosNum}` : `${totalCargosNum}`;

            const vanNo = document.getElementById('f-van-no').value || '11-3260';
            const driverName = document.getElementById('f-driver-name').value || 'Mr. Anwar';
            const driverContact = document.getElementById('f-driver-contact').value || '01939-385175';

            const merchandiser = document.getElementById('f-merchandiser').value || 'Mr. Salim Miah';
            const commercial = document.getElementById('f-commercial').value || 'Mr. Rezul Karim';
            const chatLink = document.getElementById('f-chatlink').value || 'https://chat.google.com/room/AAQAgt7BBAo?cls=7';
            const signature = document.getElementById('f-signature').value || 'ѕυℓтαη';
            const isAir = document.getElementById('f-isair').checked;

            const cbmNumeric = parseFloat(totalCbm) || 0;
            const feetSize = getFeetSizeFromCbm(cbmNumeric);

            let recipientFirstName = recipient;
            if (recipient.includes('Sohan')) {
                recipientFirstName = "Mr. Sohan";
            } else if (!recipient.startsWith("Mr.")) {
                recipientFirstName = "Mr. " + recipient.split(' ')[0];
            }

            // Cargo Source Statement for Main Google Chat SMS & Email
            let cargoSourceSMS = '';
            let cargoSourceEmail = '';

            if (smallCount > 0 && bigCount > 0) {
                const smallStr = smallCount < 10 ? '0' + smallCount : smallCount;
                const bigStr = bigCount < 10 ? '0' + bigCount : bigCount;
                if (smallTrans === bigTrans) {
                    cargoSourceSMS = `🚛 ${smallTrans}: ${smallStr} Small Cargo & ${bigStr} Big Cargo`;
                    cargoSourceEmail = ` ${smallTrans}: ${smallStr} Small Cargo & ${bigStr} Big Cargo`;
                } else {
                    cargoSourceSMS = `🚛 ${smallTrans}: ${smallStr} Cargo\n🚛 ${bigTrans}: ${bigStr} Big Cargo`;
                    cargoSourceEmail = ` ${smallTrans}: ${smallStr} Cargo\n ${bigTrans}: ${bigStr} Big Cargo`;
                }
            } else if (bigCount > 0) {
                const bigStr = bigCount < 10 ? '0' + bigCount : bigCount;
                cargoSourceSMS = `🚛 ${bigTrans}: ${bigStr} Cargo`;
                cargoSourceEmail = ` ${bigTrans}: ${bigStr} Cargo`;
            } else {
                const smallStr = smallCount < 10 ? '0' + smallCount : smallCount;
                cargoSourceSMS = `🚛 ${smallTrans}: ${smallStr} Cargo`;
                cargoSourceEmail = ` ${smallTrans}: ${smallStr} Cargo`;
            }

            // 1. MAIN STORE GOOGLE CHAT / SMS FORMAT
            const smsFormat = `Export Program for Today: ${exFactory}
Hand Over Date: ${handover}
🏭 Depot: ${depot}
📦 Total Volume: ${totalCbm}
🚛 Total Cargos: ${totalCargosStr}
🛒 Buyer: ${buyer}
📋 ERP Nos.:
${erpBreakdown}
👤 Merchandiser: ${merchandiser}
👤 Commercial: ${commercial}
🔹 Cargo Source:
${cargoSourceSMS}`;

            // 2. SEPARATED TRANSPORTER REQUISITION SMS CARDS (NO CBM DETAILS)
            const sepContainer = document.getElementById('separated-transporter-container');
            sepContainer.innerHTML = '';

            const transAssignments = {};
            if (smallCount > 0) {
                if (!transAssignments[smallTrans]) transAssignments[smallTrans] = { small: 0, big: 0, feet: feetSize };
                transAssignments[smallTrans].small += smallCount;
            }
            if (bigCount > 0) {
                if (!transAssignments[bigTrans]) transAssignments[bigTrans] = { small: 0, big: 0, feet: "23" };
                transAssignments[bigTrans].big += bigCount;
            }

            let cardIndex = 2;
            for (const [transName, counts] of Object.entries(transAssignments)) {
                let msg = '';
                const sCnt = counts.small;
                const bCnt = counts.big;

                if (bCnt > 0 && sCnt === 0) {
                    const countStr = bCnt < 10 ? `0${bCnt}` : `${bCnt}`;
                    const wordStr = numberToWord(bCnt);
                    msg = `Today ( ${exFactory} ) We 𝙽𝚎𝚎𝚍 ${countStr} ( ${wordStr} ) Big (23 Feet) 𝙲𝚊𝚛𝚐𝚘 𝙵𝚘𝚛 "${depot}" 𝙳𝚎𝚙𝚘 . 𝙶𝚘𝚘𝚍𝚜 𝚁𝚎𝚊𝚍𝚢 𝙿𝚕𝚎𝚊𝚜𝚎 𝚂𝚎𝚗𝚍 𝙲𝚊𝚛𝚐𝚘 𝚄𝚛𝚐𝚎𝚗𝚝𝚕𝚢 . [ Note: Arrange GPS-enabled cargos as per our requirement.]`;
                } else if (bCnt > 0 && sCnt > 0) {
                    const bigStr = bCnt < 10 ? `0${bCnt}` : `${bCnt}`;
                    const smallStr = sCnt < 10 ? `0${sCnt}` : `${sCnt}`;
                    msg = `Today ( ${exFactory} ) We 𝙽𝚎𝚎𝚍 ${bigStr} Big (23 Feet) & ${smallStr} Small (${counts.feet} Feet) 𝙲𝚊𝚛𝚐𝚘 𝙵𝚘𝚛 "${depot}" 𝙳𝚎𝚙𝚘 . 𝙶𝚘𝚘𝚍𝚜 𝚁𝚎𝚊𝚍𝚢 𝙿𝚕𝚎𝚊𝚜𝚎 𝚂𝚎𝚗𝚍 𝙲𝚊𝚛𝚐𝚘 𝚄𝚛𝚐𝚎𝚗𝚝𝚕𝚢 . [ Note: Arrange GPS-enabled cargos as per our requirement.]`;
                } else {
                    const countStr = sCnt < 10 ? `0${sCnt}` : `${sCnt}`;
                    const wordStr = numberToWord(sCnt);
                    msg = `Today ( ${exFactory} ) We 𝙽𝚎𝚎𝚍 ${countStr} ( ${wordStr} ) Small (${counts.feet} Feet) 𝙲𝚊𝚛𝚐𝚘 𝙵𝚘𝚛 "${depot}" 𝙳𝚎𝚙𝚘 . 𝙶𝚘𝚘𝚍𝚜 𝚁𝚎𝚊𝚍𝚢 𝙿𝚕𝚎𝚊𝚜𝚎 𝚂𝚎𝚗𝚍 𝙲𝚊𝚛𝚐𝚘 𝚄𝚛𝚐𝚎𝚗𝚝𝚕𝚢 . [ Note: Arrange GPS-enabled cargos as per our requirement.]`;
                }

                const cardDiv = document.createElement('div');
                cardDiv.className = 'card';
                const outputId = `out-trans-${transName.replace(/\s+/g, '-').toLowerCase()}`;

                cardDiv.innerHTML = `
                    <div class="card-header">
                        <div class="card-title">
                            <span>🚛</span> ${cardIndex}. Transport Group SMS – ${transName} (No CBM Mentioned)
                        </div>
                        <button class="btn btn-amber" onclick="copyOutput('${outputId}', 'Requisition SMS for ${transName} copied!')">
                            📋 Copy ${transName} SMS
                        </button>
                    </div>
                    <div id="${outputId}" class="output-box transport">${msg}</div>
                `;

                sepContainer.appendChild(cardDiv);
                cardIndex++;
            }

            // 3. PROFESSIONAL EMAIL REPLY FORMAT (MATCHING SULTAN SIR'S EXACT TEMPLATE)
            const greenLinkHTML = `<a href="${chatLink}" target="_blank" rel="noopener noreferrer" style="color: #059669 !important; font-weight: bold !important; text-decoration: underline !important;">${chatLink}</a>`;
            const displayGreenLinkUI = `<a href="${chatLink}" target="_blank" rel="noopener noreferrer" class="chat-green-link">${chatLink}</a>`;
            
            const emailFormatHTMLView = `Dear ${recipientFirstName},<br><br>
We have already made the initial arrangements for this shipment program. You can find further details via the link below:<br>
Export Program Details – Google Chat<br><br>
${displayGreenLinkUI}<br><br>
Export Program for Today: ${exFactory}<br>
Hand Over Date: ${handover}<br>
 Depot: ${depot}<br>
 Total Volume: ${totalCbm}<br>
 Total Cargos: ${totalCargosStr}<br>
 Buyer: ${buyer}<br>
 ERP Nos.:<br>
${erpBreakdown.replace(/\n/g, '<br>')}<br>
 Merchandiser: ${merchandiser}<br>
 Commercial: ${commercial}<br>
 Cargo Source:<br>
${cargoSourceEmail.replace(/\n/g, '<br>')}<br><br>
𝘑𝘢𝘻𝘢𝘬𝘢𝘭𝘭𝘢𝘩 𝘒𝘩𝘢𝘪𝘳𝘢𝘯,<br>
${signature}`;

            const emailFormatClipboardHTML = `<div style="font-family: Arial, sans-serif; font-size: 14px; color: #1e293b; line-height: 1.6;">
Dear ${recipientFirstName},<br><br>
We have already made the initial arrangements for this shipment program. You can find further details via the link below:<br>
Export Program Details – Google Chat<br><br>
${greenLinkHTML}<br><br>
Export Program for Today: ${exFactory}<br>
Hand Over Date: ${handover}<br>
 Depot: ${depot}<br>
 Total Volume: ${totalCbm}<br>
 Total Cargos: ${totalCargosStr}<br>
 Buyer: ${buyer}<br>
 ERP Nos.:<br>
${erpBreakdown.replace(/\n/g, '<br>')}<br>
 Merchandiser: ${merchandiser}<br>
 Commercial: ${commercial}<br>
 Cargo Source:<br>
${cargoSourceEmail.replace(/\n/g, '<br>')}<br><br>
𝘑𝘢𝘻𝘢𝘬𝘢𝘭𝘭𝘢𝘩 𝘒𝘩𝘢𝘪𝘳𝘢𝘯,<br>
${signature}
</div>`;

            const emailFormatText = `Dear ${recipientFirstName},

We have already made the initial arrangements for this shipment program. You can find further details via the link below:
Export Program Details – Google Chat

${chatLink}

Export Program for Today: ${exFactory}
Hand Over Date: ${handover}
 Depot: ${depot}
 Total Volume: ${totalCbm}
 Total Cargos: ${totalCargosStr}
 Buyer: ${buyer}
 ERP Nos.:
${erpBreakdown}
 Merchandiser: ${merchandiser}
 Commercial: ${commercial}
 Cargo Source:
${cargoSourceEmail}

𝘑𝘢𝘻𝘢𝘬𝘢𝘭𝘭𝘢𝘩 𝘒𝘩𝘢𝘪𝘳𝘢𝘯,
${signature}`;

            window.latestEmailHTML = emailFormatClipboardHTML;

            // 4. AIR EXPORT SMS FORMAT (POSITIONED AT BOTTOM RIGHT)
            const airFormat = `Air Export Program for Today: ${exFactory}
Hand Over Date: ${handover}
🏭 Depot: ${depot}
📦 Total Volume: ${totalCbm}
🚛 Total Cargos: ${totalCargosStr}
🛒 Buyer: ${buyer}
📋 ERP No.: ${erpBreakdown.replace(/\n/g, ', ')}
👤 Merchandiser: ${merchandiser}
👤 Commercial: ${commercial}
🔹 Cargo Source:
🚛 ${airTrans}: ${totalCargosStr} Cargo
🚐 Covered Van: ${vanNo || '11-3260'}
👤 Driver: ${driverName || 'Mr. Anwar'}
📞 Contact: ${driverContact || '01939-385175'}`;

            // Push Outputs to DOM
            document.getElementById('out-sms').textContent = smsFormat;
            document.getElementById('out-email-html').innerHTML = emailFormatHTMLView;
            document.getElementById('out-email-text').textContent = emailFormatText;
            document.getElementById('out-air').textContent = airFormat;

            // Toggle Air Card Visibility based on Air program detection or checkbox
            const airCard = document.getElementById('air-card');
            if (isAir) {
                airCard.style.display = 'flex';
            } else {
                airCard.style.display = 'none';
            }
        }

        async function copyRichTextEmail() {
            const htmlContent = window.latestEmailHTML;
            const textContent = document.getElementById('out-email-text').textContent;

            if (!htmlContent) {
                showToast('No content to copy!');
                return;
            }

            if (navigator.clipboard && window.ClipboardItem) {
                try {
                    const blobHtml = new Blob([htmlContent], { type: 'text/html' });
                    const blobText = new Blob([textContent], { type: 'text/plain' });
                    const item = new ClipboardItem({
                        'text/html': blobHtml,
                        'text/plain': blobText
                    });
                    await navigator.clipboard.write([item]);
                    showToast('📧 Rich Email Copied! Link is active green in Gmail/Outlook.');
                    return;
                } catch (err) {
                    console.warn('ClipboardItem rich text copy failed, trying fallback...', err);
                }
            }

            try {
                const tempDiv = document.createElement('div');
                tempDiv.style.position = 'fixed';
                tempDiv.style.pointerEvents = 'none';
                tempDiv.style.opacity = '0';
                tempDiv.innerHTML = htmlContent;
                document.body.appendChild(tempDiv);

                const range = document.createRange();
                range.selectNodeContents(tempDiv);
                const selection = window.getSelection();
                selection.removeAllRanges();
                selection.addRange(range);

                const successful = document.execCommand('copy');
                selection.removeAllRanges();
                document.body.removeChild(tempDiv);

                if (successful) {
                    showToast('📧 Rich Email Copied! Paste into Gmail/Outlook.');
                } else {
                    throw new Error('Selection copy failed');
                }
            } catch (err) {
                copyOutput('out-email-text', 'Copied as Plain Text.');
            }
        }

        function copyOutput(elementId, toastMessage) {
            const textToCopy = document.getElementById(elementId).textContent;
            if (!textToCopy.trim()) return;

            const tempArea = document.createElement('textarea');
            tempArea.value = textToCopy;
            document.body.appendChild(tempArea);
            tempArea.select();

            try {
                document.execCommand('copy');
                showToast(toastMessage || 'Copied to clipboard!');
            } catch (err) {
                showToast('Failed to copy text.');
            }

            document.body.removeChild(tempArea);
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toast-msg');
            toastMsg.textContent = msg;
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 2600);
        }
    </script>
</body>
</html>
