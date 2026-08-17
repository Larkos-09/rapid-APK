<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#1a202c">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>Mi Diario Financiero Pro</title>
    
    <!-- Para que funcione OFFLINE -->
    <link rel="manifest" href="data:application/json;base64,ewogICJuYW1lIjogIk1pIERpYXJpbyBGaW5hbmNpZXJvIiwKICAic2hvcnRfbmFtZSI6ICJEaWFyaW8iLAogICJkZXNjcmlwdGlvbiI6ICJBcHAgZGUgZ2FzdG9zIHkgZ2FuYW5jaWFzIiwKICAic3RhcnRfdXJsIjogIi4iLAogICJkaXNwbGF5IjogInN0YW5kYWxvbmUiLAogICJiYWNrZ3JvdW5kX2NvbG9yIjogIiMxYTIwMmMiLAogICJ0aGVtZV9jb2xvciI6ICIjMWEyMDJjIiwKICAiaWNvbnMiOiBbCiAgICB7CiAgICAgICJzcmMiOiAiZGF0YTppbWFnZS9zdmcreG1sLDxzdmcgeG1sbnM9J2h0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnJyB2aWV3Qm94PScwIDAgNTEyIDUxMicgd2lkdGg9JzUxMicgaGVpZ2h0PSc1MTInPjxyZWN0IHdpZHRoPSc1MTInIGhlaWdodD0nNTEyJyByeD0nNTAlJyBmaWxsPScjMjlkMzY2Jy8+PHRleHQgeD0nMjU2JyB5PSczNDAnIGZvbnQtc2l6ZT0nMjUwJyB0ZXh0LWFuY2hvcj0nbWlkZGxlJyBmaWxsPSd3aGl0ZScgZm9udC1mYW1pbHk9J3NhbnMtc2VyaWYnPsk8L3RleHQ+PC9zdmc+IgogICAgfQogIF0KfQ==">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }
        
        :root {
            --bg-primary: #f7fafc;
            --bg-card: #ffffff;
            --text-primary: #1a202c;
            --text-secondary: #4a5568;
            --border-color: #e2e8f0;
            --shadow: 0 10px 40px rgba(0,0,0,0.08);
            --green: #48bb78;
            --red: #fc8181;
            --blue: #4299e1;
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        [data-theme="dark"] {
            --bg-primary: #1a202c;
            --bg-card: #2d3748;
            --text-primary: #f7fafc;
            --text-secondary: #a0aec0;
            --border-color: #4a5568;
            --shadow: 0 10px 40px rgba(0,0,0,0.4);
        }
        
        body {
            background: var(--bg-primary);
            color: var(--text-primary);
            padding: 16px;
            max-width: 500px;
            margin: 0 auto;
            transition: var(--transition);
            min-height: 100vh;
        }
        
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding: 16px;
            background: var(--bg-card);
            border-radius: 16px;
            box-shadow: var(--shadow);
        }
        
        .header h1 {
            font-size: 22px;
            font-weight: 700;
            background: linear-gradient(135deg, #48bb78, #4299e1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .header-actions {
            display: flex;
            gap: 10px;
        }
        
        .btn-icon {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: var(--transition);
        }
        
        .btn-icon:hover {
            background: var(--border-color);
            transform: scale(1.1);
        }
        
        .card {
            background: var(--bg-card);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 16px;
            box-shadow: var(--shadow);
            transition: var(--transition);
            animation: slideUp 0.5s ease;
        }
        
        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .fecha {
            text-align: center;
            color: var(--text-secondary);
            font-size: 14px;
            margin-bottom: 16px;
        }
        
        .balance {
            text-align: center;
            font-size: 42px;
            font-weight: 800;
            padding: 20px;
            border-radius: 12px;
            margin: 10px 0;
            transition: var(--transition);
        }
        
        .balance.positivo {
            color: var(--green);
            background: rgba(72, 187, 120, 0.1);
        }
        
        .balance.negativo {
            color: var(--red);
            background: rgba(252, 129, 129, 0.1);
        }
        
        .balance.neutral {
            color: var(--text-secondary);
            background: rgba(160, 174, 192, 0.1);
        }
        
        .dinero-total {
            font-size: 20px;
            font-weight: 600;
            text-align: center;
            padding: 12px;
            background: rgba(66, 153, 225, 0.1);
            border-radius: 10px;
            margin: 10px 0;
            color: var(--blue);
        }
        
        .input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 12px;
            align-items: center;
        }
        
        .input-group label {
            min-width: 70px;
            font-weight: 600;
            color: var(--text-primary);
        }
        
        .input-group input {
            flex: 1;
            padding: 12px 16px;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            font-size: 16px;
            background: var(--bg-primary);
            color: var(--text-primary);
            outline: none;
            transition: var(--transition);
        }
        
        .input-group input:focus {
            border-color: var(--blue);
            box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.2);
        }
        
        .btn {
            background: var(--blue);
            color: white;
            border: none;
            padding: 14px 24px;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            width: 100%;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .btn:active {
            transform: scale(0.97);
        }
        
        .btn-success {
            background: linear-gradient(135deg, #48bb78, #38a169);
        }
        
        .btn-warning {
            background: linear-gradient(135deg, #ed8936, #dd6b20);
        }
        
        .btn-danger {
            background: linear-gradient(135deg, #fc8181, #e53e3e);
        }
        
        .btn-secondary {
            background: var(--text-secondary);
        }
        
        .btn-pequeno {
            padding: 10px 16px;
            font-size: 14px;
            width: auto;
        }
        
        .flex-botones {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .flex-botones .btn {
            flex: 1;
        }
        
        .oculto {
            display: none !important;
        }
        
        .notificacion {
            background: rgba(66, 153, 225, 0.1);
            border-left: 4px solid var(--blue);
            padding: 12px 16px;
            border-radius: 8px;
            margin-bottom: 15px;
            color: var(--blue);
            animation: slideIn 0.5s ease;
        }
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }
        
        .historial-item {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid var(--border-color);
            transition: var(--transition);
        }
        
        .historial-item:hover {
            background: var(--bg-primary);
            padding-left: 8px;
            border-radius: 8px;
        }
        
        .historial-item .dia {
            color: var(--text-secondary);
        }
        
        .historial-item .monto {
            font-weight: 600;
        }
        
        .historial-item .monto.positivo {
            color: var(--green);
        }
        
        .historial-item .monto.negativo {
            color: var(--red);
        }
        
        .grafico {
            display: flex;
            align-items: flex-end;
            gap: 4px;
            height: 120px;
            padding: 10px 0;
            margin-top: 10px;
        }
        
        .barra {
            flex: 1;
            background: linear-gradient(to top, var(--blue), #63b3ed);
            border-radius: 4px 4px 0 0;
            transition: var(--transition);
            min-height: 4px;
            position: relative;
        }
        
        .barra.positivo {
            background: linear-gradient(to top, var(--green), #68d391);
        }
        
        .barra.negativo {
            background: linear-gradient(to top, var(--red), #fc8181);
        }
        
        .barra:hover {
            opacity: 0.8;
            transform: scaleY(1.02);
            transform-origin: bottom;
        }
        
        .total-mes {
            background: linear-gradient(135deg, var(--blue), #2b6cb0);
            color: white;
            padding: 16px;
            border-radius: 12px;
            text-align: center;
            margin-top: 15px;
            font-weight: 600;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 10px;
            margin: 15px 0;
        }
        
        .stat-item {
            text-align: center;
            padding: 12px;
            background: var(--bg-primary);
            border-radius: 12px;
        }
        
        .stat-item .valor {
            font-size: 20px;
            font-weight: 700;
        }
        
        .stat-item .label {
            font-size: 12px;
            color: var(--text-secondary);
            margin-top: 4px;
        }
        
        .backup-section {
            margin-top: 15px;
            padding: 16px;
            background: var(--bg-primary);
            border-radius: 12px;
        }
        
        @media (max-width: 480px) {
            .input-group {
                flex-direction: column;
                align-items: stretch;
            }
            .input-group label {
                min-width: auto;
            }
            .stats-grid {
                grid-template-columns: 1fr 1fr;
            }
            .balance {
                font-size: 32px;
            }
        }
    </style>
</head>
<body>
    <!-- HEADER -->
    <div class="header">
        <h1>💰 Mi Diario Pro</h1>
        <div class="header-actions">
            <button class="btn-icon" id="btnTema" title="Cambiar tema">🌓</button>
            <button class="btn-icon" id="btnBackup" title="Backup">💾</button>
        </div>
    </div>

    <!-- NOTIFICACIÓN -->
    <div id="notificacionDiaAnterior" class="notificacion oculto"></div>

    <!-- BALANCE PRINCIPAL -->
    <div class="card">
        <div class="fecha" id="fechaActual"></div>
        <div id="balanceDia" class="balance neutral">$0.00</div>
        <div class="dinero-total" id="dineroTotalDisplay">💰 Total: $0.00</div>
    </div>

    <!-- STATS RÁPIDOS -->
    <div class="stats-grid" id="statsGrid">
        <div class="stat-item">
            <div class="valor" id="statDias">0</div>
            <div class="label">Días registrados</div>
        </div>
        <div class="stat-item">
            <div class="valor" id="statPromedio">$0</div>
            <div class="label">Promedio diario</div>
        </div>
        <div class="stat-item">
            <div class="valor" id="statMejorDia">$0</div>
            <div class="label">Mejor día</div>
        </div>
    </div>

    <!-- FORMULARIO -->
    <div class="card">
        <div class="input-group">
            <label>💰 Gané</label>
            <input type="number" id="ingreso" placeholder="0.00" step="0.01">
        </div>
        <div class="input-group">
            <label>💸 Gasté</label>
            <input type="number" id="gasto" placeholder="0.00" step="0.01">
        </div>
        <button class="btn btn-success" id="btnAgregar">✅ Agregar hoy</button>
        
        <div class="flex-botones">
            <button class="btn btn-warning btn-pequeno" id="btnTotalActual">💰 Actualizar total</button>
            <button class="btn btn-secondary btn-pequeno" id="btnVerHistorial">📊 Ver historial</button>
        </div>
        
        <div id="campoTotal" class="oculto" style="margin-top:15px;">
            <div class="input-group">
                <label>💰 Total actual</label>
                <input type="number" id="totalActualInput" placeholder="Ej: 1500.00" step="0.01">
            </div>
            <button class="btn btn-warning" id="btnGuardarTotal">Guardar total</button>
        </div>
    </div>

    <!-- GRÁFICO -->
    <div class="card" id="graficoContainer">
        <h3 style="margin-bottom:10px; color: var(--text-secondary);">📈 Últimos 7 días</h3>
        <div class="grafico" id="graficoBarras"></div>
    </div>

    <!-- HISTORIAL -->
    <div id="historialContainer" class="card oculto">
        <h2>📋 Historial completo</h2>
        <div id="historialLista"></div>
        <div id="resumenMes" class="total-mes"></div>
        <button class="btn btn-secondary btn-pequeno" id="btnCerrarHistorial" style="margin-top:10px;">Cerrar</button>
    </div>

    <!-- BACKUP -->
    <div id="backupContainer" class="card oculto">
        <h3>💾 Backup y restauración</h3>
        <div class="backup-section">
            <button class="btn btn-success btn-pequeno" id="btnExportar" style="width:100%; margin-bottom:10px;">📤 Exportar datos</button>
            <input type="file" id="fileInput" accept=".json" style="display:none;">
            <button class="btn btn-warning btn-pequeno" id="btnImportar" style="width:100%;">📥 Importar backup</button>
        </div>
        <button class="btn btn-secondary btn-pequeno" id="btnCerrarBackup" style="margin-top:10px;">Cerrar</button>
    </div>

    <!-- SERVICE WORKER REGISTRATION -->
    <script>
        // ============ SERVICE WORKER (OFFLINE) ============
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('data:text/javascript;base64,' + btoa(`
                const CACHE_NAME = 'diario-v1';
                const urlsToCache = [
                    '.',
                    'data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><rect width="512" height="512" rx="50%" fill="#29d366"/><text x="256" y="340" font-size="250" text-anchor="middle" fill="white" font-family="sans-serif">💰</text></svg>'
                ];

                self.addEventListener('install', event => {
                    event.waitUntil(
                        caches.open(CACHE_NAME)
                            .then(cache => cache.addAll(urlsToCache))
                    );
                });

                self.addEventListener('fetch', event => {
                    event.respondWith(
                        caches.match(event.request)
                            .then(response => response || fetch(event.request))
                    );
                });
            `))
            .then(() => console.log('✅ Service Worker registrado - OFFLINE activado'))
            .catch(err => console.log('⚠️ Service Worker:', err));
        }

        // ============ CÓDIGO PRINCIPAL ============
        const STORAGE_KEY = 'diario_pro_data';
        const NOTIF_KEY = 'diario_ultima_notificacion';

        // ============ FUNCIONES ============
        function obtenerDatos() {
            try {
                const data = localStorage.getItem(STORAGE_KEY);
                return data ? JSON.parse(data) : { dias: {}, totalActual: null, config: { tema: 'light' } };
            } catch {
                return { dias: {}, totalActual: null, config: { tema: 'light' } };
            }
        }

        function guardarDatos(data) {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
        }

        function obtenerFechaStr(fecha) {
            return fecha.toISOString().split('T')[0];
        }

        function obtenerFechaActual() {
            return new Date();
        }

        function formatearMoneda(monto) {
            return '$' + Number(monto).toFixed(2);
        }

        function obtenerNombreMes(numero) {
            const meses = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre'];
            return meses[numero];
        }

        // ============ NOTIFICACIONES ============
        function mostrarNotificacion(mensaje) {
            if (Notification.permission === 'granted') {
                new Notification('📊 Resumen diario', {
                    body: mensaje,
                    icon: 'data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><rect width="512" height="512" rx="50%" fill="#29d366"/><text x="256" y="340" font-size="250" text-anchor="middle" fill="white" font-family="sans-serif">💰</text></svg>'
                });
            }
        }

        function verificarNotificacionDiaria() {
            const hoy = obtenerFechaStr(obtenerFechaActual());
            const ultimaNotif = localStorage.getItem(NOTIF_KEY);
            
            if (ultimaNotif === hoy) return;
            
            const data = obtenerDatos();
            const ayer = new Date(obtenerFechaActual());
            ayer.setDate(ayer.getDate() - 1);
            const ayerStr = obtenerFechaStr(ayer);
            
            if (data.dias[ayerStr]) {
                const dia = data.dias[ayerStr];
                const neto = dia.ingreso - dia.gasto;
                let mensaje = `Ayer ${neto >= 0 ? 'ganaste' : 'perdiste'} ${formatearMoneda(Math.abs(neto))}.`;
                
                if (data.totalActual !== null && data.totalActual !== undefined) {
                    mensaje += ` Terminaste con ${formatearMoneda(data.totalActual)} en total.`;
                }
                
                const notifDiv = document.getElementById('notificacionDiaAnterior');
                notifDiv.textContent = '📢 ' + mensaje;
                notifDiv.classList.remove('oculto');
                
                mostrarNotificacion(mensaje);
                localStorage.setItem(NOTIF_KEY, hoy);
            }
        }

        // ============ ACTUALIZAR VISTA ============
        function actualizarVista() {
            const hoy = obtenerFechaStr(obtenerFechaActual());
            const data = obtenerDatos();
            
            // Fecha
            document.getElementById('fechaActual').textContent = '📅 ' + new Date().toLocaleDateString('es-ES', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
            
            // Balance del día
            const balanceDiv = document.getElementById('balanceDia');
            const diaActual = data.dias[hoy];
            let neto = 0;
            if (diaActual) {
                neto = diaActual.ingreso - diaActual.gasto;
            }
            balanceDiv.textContent = formatearMoneda(neto);
            balanceDiv.className = 'balance';
            if (neto > 0) balanceDiv.classList.add('positivo');
            else if (neto < 0) balanceDiv.classList.add('negativo');
            else balanceDiv.classList.add('neutral');
            
            // Dinero total
            const totalDisplay = document.getElementById