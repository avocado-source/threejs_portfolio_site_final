[index.html](https://github.com/user-attachments/files/24016200/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Portfolio Site for 3D Designer</title>
    <style>
        body { margin: 0; padding: 0; background-color: #111; font-family: 'Segoe UI', sans-serif; overflow: hidden; }
        
        #launcher-menu {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            background: linear-gradient(135deg, #1a1a1a 0%, #0d0d0d 100%);
            z-index: 10; transition: opacity 0.5s;
        }

        h1 { color: white; font-weight: 300; letter-spacing: 2px; margin-bottom: 50px; text-transform: uppercase; border-bottom: 1px solid #444; padding-bottom: 10px; }

        .card-container { display: flex; gap: 30px; }

        .app-card {
            width: 260px; height: 340px;
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 16px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            padding: 20px;
            position: relative; overflow: hidden;
        }

        .app-card:hover {
            transform: translateY(-10px);
            background: rgba(255,255,255,0.1);
            box-shadow: 0 15px 30px rgba(0,0,0,0.5);
            border-color: rgba(255,255,255,0.3);
        }

        .app-card h2 { color: #fff; margin: 0; font-size: 1.6em; text-align: center; }

        .app-card::before {
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 4px;
            background: #555; transition: 0.3s;
        }
        .card-studio:hover::before { background: #4caf50; }
        .card-anim:hover::before { background: #2196F3; }

        #app-frame {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            border: none; display: none; z-index: 5; background: #222;
        }

        #back-btn {
            position: fixed; bottom: 20px; left: 20px; z-index: 1000;
            background: rgba(0, 0, 0, 0.8); color: white;
            border: 1px solid rgba(255,255,255,0.2);
            padding: 10px 20px; border-radius: 30px;
            cursor: pointer; font-weight: bold;
            display: none; transition: 0.2s;
            backdrop-filter: blur(5px);
        }
        #back-btn:hover { background: #d32f2f; border-color: #ff5252; }
    </style>
</head>
<body>

    <div id="launcher-menu">
        <h1>Portfolio Site for 3D Designer</h1>
        <div class="card-container">
            <div class="app-card card-studio" onclick="launchApp('code-studio')">
                <h2>3D Modeling Studio</h2>
            </div>

            <div class="app-card card-anim" onclick="launchApp('code-anim')">
                <h2>Animation Studio</h2>
            </div>
        </div>
    </div>

    <iframe id="app-frame"></iframe>
    <button id="back-btn" onclick="goBack()">← Back to Menu</button>

<textarea id="code-studio" style="display:none;">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>3D Studio Viewer</title>
    <style>
        body { margin: 0; overflow: hidden; background-color: #222; }
        
        .info-panel {
            position: absolute; top: 20px; left: 20px; z-index: 100;
            color: white; font-family: 'Segoe UI', sans-serif;
            background: rgba(0,0,0,0.85); padding: 20px; border-radius: 12px; 
            width: 280px; backdrop-filter: blur(10px);
            user-select: none;
            box-shadow: 0 8px 32px rgba(0,0,0,0.5);
            max-height: 90vh; overflow-y: auto;
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        .info-panel::-webkit-scrollbar { width: 6px; }
        .info-panel::-webkit-scrollbar-track { background: transparent; }
        .info-panel::-webkit-scrollbar-thumb { background: #555; border-radius: 3px; }

        .info-panel h3 { margin: 0 0 15px 0; font-size: 1.2em; border-bottom: 1px solid #555; padding-bottom: 10px; font-weight: 600;}
        
        .control-section { margin-bottom: 20px; padding-bottom: 15px; border-bottom: 1px solid #444; }
        .control-section:last-child { border-bottom: none; margin-bottom: 0; padding-bottom: 0; }
        
        .section-title { font-size: 0.8em; color: #aaa; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 10px; display: block; font-weight: 700; }
        
        .radio-group { display: flex; flex-direction: column; gap: 8px; }
        .radio-label { display: flex; align-items: center; cursor: pointer; font-size: 0.95em; padding: 6px; border-radius: 4px; transition: 0.2s; }
        .radio-label:hover { background: rgba(255,255,255,0.1); }
        .radio-label input { margin-right: 10px; accent-color: #4caf50; }

        input[type="file"] { display: none; }
        .file-upload-label {
            display: block; width: 100%; padding: 12px; 
            background: #333; border: 1px dashed #666; color: #ccc;
            text-align: center; border-radius: 6px; cursor: pointer; box-sizing: border-box;
            transition: 0.2s; font-size: 0.9em;
        }
        .file-upload-label:hover { background: #444; border-color: #999; color: white; }

        .action-btn {
            width: 100%; padding: 10px; margin-top: 5px;
            background: #555; border: none; color: white; border-radius: 6px;
            cursor: pointer; font-weight: bold; transition: 0.2s;
        }
        .action-btn:hover { background: #666; }
        .add-light-btn { background: #2196F3; margin-top: 10px; }
        .add-light-btn:hover { background: #1976D2; }

        .btn-group { display: flex; gap: 5px; }
        .mode-btn {
            flex: 1; padding: 10px; background: #3a3a3a; border: 1px solid #555; color: #ddd;
            border-radius: 6px; cursor: pointer; transition: 0.2s; font-size: 0.9em;
        }
        .mode-btn.active { background: #4caf50; color: white; border-color: #4caf50; font-weight: bold; }
        
        #custom-controls { display: none; margin-top: 10px; padding-top: 10px; border-top: 1px dashed #444; }

        /* Rotate Controls */
        .rotate-wrapper { display: flex; align-items: center; gap: 8px; margin-top: 5px; }
        input[type=range] { flex: 1; cursor: pointer; accent-color: #2196F3; }

        /* Annotation Styles */
        .annotation-container {
            position: absolute;
            pointer-events: none; 
            transform: translate(-50%, -50%);
        }
        
        .annotation-marker {
            width: 14px; height: 14px; 
            background: #ffea00; border: 2px solid white; border-radius: 50%;
            cursor: pointer; pointer-events: auto; 
            box-shadow: 0 0 8px rgba(0,0,0,0.5);
            transition: transform 0.2s;
        }
        .annotation-marker:hover { transform: scale(1.2); }

        .annotation-input {
            position: absolute; top: 50%; left: 20px;
            transform: translateY(-50%);
            background: rgba(0,0,0,0.85); color: white; border: 1px solid #666;
            padding: 5px 10px; border-radius: 4px; font-size: 0.9em;
            outline: none; width: 150px; pointer-events: auto;
        }
        .annotation-input::placeholder { color: #aaa; }

    </style>
</head>
<body>

    <div class="info-panel">
        <h3>3D Studio</h3>

        <div class="control-section">
            <span class="section-title">Camera Angles</span>
            <div class="btn-group">
                <button class="mode-btn" onclick="setCamera('front')">Front</button>
                <button class="mode-btn" onclick="setCamera('side')">Side</button>
                <button class="mode-btn" onclick="setCamera('iso')">ISO</button>
            </div>
        </div>

        <div class="control-section">
            <span class="section-title">Auto Rotate</span>
            <div class="rotate-wrapper">
                <button id="btn-rotate-studio" class="mode-btn" style="flex:0.4;" onclick="toggleRotate()">Off</button>
                <input type="range" min="-10" max="10" value="2" step="0.5" oninput="changeRotateSpeed(this.value)">
            </div>
            <div style="font-size:0.75em; color:#aaa; text-align:right; margin-top:2px;">
                Speed: <span id="rotate-val">2.0</span>
            </div>
        </div>

        <div class="control-section">
            <span class="section-title">1. Model Upload</span>
            <label for="model-input" class="file-upload-label">Open Model (.glb / .fbx)</label>
            <input type="file" id="model-input" accept=".glb, .gltf, .fbx">
        </div>

        <div class="control-section">
            <span class="section-title">2. Background & HDRi</span>
            <div class="radio-group">
                <label class="radio-label">
                    <input type="radio" name="bgMode" value="hdr" checked onchange="changeBackground('hdr')">
                    Default HDRi
                </label>
                <label class="radio-label">
                    <input type="radio" name="bgMode" value="grey" onchange="changeBackground('grey')">
                    No HDRi
                </label>
            </div>
            
            <label for="hdr-input" class="file-upload-label" style="margin-top:10px; padding:8px; font-size:0.8em;">Upload Custom HDR</label>
            <input type="file" id="hdr-input" accept=".hdr">
        </div>

        <div class="control-section">
            <span class="section-title">3. Lighting Setup</span>
            <div class="radio-group">
                <label class="radio-label">
                    <input type="radio" name="lightMode" value="none" onchange="changeLightMode('none')">
                    No Lights
                </label>
                <label class="radio-label">
                    <input type="radio" name="lightMode" value="basic" onchange="changeLightMode('basic')">
                    Basic Lights
                </label>
                <label class="radio-label">
                    <input type="radio" name="lightMode" value="custom" checked onchange="changeLightMode('custom')">
                    Custom Lights
                </label>
            </div>
            
            <div id="custom-controls">
                <button class="action-btn add-light-btn" onclick="addNewLight()">+ Add Light</button>
            </div>
        </div>

        <div class="control-section">
            <span class="section-title">4. View Mode</span>
            <div class="btn-group">
                <button class="mode-btn active" onclick="setViewMode('original', this)">Original</button>
                <button class="mode-btn" onclick="setViewMode('clay', this)">Clay</button>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/controls/TransformControls.js"></script> 
    <script src="https://unpkg.com/three@0.128.0/examples/js/loaders/GLTFLoader.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/loaders/FBXLoader.js"></script>
    <script src="https://unpkg.com/fflate@0.8.0/umd/index.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/loaders/DataTextureLoader.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/loaders/RGBELoader.js"></script>
    <script src="https://unpkg.com/lil-gui@0.17.0/dist/lil-gui.umd.min.js"></script>

    <script>
        const params = {
            envIntensity: 1.0,
            bgBlur: 0.0,
            showBg: true,
            exposure: 1.0
        };

        let currentModel = null;
        let mixer = null;
        let hdrTexture = null; 
        let isHdrVisible = true;
        let currentLightMode = 'custom'; 
        let selectedLightMesh = null;
        let lightObjects = []; 
        let basicLights = [];
        let currentViewMode = 'original';
        let originalMaterials = {};

        let annotations = [];

        const clock = new THREE.Clock();
        const gltfLoader = new THREE.GLTFLoader();
        const fbxLoader = new THREE.FBXLoader();
        const rgbeLoader = new THREE.RGBELoader();
        const gui = new lil.GUI({ title: 'Environment Settings' });

        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x333333); 

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 2000);
        camera.position.set(0, 3, 8);

        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.outputEncoding = THREE.sRGBEncoding;
        renderer.toneMapping = THREE.ACESFilmicToneMapping;
        renderer.toneMappingExposure = 1.0;
        renderer.shadowMap.enabled = true;
        renderer.shadowMap.type = THREE.PCFSoftShadowMap;
        document.body.appendChild(renderer.domElement);

        const orbit = new THREE.OrbitControls(camera, renderer.domElement);
        orbit.enableDamping = true;
        orbit.autoRotate = false;
        orbit.autoRotateSpeed = 2.0;

        const transformControl = new THREE.TransformControls(camera, renderer.domElement);
        transformControl.addEventListener('dragging-changed', (e) => orbit.enabled = !e.value);
        scene.add(transformControl);

        window.setCamera = function(view) {
            // Disable rotation when changing views manually
            orbit.autoRotate = false;
            updateRotateBtn();

            switch(view) {
                case 'front': camera.position.set(0, 1.5, 6); break;
                case 'side': camera.position.set(6, 1.5, 0); break;
                case 'iso': camera.position.set(4, 4, 4); break;
            }
            orbit.target.set(0, 1, 0);
            orbit.update();
        }

        // Auto Rotate Logic
        window.toggleRotate = function() {
            orbit.autoRotate = !orbit.autoRotate;
            updateRotateBtn();
        }

        window.changeRotateSpeed = function(val) {
            orbit.autoRotateSpeed = parseFloat(val);
            document.getElementById('rotate-val').innerText = val;
        }

        function updateRotateBtn() {
            const btn = document.getElementById('btn-rotate-studio');
            if(orbit.autoRotate) {
                btn.innerText = "On";
                btn.classList.add('active');
            } else {
                btn.innerText = "Off";
                btn.classList.remove('active');
            }
        }

        const pmremGenerator = new THREE.PMREMGenerator(renderer);
        pmremGenerator.compileEquirectangularShader();

        const defaultHDR = 'https://dl.polyhaven.org/file/ph-assets/HDRIs/hdr/1k/brown_photostudio_02_1k.hdr';

        function loadHDR(url) {
            rgbeLoader.setDataType(THREE.UnsignedByteType);
            
            rgbeLoader.load(url, function(texture) {
                const envMap = pmremGenerator.fromEquirectangular(texture).texture;
                hdrTexture = envMap;
                
                if (isHdrVisible) {
                    scene.background = hdrTexture;
                    scene.environment = hdrTexture;
                }
                
                texture.dispose();
                pmremGenerator.dispose();
            }, undefined, function(err) {
                changeBackground('grey');
                document.querySelector('input[name="bgMode"][value="grey"]').checked = true;
            });
        }
        loadHDR(defaultHDR);

        window.changeBackground = function(mode) {
            if (mode === 'hdr') {
                isHdrVisible = true;
                if (hdrTexture) {
                    scene.background = hdrTexture;
                    scene.environment = hdrTexture;
                } else {
                    loadHDR(defaultHDR);
                }
            } else {
                isHdrVisible = false;
                scene.background = new THREE.Color(0x333333); 
                scene.environment = null; 
            }
        };

        document.getElementById('hdr-input').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;
            const url = URL.createObjectURL(file);
            loadHDR(url);
            document.querySelector('input[name="bgMode"][value="hdr"]').checked = true;
            isHdrVisible = true;
        });

        gui.add(params, 'exposure', 0, 2).name('Exposure').onChange(v => {
            renderer.toneMappingExposure = v;
        });

        gui.add(params, 'envIntensity', 0, 2).name('Env Intensity').onChange(v => {
            scene.traverse(child => {
                if (child.isMesh && child.material && child.material.isMeshStandardMaterial) {
                    child.material.envMapIntensity = v;
                }
            });
        });

        gui.add(params, 'showBg').name('Show Background').onChange(v => {
            if (isHdrVisible) {
                scene.background = v ? hdrTexture : new THREE.Color(0x222222);
            }
        });

        let lightGui = null; 

        function clearLights() {
            lightObjects.forEach(mesh => {
                scene.remove(mesh);
                if(mesh.userData.helper) scene.remove(mesh.userData.helper);
            });
            lightObjects = [];

            basicLights.forEach(light => scene.remove(light));
            basicLights = [];

            transformControl.detach();
            if(lightGui) { lightGui.destroy(); lightGui = null; }
            selectedLightMesh = null;
        }

        window.changeLightMode = function(mode) {
            currentLightMode = mode;
            clearLights();
            
            const customControls = document.getElementById('custom-controls');
            
            if (mode === 'none') {
                customControls.style.display = 'none';
            } else if (mode === 'basic') {
                customControls.style.display = 'none';
                
                const hemi = new THREE.HemisphereLight(0xffffff, 0x444444, 1.0);
                hemi.position.set(0, 20, 0);
                scene.add(hemi);
                
                const dir = new THREE.DirectionalLight(0xffffff, 1.5);
                dir.position.set(5, 10, 7);
                dir.castShadow = true;
                scene.add(dir);
                basicLights.push(hemi, dir);

            } else if (mode === 'custom') {
                customControls.style.display = 'block';
                createInteractiveLight('Key Light', 0xffffff, 1.5, 5, 5, 5);
                createInteractiveLight('Fill Light', 0xffffee, 0.5, -5, 3, 5);
                createInteractiveLight('Rim Light', 0xccccff, 2.0, 0, 5, -5);
                
                const ambient = new THREE.AmbientLight(0x222222);
                scene.add(ambient);
                basicLights.push(ambient);
            }
        };

        window.addNewLight = function() {
            const x = (Math.random() - 0.5) * 10;
            const z = (Math.random() - 0.5) * 10 + 5;
            const id = lightObjects.length + 1;
            createInteractiveLight(`Light ${id}`, 0xffffff, 1.0, x, 5, z);
        };

        function createInteractiveLight(name, color, intensity, x, y, z) {
            const bulbGeo = new THREE.SphereGeometry(0.4, 16, 16);
            const bulbMat = new THREE.MeshBasicMaterial({ color: color });
            const bulb = new THREE.Mesh(bulbGeo, bulbMat);
            
            bulb.position.set(x, y, z);
            bulb.lookAt(0, 0, 0); 
            
            bulb.userData = { isLightHandle: true, name: name };
            scene.add(bulb);

            const light = new THREE.SpotLight(color, intensity);
            light.angle = Math.PI / 6;
            light.penumbra = 0.3;
            light.castShadow = true;
            
            bulb.add(light);
            bulb.add(light.target);
            light.target.position.set(0, 0, 5);

            lightObjects.push(bulb);

            const helper = new THREE.SpotLightHelper(light);
            helper.visible = false; 
            scene.add(helper);
            
            bulb.userData.light = light;
            bulb.userData.helper = helper; 
        }

        changeLightMode('custom');

        const raycaster = new THREE.Raycaster();
        const mouse = new THREE.Vector2();

        function addAnnotation(position) {
            const container = document.createElement('div');
            container.className = 'annotation-container';
            
            const marker = document.createElement('div');
            marker.className = 'annotation-marker';
            
            const input = document.createElement('input');
            input.className = 'annotation-input';
            input.placeholder = "Enter text...";
            input.addEventListener('keydown', (e) => e.stopPropagation()); 
            input.addEventListener('keyup', (e) => {
                if(e.key === 'Enter') input.blur();
                e.stopPropagation();
            });

            container.appendChild(marker);
            container.appendChild(input);
            document.body.appendChild(container);

            marker.addEventListener('contextmenu', (e) => {
                e.preventDefault();
                document.body.removeChild(container);
                annotations = annotations.filter(a => a.container !== container);
            });

            annotations.push({
                position: position,
                container: container
            });
            
            updateAnnotations();
            setTimeout(() => input.focus(), 50);
        }

        renderer.domElement.addEventListener('dblclick', function(event) {
            if (!currentModel) return;

            mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
            mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

            raycaster.setFromCamera(mouse, camera);
            const intersects = raycaster.intersectObject(currentModel, true);

            if (intersects.length > 0) {
                const p = intersects[0].point;
                addAnnotation(p);
            }
        });

        renderer.domElement.addEventListener('pointerdown', function(event) {
            if (transformControl.dragging) return;

            mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
            mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

            raycaster.setFromCamera(mouse, camera);

            const clickableLights = lightObjects.filter(obj => obj.isMesh);
            const lightIntersects = raycaster.intersectObjects(clickableLights);

            if (lightIntersects.length > 0 && currentLightMode === 'custom') {
                const clickedMesh = lightIntersects[0].object;
                if (selectedLightMesh && selectedLightMesh !== clickedMesh) {
                    selectedLightMesh.userData.helper.visible = false;
                }
                selectedLightMesh = clickedMesh;
                selectedLightMesh.userData.helper.visible = true; 
                transformControl.attach(selectedLightMesh);
                updateGUI(selectedLightMesh);
                return;
            }

            if (currentModel) {
                const modelIntersects = raycaster.intersectObject(currentModel, true);
                if (modelIntersects.length > 0) {
                     if (selectedLightMesh) {
                        selectedLightMesh.userData.helper.visible = false;
                        selectedLightMesh = null;
                        if(lightGui) { lightGui.destroy(); lightGui = null; }
                    }
                    transformControl.attach(currentModel);
                    return;
                }
            }

            transformControl.detach();
            if(lightGui) { lightGui.destroy(); lightGui = null; }
            if (selectedLightMesh) {
                selectedLightMesh.userData.helper.visible = false;
                selectedLightMesh = null;
            }
        });

        let currentColorObj = { color: '#ffffff' };
        function updateGUI(mesh) {
            if(lightGui) lightGui.destroy();
            lightGui = new lil.GUI({ title: mesh.userData.name });
            
            const light = mesh.userData.light;
            currentColorObj.color = '#' + light.color.getHexString();

            lightGui.add(light, 'intensity', 0, 10).name('Intensity');
            lightGui.addColor(currentColorObj, 'color').name('Color').onChange((val) => {
                light.color.set(val);
                mesh.material.color.set(val);
            });
            lightGui.add(light, 'angle', 0, Math.PI/2).name('Angle').onChange(() => mesh.userData.helper.update());
            lightGui.add(light.shadow, 'bias', -0.005, 0.005).name('Shadow Bias');
            
            lightGui.add({ remove: () => {
                scene.remove(mesh);
                scene.remove(mesh.userData.helper);
                lightObjects = lightObjects.filter(l => l !== mesh);
                transformControl.detach();
                if(lightGui) { lightGui.destroy(); lightGui = null; }
            }}, 'remove').name('Remove Light');
        }

        window.addEventListener('keydown', (e) => {
            if(e.target.tagName === 'INPUT') return; 
            switch(e.key.toLowerCase()) {
                case 'w': transformControl.setMode('translate'); break;
                case 'e': transformControl.setMode('rotate'); break;
                case 'r': transformControl.setMode('scale'); break;
            }
        });

        const clayMaterial = new THREE.MeshStandardMaterial({ 
            color: 0xcccccc, roughness: 0.4, metalness: 0.1 
        });

        function backupMaterials(model) {
            originalMaterials = {};
            model.traverse(child => {
                if (child.isMesh) originalMaterials[child.uuid] = child.material;
            });
        }

        window.setViewMode = function(mode, btnElement) {
            currentViewMode = mode;
            document.querySelectorAll('.mode-btn').forEach(btn => btn.classList.remove('active'));
            if(btnElement) btnElement.classList.add('active');

            if (!currentModel) return;

            currentModel.traverse(child => {
                if (child.isMesh) {
                    if (mode === 'clay') {
                        child.material = clayMaterial;
                        child.castShadow = true;
                        child.receiveShadow = true;
                    } else {
                        if (originalMaterials[child.uuid]) child.material = originalMaterials[child.uuid];
                    }
                }
            });
        }

        document.getElementById('model-input').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;
            const url = URL.createObjectURL(file);
            const ext = file.name.toLowerCase();

            const onLoad = (model, anims) => {
                if (currentModel) scene.remove(currentModel);
                currentModel = model;
                backupMaterials(currentModel);
                
                currentModel.traverse(n => {
                    if (n.isMesh) {
                        n.castShadow = true;
                        n.receiveShadow = true;
                        if(n.material.isMeshStandardMaterial) n.material.envMapIntensity = params.envIntensity;
                    }
                });
                scene.add(currentModel);

                if (anims && anims.length) {
                    mixer = new THREE.AnimationMixer(currentModel);
                    mixer.clipAction(anims[0]).play();
                }

                const box = new THREE.Box3().setFromObject(currentModel);
                const size = box.getSize(new THREE.Vector3());
                const center = box.getCenter(new THREE.Vector3());
                currentModel.position.sub(center);
                currentModel.position.y += size.y / 2;

                window.setViewMode(currentViewMode, null);
            };

            if (ext.endsWith('glb') || ext.endsWith('gltf')) gltfLoader.load(url, (g) => onLoad(g.scene, g.animations));
            else if (ext.endsWith('fbx')) fbxLoader.load(url, (o) => onLoad(o, o.animations));
        });

        function updateAnnotations() {
            annotations.forEach(item => {
                const vector = item.position.clone();
                vector.project(camera);

                if (vector.z > 1) {
                    item.container.style.display = 'none';
                } else {
                    item.container.style.display = 'block';
                    const x = (vector.x * .5 + .5) * window.innerWidth;
                    const y = (-(vector.y * .5) + .5) * window.innerHeight;
                    
                    item.container.style.left = `${x}px`;
                    item.container.style.top = `${y}px`;
                }
            });
        }

        function animate() {
            requestAnimationFrame(animate);
            const delta = clock.getDelta();
            if (mixer) mixer.update(delta);
            
            lightObjects.forEach(obj => {
                if(obj.isMesh && obj.userData.helper && obj.userData.helper.visible) {
                    obj.userData.helper.update();
                }
            });

            updateAnnotations();

            orbit.update();
            renderer.render(scene, camera);
        }
        animate();

        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
    </textarea>

<textarea id="code-anim" style="display:none;">
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Animation Portfolio - Wireframe</title>
    <style>
        body { margin: 0; overflow: hidden; background-color: #222; font-family: 'Segoe UI', sans-serif; }
        
        .info-panel {
            position: absolute; top: 20px; left: 20px; z-index: 100;
            color: white; 
            background: rgba(0,0,0,0.85); padding: 20px; border-radius: 12px; 
            width: 320px; backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0,0,0,0.5);
            border: 1px solid rgba(255,255,255,0.1);
            max-height: 90vh; overflow-y: auto;
        }
        h3 { margin: 0 0 10px 0; font-size: 1.1em; color: #fff; border-bottom: 1px solid #555; padding-bottom: 8px;}
        h4 { margin: 15px 0 8px 0; font-size: 0.9em; color: #aaa; text-transform: uppercase; letter-spacing: 1px; }

        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 15px; }
        .cam-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 5px; margin-bottom: 10px; }

        .avatar-btn, .cam-btn {
            background: #444; border: 2px solid #555; color: #ddd;
            padding: 8px; border-radius: 8px; cursor: pointer;
            transition: 0.2s; font-weight: bold; font-size: 0.85em;
        }
        .avatar-btn:hover, .cam-btn:hover { background: #555; border-color: #888; color: white; }
        .avatar-btn.active, .cam-btn.active { background: #4caf50; border-color: #4caf50; color: white; }

        .upload-btn {
            display: block; width: 100%; padding: 12px; margin-bottom: 10px; box-sizing: border-box;
            background: #333; border: 1px dashed #777; color: #ccc;
            text-align: center; border-radius: 6px; cursor: pointer; transition: 0.2s;
        }
        .upload-btn:hover { background: #444; border-color: #fff; color: #fff; }
        
        .custom-section { border-top: 1px solid #444; padding-top: 10px; margin-top: 10px; }

        input[type="file"] { display: none; }

        .keypose-panel {
            position: absolute; top: 100px; right: 20px; z-index: 100;
            color: white; 
            background: rgba(0,0,0,0.85); padding: 20px; border-radius: 12px; 
            width: 200px; backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0,0,0,0.5);
            border: 1px solid rgba(255,255,255,0.1);
            max-height: 80vh; overflow-y: auto;
        }

        .saved-pose {
            background: #444; border: 1px solid #666; 
            padding: 8px; margin-top: 5px; border-radius: 4px;
            cursor: pointer; display: flex; justify-content: space-between;
            align-items: center; transition: 0.2s; position: relative;
        }
        .saved-pose:hover { background: #555; border-color: #4caf50; }
        .del-btn { background: none; border: none; color: #ff5555; cursor: pointer; font-weight: bold; margin-left:10px; }
        
        .pose-info { flex: 1; display: flex; align-items: center; overflow: hidden; white-space: nowrap; }
        .pose-text { margin-left: 5px; color: #aaa; font-style: italic; cursor: text; flex: 1; overflow: hidden; text-overflow: ellipsis; min-height: 20px;}
        .pose-text:hover { color: white; }
        .pose-text-input { background: #222; color: white; border: 1px solid #666; width: 100%; border-radius: 3px; font-size: 0.9em; padding: 2px; }

        .control-bar { margin-top: 20px; padding-top: 15px; border-top: 1px solid #444; }
        .slider-container { display: flex; align-items: center; gap: 10px; margin-bottom: 10px; }
        input[type=range] { flex: 1; cursor: pointer; accent-color: #2196F3; }
        
        .btn-row { display: flex; gap: 5px; }
        .ctrl-btn { flex: 1; padding: 8px; background: #444; border: none; color: white; border-radius: 4px; cursor: pointer; }
        .ctrl-btn:hover { background: #666; }
        
        #anim-name { font-size: 0.9em; color: #4caf50; margin-bottom: 10px; font-weight: bold; min-height: 20px;}
        #frame-info {
            position: absolute; top: 20px; right: 20px; z-index: 100; 
            color: #00ff00; font-family: 'Courier New', monospace; font-weight: bold; 
            background: rgba(0,0,0,0.6); padding: 10px; border-radius: 6px; pointer-events: none;
        }
        
        .rotate-wrapper { display: flex; align-items: center; gap: 8px; margin-bottom: 5px; }
        
    </style>
</head>
<body>

    <div id="frame-info">Frame: <span id="frame-display">0</span></div>

    <div class="keypose-panel">
        <h3>Key Poses</h3>
        <button class="ctrl-btn" style="width:100%; background:#2196F3;" onclick="saveKeyPose()">+ Save Current</button>
        <div id="keypose-list" style="margin-top: 15px;"></div>
    </div>

    <div class="info-panel">
        <h3>Animation Portfolio</h3>
        
        <div class="custom-section" style="margin-top:0; border-top:none;">
            <h4>Camera Angles</h4>
            <div class="cam-grid">
                <button class="cam-btn" onclick="setCamera('front')">Front</button>
                <button class="cam-btn" onclick="setCamera('side')">Side</button>
                <button class="cam-btn" onclick="setCamera('iso')">ISO</button>
            </div>
            
            <div style="margin-top:10px; border-top:1px dashed #444; padding-top:10px;">
                <span style="font-size:0.8em; color:#aaa; font-weight:bold; display:block; margin-bottom:5px;">AUTO ROTATE</span>
                <div class="rotate-wrapper">
                    <button class="ctrl-btn" id="btn-rotate" style="flex:0.4;" onclick="toggleAutoRotate()">Off</button>
                    <input type="range" min="-10" max="10" value="2" step="0.5" oninput="changeRotateSpeed(this.value)">
                </div>
                <div style="font-size:0.75em; color:#aaa; text-align:right;">
                    Speed: <span id="rotate-val">2.0</span>
                </div>
            </div>
        </div>

        <h4>1. Default Avatar</h4>
        <div class="btn-grid">
            <button class="avatar-btn active" id="btn-female" onclick="selectDefault('female')">
                Female<br><span style="font-size:0.7em; font-weight:normal;">(X Bot)</span>
            </button>
            <button class="avatar-btn" id="btn-male" onclick="selectDefault('male')">
                Male<br><span style="font-size:0.7em; font-weight:normal;">(Y Bot)</span>
            </button>
        </div>

        <div class="custom-section">
            <h4>2. Custom Upload</h4>
            <label class="upload-btn">
                Upload Own Character
                <input type="file" id="char-input" accept=".glb, .gltf, .fbx">
            </label>
        </div>

        <div class="custom-section">
            <h4>3. Animation</h4>
            <label class="upload-btn" style="border-style: solid; border-color: #4caf50; color:#4caf50;">
                Apply Animation File
                <input type="file" id="anim-input" accept=".glb, .gltf, .fbx">
            </label>
        </div>

        <div class="control-bar">
            <div id="anim-name">Ready</div>
            
            <div class="slider-container">
                <span style="font-size:0.8em">Progress</span>
                <input type="range" id="progress-bar" min="0" max="100" value="0" step="0.1">
            </div>

            <div class="slider-container">
                <span style="font-size:0.8em">Speed (x<span id="speed-val">1.0</span>)</span>
                <input type="range" id="time-scale" min="0" max="2" value="1" step="0.1">
            </div>

            <div class="btn-row">
                <button class="ctrl-btn" id="btn-play">Play</button>
                <button class="ctrl-btn" id="btn-wireframe" onclick="toggleWireframeMode()">Wireframe</button>
                <button class="ctrl-btn" id="btn-skeleton" onclick="toggleSkeleton()">Skeleton</button>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/loaders/GLTFLoader.js"></script>
    <script src="https://unpkg.com/three@0.128.0/examples/js/loaders/FBXLoader.js"></script>
    <script src="https://unpkg.com/fflate@0.8.0/umd/index.js"></script>

    <script>
        const DEFAULTS = {
            female: 'https://cdn.jsdelivr.net/gh/avocado-source/mixamo_default@main/X%20Bot.fbx',
            male:   'https://cdn.jsdelivr.net/gh/avocado-source/mixamo_default@main/Y%20Bot.fbx'
        };

        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x333333);
        
        const grid = new THREE.GridHelper(10, 10, 0x555555, 0x444444);
        scene.add(grid);

        const camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, 0.1, 1000);
        camera.position.set(0, 1.5, 4);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.outputEncoding = THREE.sRGBEncoding;
        renderer.shadowMap.enabled = true;
        document.body.appendChild(renderer.domElement);

        const controls = new THREE.OrbitControls(camera, renderer.domElement);
        controls.target.set(0, 1, 0);
        controls.enableDamping = true;
        controls.autoRotate = false;
        controls.autoRotateSpeed = 2.0;

        const hemiLight = new THREE.HemisphereLight(0xffffff, 0x444444, 1.2);
        hemiLight.position.set(0, 20, 0);
        scene.add(hemiLight);

        const dirLight = new THREE.DirectionalLight(0xffffff, 1.0);
        dirLight.position.set(3, 10, 10);
        dirLight.castShadow = true;
        scene.add(dirLight);

        let characterModel = null;
        let mixer = null;
        let currentAction = null;
        
        let skeletonHelper = null;
        let isSkeletonVisible = false;

        let isPlaying = false;
        let cachedAnimClip = null;
        let isUserAnimation = false;

        // Key Poses Array
        let savedKeyPoses = [];
        let poseCounter = 0;
        
        const clock = new THREE.Clock();
        const gltfLoader = new THREE.GLTFLoader();
        const fbxLoader = new THREE.FBXLoader();

        window.toggleSkeleton = function() {
            if(!skeletonHelper) return;
            isSkeletonVisible = !isSkeletonVisible;
            skeletonHelper.visible = isSkeletonVisible;

            const btn = document.getElementById('btn-skeleton');
            if(isSkeletonVisible) {
                btn.innerText = "Skeleton (On)";
                btn.style.background = "#4caf50";
            } else {
                btn.innerText = "Skeleton (Off)";
                btn.style.background = "#444";
            }
        }

        window.setCamera = function(view) {
            controls.autoRotate = false; 
            updateRotateBtn();
            switch(view) {
                case 'front': camera.position.set(0, 1.0, 3.5); break;
                case 'side': camera.position.set(3.5, 1.0, 0); break;
                case 'iso': camera.position.set(2.5, 2.5, 2.5); break;
            }
            controls.target.set(0, 1, 0);
            controls.update();
        }

        window.toggleAutoRotate = function() {
            controls.autoRotate = !controls.autoRotate;
            updateRotateBtn();
        }

        window.changeRotateSpeed = function(val) {
            controls.autoRotateSpeed = parseFloat(val);
            document.getElementById('rotate-val').innerText = val;
        }

        function updateRotateBtn() {
            const btn = document.getElementById('btn-rotate');
            if(controls.autoRotate) {
                btn.innerText = "On";
                btn.style.background = "#4caf50";
            } else {
                btn.innerText = "Off";
                btn.style.background = "#444";
            }
        }

        let isWireframeMode = false;

        function applyRenderMode() {
            if (!characterModel) return;
            characterModel.traverse(child => {
                if (child.isMesh && child.material) {
                    const mat = child.material;
                    if (isWireframeMode) {
                        if (child.userData.origWireframe === undefined) {
                            child.userData.origWireframe = mat.wireframe;
                        }
                        mat.wireframe = true;
                    } else {
                        if (child.userData.origWireframe !== undefined) {
                            mat.wireframe = child.userData.origWireframe;
                            delete child.userData.origWireframe;
                        }
                    }
                    mat.needsUpdate = true;
                }
            });
        }

        window.toggleWireframeMode = function() {
            isWireframeMode = !isWireframeMode;
            const btn = document.getElementById('btn-wireframe');
            
            if(isWireframeMode) {
                btn.innerText = "Normal Mode";
                btn.style.background = "#4caf50"; 
            } else {
                btn.innerText = "Wireframe";
                btn.style.background = "#444";
            }
            applyRenderMode();
        }

        function loadCharacter(url, fileName, isCustom = false) {
            const ext = fileName.split('.').pop().toLowerCase();
            
            if(isCustom) {
                document.getElementById('btn-female').classList.remove('active');
                document.getElementById('btn-male').classList.remove('active');
            }

            let savedTime = 0;
            if (currentAction) savedTime = currentAction.time;

            document.getElementById('anim-name').innerText = "Loading Model...";

            const onLoad = (model) => {
                if (skeletonHelper) {
                    scene.remove(skeletonHelper);
                    skeletonHelper = null;
                }

                if(characterModel) scene.remove(characterModel);
                characterModel = model;
                
                characterModel.traverse(n => {
                    if(n.isMesh) { n.castShadow = true; n.receiveShadow = true; }
                });
                scene.add(characterModel);

                skeletonHelper = new THREE.SkeletonHelper(characterModel);
                skeletonHelper.visible = isSkeletonVisible; 
                scene.add(skeletonHelper);

                applyRenderMode();

                mixer = new THREE.AnimationMixer(characterModel);
                
                let clipToPlay = null;
                if (isUserAnimation && cachedAnimClip) {
                    clipToPlay = cachedAnimClip;
                } else if (model.animations && model.animations.length > 0) {
                    clipToPlay = model.animations[0];
                    cachedAnimClip = clipToPlay;
                    isUserAnimation = false;
                }

                if (clipToPlay) {
                    currentAction = mixer.clipAction(clipToPlay);
                    if (isUserAnimation) {
                        if (isPlaying) currentAction.play();
                        else {
                            currentAction.play();
                            currentAction.paused = true;
                        }
                        currentAction.time = savedTime;
                    } else {
                        currentAction.play();
                        currentAction.paused = true;
                        isPlaying = false;
                        currentAction.time = 0;
                    }
                } else {
                    currentAction = null;
                }
                
                updatePlayBtn();
                document.getElementById('anim-name').innerText = isCustom ? "Custom Model Loaded" : fileName.replace('.fbx','');
            };

            if(ext === 'glb' || ext === 'gltf') {
                gltfLoader.load(url, (g) => onLoad(g.scene));
            } else if (ext === 'fbx') {
                fbxLoader.load(url, (o) => {
                    const box = new THREE.Box3().setFromObject(o);
                    const size = box.getSize(new THREE.Vector3()).length();
                    if(size > 100) o.scale.set(0.01, 0.01, 0.01);
                    onLoad(o);
                });
            }
        }

        window.selectDefault = function(type) {
            document.getElementById('btn-female').classList.remove('active');
            document.getElementById('btn-male').classList.remove('active');
            document.getElementById('btn-' + type).classList.add('active');

            const url = DEFAULTS[type];
            const name = type === 'female' ? "Female (X Bot)" : "Male (Y Bot)";
            loadCharacter(url, name + ".fbx");
        }

        selectDefault('female');

        const charInput = document.getElementById('char-input');
        charInput.addEventListener('change', function(e) {
            const file = e.target.files[0];
            if(!file) return;
            const url = URL.createObjectURL(file);
            loadCharacter(url, file.name, true);
        });

        const animInput = document.getElementById('anim-input');
        animInput.addEventListener('change', function(e) {
            if (!characterModel) {
                alert("먼저 캐릭터를 선택하세요.");
                return;
            }

            const file = e.target.files[0];
            if(!file) return;
            const url = URL.createObjectURL(file);
            const ext = file.name.toLowerCase();

            const onAnimLoad = (animations) => {
                if (animations && animations.length > 0) {
                    if (currentAction) currentAction.stop();
                    mixer.stopAllAction();

                    cachedAnimClip = animations[0];
                    isUserAnimation = true;

                    currentAction = mixer.clipAction(cachedAnimClip);
                    currentAction.play();
                    isPlaying = true;
                    currentAction.paused = false;
                    
                    document.getElementById('anim-name').innerText = file.name;
                    updatePlayBtn();
                } else {
                    alert("애니메이션 데이터가 없습니다.");
                }
            };

            if(ext.endsWith('glb') || ext.endsWith('gltf')) {
                gltfLoader.load(url, (g) => onAnimLoad(g.animations));
            } else if (ext.endsWith('fbx')) {
                fbxLoader.load(url, (o) => onAnimLoad(o.animations));
            }
        });

        const playBtn = document.getElementById('btn-play');
        playBtn.addEventListener('click', () => {
            if(currentAction) {
                isPlaying = !isPlaying;
                currentAction.paused = !isPlaying;
                updatePlayBtn();
            }
        });

        function updatePlayBtn() {
            playBtn.innerText = isPlaying ? "Pause" : "Play";
            playBtn.style.background = isPlaying ? "#4caf50" : "#444";
        }

        const speedInput = document.getElementById('time-scale');
        const speedVal = document.getElementById('speed-val');
        speedInput.addEventListener('input', (e) => {
            const speed = parseFloat(e.target.value);
            speedVal.innerText = speed.toFixed(1);
            if(mixer) mixer.timeScale = speed;
        });

        const progressBar = document.getElementById('progress-bar');
        let isDraggingSlider = false;

        progressBar.addEventListener('mousedown', () => { 
            isDraggingSlider = true; 
            if(currentAction) currentAction.paused = true; 
        });
        progressBar.addEventListener('mouseup', () => { 
            isDraggingSlider = false; 
            if(currentAction && isPlaying) currentAction.paused = false; 
        });
        progressBar.addEventListener('input', (e) => {
            if (currentAction) {
                const duration = currentAction.getClip().duration;
                currentAction.time = duration * (e.target.value / 100);
                mixer.update(0); 
            }
        });

        function animate() {
            requestAnimationFrame(animate);
            const delta = clock.getDelta();

            if (mixer) {
                if (!isDraggingSlider) mixer.update(delta);

                if (currentAction) {
                    const time = currentAction.time;
                    const duration = currentAction.getClip().duration;
                    
                    if (!isDraggingSlider && duration > 0) {
                        const percent = (time / duration) * 100;
                        progressBar.value = percent % 100;
                    }
                    const currentFrame = Math.floor(time * 30); 
                    document.getElementById('frame-display').innerText = currentFrame;
                }
            }
            controls.update();
            renderer.render(scene, camera);
        }
        animate();

        window.saveKeyPose = function() {
            if (!currentAction) return;
            
            const time = currentAction.time;
            const frame = Math.floor(time * 30);
            poseCounter++;

            const initialText = "";
            const poseId = Date.now();
            
            savedKeyPoses.push({ id: poseId, time: time, text: initialText, frame: frame });

            const list = document.getElementById('keypose-list');
            const div = document.createElement('div');
            div.className = 'saved-pose';
            
            div.innerHTML = `
                <div class="pose-info">
                    <span>Frame ${frame}:</span> 
                    <span class="pose-text" id="text-${poseId}"></span>
                </div>
                <button class="del-btn" onclick="event.stopPropagation(); removeKeyPose(this, ${poseId});">×</button>
            `;

            div.onclick = function() {
                currentAction.time = time;
                mixer.update(0); 
                isPlaying = false;
                currentAction.paused = true;
                updatePlayBtn();
                
                const duration = currentAction.getClip().duration;
                progressBar.value = (time / duration) * 100;
            };

            const textSpan = div.querySelector('.pose-text');
            textSpan.addEventListener('dblclick', function(e) {
                e.stopPropagation();
                const currentVal = this.innerText;
                
                const input = document.createElement('input');
                input.type = 'text';
                input.className = 'pose-text-input';
                input.value = currentVal;

                const saveEdit = () => {
                    const newVal = input.value;
                    const poseObj = savedKeyPoses.find(p => p.id === poseId);
                    if(poseObj) poseObj.text = newVal;
                    
                    textSpan.innerHTML = newVal;
                };

                input.addEventListener('blur', saveEdit);
                input.addEventListener('keydown', (ev) => {
                    if(ev.key === 'Enter') input.blur();
                    ev.stopPropagation();
                });
                
                this.innerHTML = '';
                this.appendChild(input);
                input.focus();
            });

            list.appendChild(div);
        }

        window.removeKeyPose = function(btn, id) {
            btn.parentElement.remove();
            savedKeyPoses = savedKeyPoses.filter(p => p.id !== id);
        }
        
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
    </textarea>

    <script>
        function launchApp(textareaId) {
            const sourceCode = document.getElementById(textareaId).value.trim();
            const blob = new Blob([sourceCode], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            
            const frame = document.getElementById('app-frame');
            frame.src = url;
            frame.style.display = 'block';

            document.getElementById('launcher-menu').style.opacity = '0';
            setTimeout(() => {
                document.getElementById('launcher-menu').style.display = 'none';
                document.getElementById('back-btn').style.display = 'block';
            }, 500);
        }

        function goBack() {
            const frame = document.getElementById('app-frame');
            frame.src = 'about:blank';
            frame.style.display = 'none';

            const menu = document.getElementById('launcher-menu');
            menu.style.display = 'flex';
            
            requestAnimationFrame(() => {
                menu.style.opacity = '1';
            });
            
            document.getElementById('back-btn').style.display = 'none';
        }
    </script>

</body>
</html>
