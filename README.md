[index.html](https://github.com/user-attachments/files/27287651/index.html)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Beauty Of Novella">
    <title>Beauty Of Novella v4.0 - Búsqueda Inteligente</title>
    
    <!-- EmailJS -->
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/index.min.js"></script>
    
    <!-- PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --cafe-intenso: #3B2417;
            --caramelo: #6D3C1C;
            --miel: #C57938;
            --vainilla: #E7C196;
            --blanco: #FFFFFF;
            --negro: #000000;
            --verde: #34A853;
            --azul: #4284F4;
            --naranja: #F37220;
            --rojo: #DF1E26;
            --gris-claro: #F5F5F5;
            --gris-medio: #D9D9D9;
            --gris-oscuro: #666666;
        }

        html, body {
            width: 100%;
            height: 100%;
            overflow-x: hidden;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, var(--vainilla) 0%, var(--blanco) 100%);
            color: var(--cafe-intenso);
            font-size: 16px;
        }

        input, select, textarea {
            -webkit-user-select: text;
            user-select: text;
        }

        .header {
            background: linear-gradient(135deg, var(--cafe-intenso) 0%, var(--caramelo) 100%);
            color: var(--blanco);
            padding: max(1rem, env(safe-area-inset-top)) 1rem 1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 4px 15px rgba(59, 36, 23, 0.15);
            position: sticky;
            top: 0;
            z-index: 100;
            gap: 1rem;
        }

        .header-left {
            display: flex;
            align-items: center;
            gap: 0.8rem;
            flex: 1;
            min-width: 0;
        }

        .logo {
            width: 45px;
            height: 45px;
            background: var(--vainilla);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            color: var(--cafe-intenso);
            flex-shrink: 0;
        }

        .header-title h1 {
            font-size: 0.95rem;
            font-weight: 700;
            margin: 0;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .header-title p {
            font-size: 0.6rem;
            opacity: 0.85;
            margin: 2px 0 0 0;
        }

        .sync-status {
            display: flex;
            align-items: center;
            gap: 0.4rem;
            font-size: 0.7rem;
            padding: 0.3rem 0.6rem;
            background: rgba(255,255,255,0.15);
            border-radius: 12px;
            flex-shrink: 0;
        }

        .sync-dot {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: var(--rojo);
            animation: pulse 1s infinite;
            flex-shrink: 0;
        }

        .sync-dot.connected {
            background: var(--verde);
            animation: none;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .nav-tabs {
            display: flex;
            gap: 0;
            background: var(--blanco);
            border-bottom: 2px solid var(--gris-medio);
            overflow-x: auto;
            padding: 0;
        }

        .nav-tab {
            padding: 1rem 0.8rem;
            cursor: pointer;
            border: none;
            background: none;
            color: var(--gris-oscuro);
            font-size: 1.2rem;
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
            white-space: nowrap;
            min-height: 44px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .nav-tab.active {
            color: var(--cafe-intenso);
            border-bottom-color: var(--miel);
        }

        .container {
            max-width: 100%;
            margin: 0;
            padding: 1rem;
            padding-bottom: max(2rem, env(safe-area-inset-bottom));
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.3s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .card {
            background: var(--blanco);
            border-radius: 12px;
            padding: 1.2rem;
            box-shadow: 0 2px 8px rgba(59, 36, 23, 0.08);
            border-left: 4px solid var(--miel);
            margin-bottom: 1rem;
        }

        .card h3 {
            font-size: 1rem;
            margin-bottom: 1rem;
            color: var(--cafe-intenso);
        }

        .alert {
            padding: 0.8rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            border-left: 4px solid var(--naranja);
            background: rgba(243, 114, 32, 0.1);
            font-size: 0.9rem;
        }

        .alert-info {
            border-left-color: var(--azul);
            background: rgba(66, 132, 244, 0.1);
            color: var(--azul);
        }

        .btn {
            padding: 0.75rem 1.2rem;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1rem;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            min-height: 44px;
            min-width: 44px;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--cafe-intenso), var(--caramelo));
            color: var(--blanco);
        }

        .btn-success {
            background: var(--verde);
            color: var(--blanco);
        }

        .btn-warning {
            background: var(--naranja);
            color: var(--blanco);
        }

        .btn-danger {
            background: var(--rojo);
            color: var(--blanco);
        }

        .btn-block {
            width: 100%;
            justify-content: center;
            margin-top: 1rem;
        }

        label {
            display: block;
            margin: 1rem 0 0.4rem 0;
            font-weight: 600;
            color: var(--cafe-intenso);
            font-size: 0.9rem;
        }

        input, select, textarea {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid var(--gris-medio);
            border-radius: 8px;
            font-family: inherit;
            font-size: 16px;
            margin-bottom: 0.5rem;
            -webkit-appearance: none;
            appearance: none;
            background-color: var(--blanco);
        }

        select {
            background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 12 8'><polyline points='1 1 6 6 11 1' fill='none' stroke='%236D3C1C' stroke-width='2' stroke-linecap='round'/></svg>");
            background-repeat: no-repeat;
            background-position: right 0.75rem center;
            background-size: 12px;
            padding-right: 2.5rem;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--miel);
            box-shadow: 0 0 0 3px rgba(197, 121, 56, 0.1);
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.8rem;
        }

        .grid-3 {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 0.8rem;
        }

        .resultado-item {
            padding: 1rem;
            background: var(--gris-claro);
            border-radius: 10px;
            margin-bottom: 0.8rem;
            border-left: 4px solid var(--miel);
            display: grid;
            grid-template-columns: 80px 1fr auto;
            gap: 1rem;
            align-items: start;
        }

        .resultado-imagen {
            width: 80px;
            height: 80px;
            border-radius: 8px;
            background: var(--blanco);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            border: 1px solid var(--gris-medio);
            overflow: hidden;
        }

        .resultado-imagen img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .resultado-info {
            display: flex;
            flex-direction: column;
            gap: 0.3rem;
        }

        .resultado-info strong {
            color: var(--cafe-intenso);
            font-size: 0.95rem;
        }

        .resultado-info small {
            color: var(--gris-oscuro);
            font-size: 0.85rem;
        }

        .resultado-precio {
            font-weight: 700;
            color: var(--miel);
            font-size: 1.1rem;
        }

        .resultado-stock {
            padding: 0.4rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            white-space: nowrap;
        }

        .stock-alto {
            background: rgba(52, 168, 83, 0.2);
            color: var(--verde);
        }

        .stock-bajo {
            background: rgba(223, 30, 38, 0.2);
            color: var(--rojo);
        }

        .stock-medio {
            background: rgba(243, 114, 32, 0.2);
            color: var(--naranja);
        }

        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid var(--gris-claro);
            border-top-color: var(--miel);
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .result {
            padding: 0.8rem;
            border-radius: 8px;
            margin-top: 0.8rem;
            text-align: center;
            animation: slideIn 0.3s ease;
            font-weight: 600;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .result.success {
            background: rgba(52, 168, 83, 0.15);
            border: 2px solid var(--verde);
            color: var(--verde);
        }

        .result.error {
            background: rgba(223, 30, 38, 0.15);
            border: 2px solid var(--rojo);
            color: var(--rojo);
        }

        .info-text {
            font-size: 0.85rem;
            color: var(--gris-oscuro);
            line-height: 1.6;
            margin-bottom: 1rem;
        }

        @media (max-width: 768px) {
            .resultado-item {
                grid-template-columns: 1fr;
            }

            .grid-2, .grid-3 {
                grid-template-columns: 1fr;
            }

            .resultado-imagen {
                width: 100%;
                height: 100px;
            }
        }
    </style>
</head>
<body>
    <!-- HEADER -->
    <header class="header">
        <div class="header-left">
            <div class="logo">BON</div>
            <div class="header-title">
                <h1>Beauty Of Novella</h1>
                <p>v4.0 Búsqueda Inteligente</p>
            </div>
        </div>
        <div class="sync-status">
            <div class="sync-dot" id="sync-dot"></div>
            <span id="sync-text">●</span>
        </div>
    </header>

    <!-- NAVEGACIÓN -->
    <div class="nav-tabs">
        <button class="nav-tab active" onclick="cambiarPestana(event, 'config')">⚙️</button>
        <button class="nav-tab" onclick="cambiarPestana(event, 'buscar')">🔍</button>
        <button class="nav-tab" onclick="cambiarPestana(event, 'venta')">🛒</button>
        <button class="nav-tab" onclick="cambiarPestana(event, 'stock')">📦</button>
        <button class="nav-tab" onclick="cambiarPestana(event, 'inventario')">📋</button>
        <button class="nav-tab" onclick="cambiarPestana(event, 'reportes')">📈</button>
    </div>

    <!-- CONTENEDOR -->
    <div class="container">

        <!-- CONFIG -->
        <div id="config" class="tab-content active">
            <h2 style="margin-bottom: 1.5rem; color: var(--cafe-intenso);">⚙️ Configuración</h2>

            <div class="card">
                <h3>Google Apps Script v2.2</h3>
                <p class="info-text">URL del Google Apps Script</p>
                <input type="text" id="script-url" placeholder="https://script.google.com/macros/s/...">
                <button class="btn btn-primary btn-block" onclick="verificarConexion()">🔌 Verificar</button>
                <div id="resultado-config"></div>
            </div>

            <div class="card">
                <h3>📧 EmailJS (Opcional)</h3>
                <p class="info-text">Para envío automático de recibos</p>
                <input type="text" id="emailjs-service" placeholder="service_xxxxx">
                <input type="text" id="emailjs-template" placeholder="template_xxxxx">
                <input type="text" id="emailjs-user" placeholder="xxxxxxxxxxxxxx">
                <button class="btn btn-primary btn-block" onclick="verificarEmail()">📧 Verificar</button>
                <div id="resultado-email"></div>
            </div>

            <div class="card" style="background: rgba(52, 168, 83, 0.05); border-left-color: var(--verde);">
                <h3 style="color: var(--verde);">✅ v4.0 Incluye</h3>
                <p class="info-text">
                    ✓ Búsqueda por marca/categoría/código<br>
                    ✓ 16 categorías precargadas<br>
                    ✓ 45+ marcas precargadas<br>
                    ✓ Carga de imágenes<br>
                    ✓ Dropdowns inteligentes<br>
                    ✓ Tabla de resultados clara
                </p>
            </div>
        </div>

        <!-- BUSCAR PRODUCTO -->
        <div id="buscar" class="tab-content">
            <h2 style="margin-bottom: 1rem; color: var(--cafe-intenso);">🔍 Buscar Producto</h2>

            <div class="alert alert-info">
                <strong>Cómo usar:</strong> Selecciona marca, categoría o ingresa código. Rellena al menos uno y haz clic Buscar.
            </div>

            <div class="card">
                <h3>Filtros de Búsqueda</h3>
                
                <label>Marca (opcional):</label>
                <select id="buscar-marca">
                    <option value="">-- Selecciona marca --</option>
                    <optgroup label="COREANAS">
                        <option>COSRX</option>
                        <option>MIXSOON</option>
                        <option>ROUND LA</option>
                        <option>MEDICUBE</option>
                        <option>BEAUTY OF JOSEON</option>
                        <option>SKIN1004</option>
                        <option>MARY & MAY</option>
                        <option>ANUA</option>
                        <option>TOCOBO</option>
                        <option>PURITO</option>
                        <option>ISNTREE</option>
                        <option>SINK & LAB</option>
                        <option>DR. JART+</option>
                        <option>NUMBUZIN</option>
                        <option>VT</option>
                        <option>TORRIDEN</option>
                        <option>LASHILE BEAUTY</option>
                        <option>THE ORDINARY</option>
                        <option>INNISFREE</option>
                        <option>PYUNKANG YUL</option>
                        <option>SHINFOOD</option>
                        <option>SOME BY MI</option>
                        <option>BIODANCE</option>
                        <option>DR. ALTHEA</option>
                        <option>KLAIRS</option>
                        <option>AROMATICA</option>
                        <option>TIRTIR</option>
                        <option>SEOUL 1988</option>
                        <option>PETITFEE</option>
                        <option>CENTELLIAN 24+</option>
                    </optgroup>
                    <optgroup label="JAPONESAS">
                        <option>HADA LABO</option>
                        <option>ROHTO</option>
                        <option>MISSHA</option>
                    </optgroup>
                    <optgroup label="BELGAS Y OTRAS">
                        <option>AVENE</option>
                        <option>PURE ELEMENT ORGANICS</option>
                        <option>PATCHOLOGY</option>
                        <option>TNTNMOMS</option>
                        <option>KLAVUU</option>
                        <option>CERAVE</option>
                        <option>EUCERIN</option>
                    </optgroup>
                </select>

                <label>Categoría (opcional):</label>
                <select id="buscar-categoria">
                    <option value="">-- Selecciona categoría --</option>
                    <optgroup label="LIMPIADORES">
                        <option>Aceite Limpiador</option>
                        <option>Limpiador en Espuma</option>
                        <option>Limpiador en Bálsamo</option>
                        <option>Limpiador en Gel</option>
                    </optgroup>
                    <optgroup label="TÓNICOS Y LOCIONES">
                        <option>Tónico</option>
                        <option>Loción</option>
                        <option>Mist - Bruma</option>
                    </optgroup>
                    <optgroup label="TRATAMIENTOS">
                        <option>Mascarilla Sheets</option>
                        <option>Mascarilla Gel</option>
                        <option>Contorno de Ojos</option>
                        <option>Crema</option>
                    </optgroup>
                    <optgroup label="PROTECCIÓN SOLAR">
                        <option>Protector Solar Crema</option>
                        <option>Protector Solar en Barra</option>
                    </optgroup>
                    <optgroup label="EXTRAS">
                        <option>Muestras</option>
                        <option>Accesorios</option>
                        <option>Papelería</option>
                    </optgroup>
                </select>

                <label>Código de Barras (opcional):</label>
                <input type="text" id="buscar-codigo" placeholder="8809662381046">

                <button class="btn btn-primary btn-block" onclick="buscarProductos()">🔍 Buscar</button>
                <div id="resultado-busqueda"></div>
            </div>
        </div>

        <!-- VENTA -->
        <div id="venta" class="tab-content">
            <h2 style="margin-bottom: 1rem; color: var(--cafe-intenso);">🛒 Nueva Venta</h2>

            <div class="grid-2">
                <div class="card">
                    <h3>Cliente</h3>
                    <input type="text" id="venta-nombre" placeholder="Nombre" style="margin-bottom: 0.5rem;">
                    <input type="email" id="venta-email" placeholder="Email" style="margin-bottom: 0.5rem;">
                    <input type="tel" id="venta-telefono" placeholder="Teléfono">
                </div>
                <div class="card">
                    <h3>Producto</h3>
                    <div id="producto-venta" style="padding: 1rem; background: var(--gris-claro); border-radius: 8px; text-align: center; color: var(--gris-oscuro); min-height: 100px; display: flex; align-items: center; justify-content: center;">
                        Sin producto
                    </div>
                </div>
            </div>

            <div class="card">
                <h3>Detalles de Venta</h3>
                
                <label>Cantidad:</label>
                <input type="number" id="venta-cantidad" value="1" min="1" style="margin-bottom: 0.5rem;">
                
                <label>Tipo:</label>
                <select id="venta-tipo" style="margin-bottom: 0.5rem;">
                    <option>Normal</option>
                    <option>Promo 1</option>
                    <option>Promo 2</option>
                    <option>🎁 Regalo</option>
                </select>

                <label>Forma de Pago:</label>
                <select id="venta-pago" style="margin-bottom: 0.5rem;">
                    <option value="">Selecciona</option>
                    <option>Efectivo</option>
                    <option>Transferencia</option>
                    <option>QR</option>
                    <option>Revolut</option>
                    <option>Bancontact</option>
                </select>

                <label>Medio:</label>
                <select id="venta-medio" style="margin-bottom: 1rem;">
                    <option value="">Selecciona</option>
                    <option>Instagram</option>
                    <option>Facebook</option>
                    <option>TikTok</option>
                    <option>Feria</option>
                    <option>Workshop</option>
                </select>

                <div style="display: flex; align-items: center; gap: 0.5rem; margin-bottom: 1rem;">
                    <input type="checkbox" id="enviar-email" checked style="width: 18px; height: 18px; margin: 0;">
                    <label style="margin: 0; display: inline;">📧 Enviar recibo</label>
                </div>

                <button class="btn btn-success btn-block" onclick="registrarVenta()">✅ Registrar</button>
                <div id="resultado-venta"></div>
            </div>
        </div>

        <!-- AGREGAR STOCK -->
        <div id="stock" class="tab-content">
            <h2 style="margin-bottom: 1rem; color: var(--cafe-intenso);">📦 Agregar Stock</h2>

            <div class="card">
                <h3>Información del Producto</h3>
                
                <label>Marca:</label>
                <select id="stock-marca" style="margin-bottom: 0.5rem;">
                    <option value="">-- Selecciona o escribe --</option>
                    <optgroup label="COREANAS">
                        <option>COSRX</option>
                        <option>MIXSOON</option>
                        <option>ROUND LA</option>
                        <option>MEDICUBE</option>
                        <option>BEAUTY OF JOSEON</option>
                        <option>SKIN1004</option>
                        <option>MARY & MAY</option>
                        <option>ANUA</option>
                        <option>TOCOBO</option>
                        <option>PURITO</option>
                        <option>ISNTREE</option>
                        <option>SINK & LAB</option>
                        <option>DR. JART+</option>
                        <option>NUMBUZIN</option>
                        <option>VT</option>
                        <option>TORRIDEN</option>
                        <option>LASHILE BEAUTY</option>
                        <option>THE ORDINARY</option>
                        <option>INNISFREE</option>
                        <option>PYUNKANG YUL</option>
                        <option>SHINFOOD</option>
                        <option>SOME BY MI</option>
                        <option>BIODANCE</option>
                        <option>DR. ALTHEA</option>
                        <option>KLAIRS</option>
                        <option>AROMATICA</option>
                        <option>TIRTIR</option>
                        <option>SEOUL 1988</option>
                        <option>PETITFEE</option>
                        <option>CENTELLIAN 24+</option>
                    </optgroup>
                    <optgroup label="JAPONESAS">
                        <option>HADA LABO</option>
                        <option>ROHTO</option>
                        <option>MISSHA</option>
                    </optgroup>
                    <optgroup label="BELGAS Y OTRAS">
                        <option>AVENE</option>
                        <option>PURE ELEMENT ORGANICS</option>
                        <option>PATCHOLOGY</option>
                        <option>TNTNMOMS</option>
                        <option>KLAVUU</option>
                        <option>CERAVE</option>
                        <option>EUCERIN</option>
                    </optgroup>
                </select>
                <input type="text" id="stock-marca-custom" placeholder="O escribe nueva marca" style="margin-bottom: 0.5rem; display: none;">

                <label>Categoría:</label>
                <select id="stock-categoria" style="margin-bottom: 0.5rem;">
                    <option value="">-- Selecciona o escribe --</option>
                    <optgroup label="LIMPIADORES">
                        <option>Aceite Limpiador</option>
                        <option>Limpiador en Espuma</option>
                        <option>Limpiador en Bálsamo</option>
                        <option>Limpiador en Gel</option>
                    </optgroup>
                    <optgroup label="TÓNICOS Y LOCIONES">
                        <option>Tónico</option>
                        <option>Loción</option>
                        <option>Mist - Bruma</option>
                    </optgroup>
                    <optgroup label="TRATAMIENTOS">
                        <option>Mascarilla Sheets</option>
                        <option>Mascarilla Gel</option>
                        <option>Contorno de Ojos</option>
                        <option>Crema</option>
                    </optgroup>
                    <optgroup label="PROTECCIÓN SOLAR">
                        <option>Protector Solar Crema</option>
                        <option>Protector Solar en Barra</option>
                    </optgroup>
                    <optgroup label="EXTRAS">
                        <option>Muestras</option>
                        <option>Accesorios</option>
                        <option>Papelería</option>
                    </optgroup>
                </select>
                <input type="text" id="stock-categoria-custom" placeholder="O escribe nueva categoría" style="margin-bottom: 0.5rem; display: none;">

                <input type="text" id="stock-producto" placeholder="Nombre del producto" style="margin-bottom: 0.5rem;">
                <input type="text" id="stock-codigo" placeholder="Código de barras" style="margin-bottom: 0.5rem;">
                
                <label>Imagen del Producto:</label>
                <input type="text" id="stock-imagen" placeholder="URL de la imagen (ej: https://...)" style="margin-bottom: 0.5rem;">
                <small style="display: block; color: var(--gris-oscuro); margin-bottom: 1rem;">💡 Pega la URL de la imagen del producto. Ejemplo: https://drive.google.com/uc?id=XXXXX</small>
            </div>

            <div class="card">
                <h3>Cantidad y Precios</h3>
                <label>Cantidad:</label>
                <input type="number" id="stock-cantidad" placeholder="50" min="1" style="margin-bottom: 0.5rem;">
                
                <label>Costo (€):</label>
                <input type="number" id="stock-costo" placeholder="10.50" min="0" step="0.01" style="margin-bottom: 0.5rem;">
                
                <label>Precio (€):</label>
                <input type="number" id="stock-precio" placeholder="25.00" min="0" step="0.01" style="margin-bottom: 0.5rem;">
                
                <label>Vencimiento:</label>
                <input type="date" id="stock-vencimiento" style="margin-bottom: 1rem;">

                <button class="btn btn-success btn-block" onclick="agregarStock()">➕ Agregar Stock</button>
                <div id="resultado-stock"></div>
            </div>
        </div>

        <!-- INVENTARIO -->
        <div id="inventario" class="tab-content">
            <h2 style="margin-bottom: 1rem; color: var(--cafe-intenso);">📋 Inventario</h2>

            <button class="btn btn-primary btn-block" style="margin-bottom: 1.5rem;" onclick="cargarInventario()">↔️ Recargar</button>
            <div id="lista-inventario">
                <p style="text-align: center; color: var(--gris-oscuro);">Haz clic en Recargar</p>
            </div>
        </div>

        <!-- REPORTES -->
        <div id="reportes" class="tab-content">
            <h2 style="margin-bottom: 1rem; color: var(--cafe-intenso);">📈 Reportes</h2>

            <div class="grid-2">
                <div class="card">
                    <h3>Reporte Diario</h3>
                    <button class="btn btn-primary" style="width: 100%; margin-bottom: 0.5rem;" onclick="obtenerReporteDia()">👁️ Ver</button>
                    <button class="btn btn-warning" style="width: 100%;" onclick="descargarPDF()">📥 PDF</button>
                    <div id="reporte-dia" style="margin-top: 1rem; font-size: 0.9rem;"></div>
                </div>

                <div class="card">
                    <h3>Estadísticas</h3>
                    <button class="btn btn-primary btn-block" onclick="obtenerEstadisticas()">Ver</button>
                    <div id="estadisticas" style="margin-top: 1rem; font-size: 0.9rem;"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // MARCAS Y CATEGORÍAS (precargadas)
        const MARCAS = ['COSRX', 'MIXSOON', 'ROUND LA', 'MEDICUBE', 'BEAUTY OF JOSEON', 'SKIN1004', 'MARY & MAY', 'ANUA', 'TOCOBO', 'PURITO', 'ISNTREE', 'SINK & LAB', 'DR. JART+', 'NUMBUZIN', 'VT', 'TORRIDEN', 'LASHILE BEAUTY', 'THE ORDINARY', 'INNISFREE', 'PYUNKANG YUL', 'SHINFOOD', 'SOME BY MI', 'BIODANCE', 'DR. ALTHEA', 'KLAIRS', 'AROMATICA', 'TIRTIR', 'SEOUL 1988', 'PETITFEE', 'CENTELLIAN 24+', 'HADA LABO', 'ROHTO', 'MISSHA', 'AVENE', 'PURE ELEMENT ORGANICS', 'PATCHOLOGY', 'TNTNMOMS', 'KLAVUU', 'CERAVE', 'EUCERIN'];

        const CATEGORIAS = ['Aceite Limpiador', 'Limpiador en Espuma', 'Limpiador en Bálsamo', 'Limpiador en Gel', 'Tónico', 'Loción', 'Mist - Bruma', 'Mascarilla Sheets', 'Mascarilla Gel', 'Contorno de Ojos', 'Crema', 'Protector Solar Crema', 'Protector Solar en Barra', 'Muestras', 'Accesorios', 'Papelería'];

        let scriptURL = '';
        let emailConfig = { serviceId: '', templateId: '', userId: '' };
        let isConnected = false;
        let productoSeleccionado = null;

        // INICIALIZAR
        document.addEventListener('DOMContentLoaded', function() {
            cargarConfig();
            verificarConexion();
            
            // Event listeners para detectar entrada personalizada
            document.getElementById('stock-marca').addEventListener('change', function() {
                const custom = document.getElementById('stock-marca-custom');
                if (this.value === '') {
                    custom.style.display = 'block';
                } else {
                    custom.style.display = 'none';
                    custom.value = '';
                }
            });

            document.getElementById('stock-categoria').addEventListener('change', function() {
                const custom = document.getElementById('stock-categoria-custom');
                if (this.value === '') {
                    custom.style.display = 'block';
                } else {
                    custom.style.display = 'none';
                    custom.value = '';
                }
            });
        });

        function cambiarPestana(event, nombre) {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
            document.getElementById(nombre).classList.add('active');
            if (event) event.target.classList.add('active');
        }

        function guardarConfig() {
            scriptURL = document.getElementById('script-url').value.trim();
            emailConfig.serviceId = document.getElementById('emailjs-service').value.trim();
            emailConfig.templateId = document.getElementById('emailjs-template').value.trim();
            emailConfig.userId = document.getElementById('emailjs-user').value.trim();
            
            localStorage.setItem('beauty_script_url', scriptURL);
            localStorage.setItem('beauty_emailjs_config', JSON.stringify(emailConfig));
        }

        function cargarConfig() {
            scriptURL = localStorage.getItem('beauty_script_url') || '';
            const config = localStorage.getItem('beauty_emailjs_config');
            if (config) emailConfig = JSON.parse(config);
            
            if (scriptURL) document.getElementById('script-url').value = scriptURL;
            if (emailConfig.serviceId) {
                document.getElementById('emailjs-service').value = emailConfig.serviceId;
                document.getElementById('emailjs-template').value = emailConfig.templateId;
                document.getElementById('emailjs-user').value = emailConfig.userId;
            }
        }

        function verificarConexion() {
            guardarConfig();
            if (!scriptURL) {
                actualizarEstado(false);
                return;
            }
            fetch(scriptURL + '?accion=obtener_productos')
                .then(r => r.json())
                .then(data => {
                    isConnected = data.success === true;
                    actualizarEstado(isConnected);
                })
                .catch(() => actualizarEstado(false));
        }

        function verificarEmail() {
            guardarConfig();
            if (emailConfig.serviceId && emailConfig.templateId && emailConfig.userId) {
                emailjs.init(emailConfig.userId);
                mostrarAlerta('email', '✅ EmailJS configurado', 'success');
            } else {
                mostrarAlerta('email', '⚠️ Faltan datos de EmailJS', 'error');
            }
        }

        function actualizarEstado(conectado) {
            const dot = document.getElementById('sync-dot');
            const text = document.getElementById('sync-text');
            if (conectado) {
                dot.classList.add('connected');
                text.textContent = '✅';
            } else {
                dot.classList.remove('connected');
                text.textContent = '❌';
            }
        }

        // BÚSQUEDA INTELIGENTE
        function buscarProductos() {
            if (!isConnected) {
                mostrarAlerta('busqueda', 'Configura Google Sheets primero', 'error');
                return;
            }

            const marca = document.getElementById('buscar-marca').value.trim();
            const categoria = document.getElementById('buscar-categoria').value.trim();
            const codigo = document.getElementById('buscar-codigo').value.trim();

            if (!marca && !categoria && !codigo) {
                mostrarAlerta('busqueda', 'Rellena al menos un campo', 'error');
                return;
            }

            const resultadoDiv = document.getElementById('resultado-busqueda');
            resultadoDiv.innerHTML = '<div class="loading" style="margin: 1rem auto;"></div>';

            // Construir parámetros de búsqueda
            let params = '?accion=buscar_producto';
            if (marca) params += '&marca=' + encodeURIComponent(marca);
            if (categoria) params += '&categoria=' + encodeURIComponent(categoria);
            if (codigo) params += '&codigo=' + encodeURIComponent(codigo);

            fetch(scriptURL + params)
                .then(r => r.json())
                .then(data => {
                    if (data.productos && data.productos.length > 0) {
                        resultadoDiv.innerHTML = data.productos.map(p => `
                            <div class="resultado-item">
                                <div class="resultado-imagen">
                                    ${p['Imagen URL'] ? `<img src="${p['Imagen URL']}" alt="${p['Producto']}">` : '📦'}
                                </div>
                                <div class="resultado-info">
                                    <strong>${p['Marca']}</strong>
                                    <span>${p['Producto']}</span>
                                    <small>${p['Categoría']}</small>
                                    <small>Código: ${p['Código de Barras']}</small>
                                    <div class="resultado-precio">€${p['Precio por Unidad (€)'].toFixed(2)}</div>
                                </div>
                                <div>
                                    <div class="resultado-stock ${p['Cantidad Disponible'] > 20 ? 'stock-alto' : p['Cantidad Disponible'] > 5 ? 'stock-medio' : 'stock-bajo'}">
                                        ${p['Cantidad Disponible']} unidades
                                    </div>
                                    <button class="btn btn-success" style="width: 100%; margin-top: 0.5rem;" onclick="seleccionarProducto('${p['Código de Barras']}', '${p['Marca']}', '${p['Producto']}', ${p['Precio por Unidad (€)']}, ${p['Costo Unitario (€)']})">
                                        ➕ Vender
                                    </button>
                                </div>
                            </div>
                        `).join('');
                    } else {
                        resultadoDiv.innerHTML = '<p style="text-align: center; color: var(--gris-oscuro);">No se encontraron productos</p>';
                    }
                })
                .catch(() => resultadoDiv.innerHTML = '<p style="color: var(--rojo);">Error en la búsqueda</p>');
        }

        function seleccionarProducto(codigo, marca, producto, precio, costo) {
            productoSeleccionado = {
                'Código de Barras': codigo,
                'Marca': marca,
                'Producto': producto,
                'Precio por Unidad (€)': precio,
                'Costo Unitario (€)': costo
            };

            document.getElementById('producto-venta').innerHTML = `
                <div style="width: 100%;">
                    <strong>${marca}</strong><br>
                    <p style="margin: 0.5rem 0; font-size: 0.9rem;">${producto}</p>
                    <p style="color: var(--miel); font-weight: bold;">€${precio.toFixed(2)}</p>
                </div>
            `;

            cambiarPestana(null, 'venta');
        }

        function registrarVenta() {
            if (!isConnected) {
                mostrarAlerta('venta', 'Desconectado', 'error');
                return;
            }

            if (!productoSeleccionado) {
                mostrarAlerta('venta', 'Selecciona un producto primero', 'error');
                return;
            }

            const nombre = document.getElementById('venta-nombre').value.trim();
            const email = document.getElementById('venta-email').value.trim();
            const pago = document.getElementById('venta-pago').value;
            const medio = document.getElementById('venta-medio').value;

            if (!nombre || !email || !pago || !medio) {
                mostrarAlerta('venta', 'Completa todos los campos', 'error');
                return;
            }

            const ventaData = {
                cliente: nombre,
                email: email,
                telefono: document.getElementById('venta-telefono').value,
                codigo: productoSeleccionado['Código de Barras'],
                marca: productoSeleccionado['Marca'],
                producto: productoSeleccionado['Producto'],
                cantidad: parseInt(document.getElementById('venta-cantidad').value) || 1,
                tipo: document.getElementById('venta-tipo').value,
                precio: productoSeleccionado['Precio por Unidad (€)'],
                costo: productoSeleccionado['Costo Unitario (€)'],
                pago: pago,
                medio: medio
            };

            fetch(scriptURL + '?accion=registrar_venta', {
                method: 'POST',
                body: new URLSearchParams({
                    accion: 'registrar_venta',
                    datos: JSON.stringify(ventaData)
                })
            })
            .then(r => r.json())
            .then(data => {
                if (data.success) {
                    const numeroRecibo = data.numeroRecibo || '2026001';
                    const total = data.total || (ventaData.precio * ventaData.cantidad);
                    
                    mostrarAlerta('venta', `✅ Venta #${numeroRecibo} - €${total.toFixed(2)}`, 'success');
                    
                    if (document.getElementById('enviar-email').checked && emailConfig.serviceId) {
                        enviarReciboPorEmail(nombre, email, numeroRecibo, ventaData, total);
                    }
                    
                    setTimeout(() => {
                        document.getElementById('venta-nombre').value = '';
                        document.getElementById('venta-email').value = '';
                        document.getElementById('venta-telefono').value = '';
                        document.getElementById('venta-cantidad').value = '1';
                        document.getElementById('venta-pago').value = '';
                        document.getElementById('venta-medio').value = '';
                        document.getElementById('producto-venta').innerHTML = 'Sin producto';
                        productoSeleccionado = null;
                    }, 2000);
                }
            })
            .catch(error => mostrarAlerta('venta', 'Error: ' + error, 'error'));
        }

        function enviarReciboPorEmail(cliente, email, numeroRecibo, venta, total) {
            if (!emailConfig.serviceId) return;

            const ahora = new Date();
            const fecha = ahora.toLocaleDateString('es-ES');
            const hora = ahora.toLocaleTimeString('es-ES');

            emailjs.send(
                emailConfig.serviceId,
                emailConfig.templateId,
                {
                    to_email: email,
                    to_name: cliente,
                    numero_recibo: numeroRecibo,
                    marca: venta.marca,
                    producto: venta.producto,
                    cantidad: venta.cantidad,
                    precio_unitario: venta.precio.toFixed(2),
                    total: total.toFixed(2),
                    fecha: fecha,
                    hora: hora,
                    forma_pago: venta.pago
                },
                emailConfig.userId
            ).then(
                () => console.log('✅ Email enviado'),
                (error) => console.log('❌ Error:', error)
            );
        }

        function agregarStock() {
            if (!isConnected) {
                mostrarAlerta('stock', 'Desconectado', 'error');
                return;
            }

            const marca = document.getElementById('stock-marca').value || document.getElementById('stock-marca-custom').value;
            const categoria = document.getElementById('stock-categoria').value || document.getElementById('stock-categoria-custom').value;
            const codigo = document.getElementById('stock-codigo').value.trim();

            if (!marca || !categoria || !codigo) {
                mostrarAlerta('stock', 'Completa marca, categoría y código', 'error');
                return;
            }

            const stockData = {
                codigo: codigo,
                marca: marca,
                producto: document.getElementById('stock-producto').value,
                categoria: categoria,
                imagen: document.getElementById('stock-imagen').value,
                cantidad: parseInt(document.getElementById('stock-cantidad').value) || 0,
                costo: parseFloat(document.getElementById('stock-costo').value) || 0,
                precio: parseFloat(document.getElementById('stock-precio').value) || 0,
                vencimiento: document.getElementById('stock-vencimiento').value
            };

            fetch(scriptURL + '?accion=agregar_producto', {
                method: 'POST',
                body: new URLSearchParams({
                    accion: 'agregar_producto',
                    datos: JSON.stringify(stockData)
                })
            })
            .then(r => r.json())
            .then(data => {
                if (data.success) {
                    mostrarAlerta('stock', '✅ Stock agregado!', 'success');
                    limpiarFormularioStock();
                }
            })
            .catch(error => mostrarAlerta('stock', 'Error: ' + error, 'error'));
        }

        function limpiarFormularioStock() {
            document.getElementById('stock-codigo').value = '';
            document.getElementById('stock-marca').value = '';
            document.getElementById('stock-categoria').value = '';
            document.getElementById('stock-producto').value = '';
            document.getElementById('stock-imagen').value = '';
            document.getElementById('stock-cantidad').value = '';
            document.getElementById('stock-costo').value = '';
            document.getElementById('stock-precio').value = '';
            document.getElementById('stock-vencimiento').value = '';
        }

        function cargarInventario() {
            if (!isConnected) return;
            const lista = document.getElementById('lista-inventario');
            lista.innerHTML = '<div class="loading" style="margin: 1rem auto;"></div>';

            fetch(scriptURL + '?accion=obtener_productos')
                .then(r => r.json())
                .then(data => {
                    if (data.success && data.productos) {
                        const productos = data.productos.filter(p => p['Código de Barras']);
                        if (productos.length === 0) {
                            lista.innerHTML = '<p style="text-align: center;">Sin productos</p>';
                            return;
                        }
                        lista.innerHTML = productos.map(p => `
                            <div class="resultado-item">
                                <div class="resultado-imagen">
                                    ${p['Imagen URL'] ? `<img src="${p['Imagen URL']}" alt="${p['Producto']}">` : '📦'}
                                </div>
                                <div class="resultado-info">
                                    <strong>${p['Marca']}</strong>
                                    <span>${p['Producto']}</span>
                                    <small>${p['Categoría']}</small>
                                    <div class="resultado-precio">€${p['Precio por Unidad (€)'].toFixed(2)}</div>
                                </div>
                                <div class="resultado-stock ${p['Cantidad Disponible'] > 20 ? 'stock-alto' : p['Cantidad Disponible'] > 5 ? 'stock-medio' : 'stock-bajo'}">
                                    ${p['Cantidad Disponible']} ud
                                </div>
                            </div>
                        `).join('');
                    }
                })
                .catch(() => lista.innerHTML = '<p style="color: var(--rojo);">Error</p>');
        }

        function obtenerReporteDia() {
            if (!isConnected) return;
            const div = document.getElementById('reporte-dia');
            div.innerHTML = '<div class="loading"></div>';
            
            const hoy = new Date().toLocaleDateString('es-ES');
            fetch(scriptURL + '?accion=obtener_reporte_dia&fecha=' + encodeURIComponent(hoy))
                .then(r => r.json())
                .then(data => {
                    if (data.success) {
                        const r = data.reporte;
                        div.innerHTML = `<strong>Ventas:</strong> ${r.totalVentas}<br><strong>Ingresos:</strong> €${r.totalIngresos.toFixed(2)}<br><strong style="color: var(--verde);">Ganancia:</strong> €${r.ganancia.toFixed(2)}`;
                    }
                })
                .catch(() => div.innerHTML = '<p style="color: var(--rojo);">Error</p>');
        }

        function descargarPDF() {
            if (!isConnected) return;
            const hoy = new Date().toLocaleDateString('es-ES');
            fetch(scriptURL + '?accion=obtener_reporte_dia&fecha=' + encodeURIComponent(hoy))
                .then(r => r.json())
                .then(data => {
                    if (data.success) {
                        const r = data.reporte;
                        const html = `<h2 style="text-align: center;">Beauty Of Novella</h2><h3 style="text-align: center;">Reporte ${hoy}</h3><table border="1" cellpadding="12" style="width: 100%;"><tr><td><strong>Concepto</strong></td><td><strong>Valor</strong></td></tr><tr><td>Ventas</td><td>${r.totalVentas}</td></tr><tr><td>Ingresos</td><td>€${r.totalIngresos.toFixed(2)}</td></tr><tr><td>Costos</td><td>€${r.totalCostos.toFixed(2)}</td></tr><tr style="background: #34a853; color: white;"><td><strong>Ganancia</strong></td><td><strong>€${r.ganancia.toFixed(2)}</strong></td></tr></table>`;
                        html2pdf().set({margin: 15, filename: `Reporte-${hoy}.pdf`, html2canvas: {scale: 2}, jsPDF: {orientation: 'portrait', unit: 'mm', format: 'a4'}}).fromHtml(html).save();
                    }
                });
        }

        function obtenerEstadisticas() {
            if (!isConnected) return;
            const div = document.getElementById('estadisticas');
            div.innerHTML = '<div class="loading"></div>';

            Promise.all([
                fetch(scriptURL + '?accion=obtener_productos').then(r => r.json()),
                fetch(scriptURL + '?accion=obtener_ventas').then(r => r.json()),
                fetch(scriptURL + '?accion=obtener_clientes').then(r => r.json())
            ])
            .then(([prods, ventas, clientes]) => {
                const prodCount = prods.productos ? prods.productos.filter(p => p['Código de Barras']).length : 0;
                const ventCount = ventas.ventas ? ventas.ventas.filter(v => v['Número Recibo']).length : 0;
                const cliCount = clientes.clientes ? clientes.clientes.filter(c => c['Nombre']).length : 0;
                div.innerHTML = `<strong>📦 Productos:</strong> ${prodCount}<br><strong>🛒 Ventas:</strong> ${ventCount}<br><strong>👥 Clientes:</strong> ${cliCount}`;
            })
            .catch(() => div.innerHTML = '<p style="color: var(--rojo);">Error</p>');
        }

        function mostrarAlerta(elemento, mensaje, tipo) {
            const resultado = document.getElementById(`resultado-${elemento}`);
            if (resultado) {
                resultado.innerHTML = `<div class="result ${tipo}">${mensaje}</div>`;
                setTimeout(() => resultado.innerHTML = '', 5000);
            }
        }
    </script>
</body>
</html>
