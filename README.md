<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Simple 3D Cube</title>
    <style>
        body { margin: 0; overflow: hidden; } /* Removes default body margins */
        canvas { display: block; } /* Makes the canvas element a block element */
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        // --- 2. Setup the Scene, Camera, and Renderer ---
        const scene = new THREE.Scene();

        // Perspective Camera (Field of View, Aspect Ratio, Near, Far)
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);

        // Renderer (Where the 3D graphics are drawn)
        const renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // --- 3. Create the 3D Object (Cube) ---
        // Define the geometry (the shape)
        const geometry = new THREE.BoxGeometry(1, 1, 1);

        // Define the material (the look/color)
        const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 }); // Green color

        // Combine geometry and material into a Mesh (the final object)
        const cube = new THREE.Mesh(geometry, material);

        // Add the cube to the scene
        scene.add(cube);

        // Move the camera back so we can see the cube
        camera.position.z = 5;

        // --- 4. Animation Loop (Game Loop) ---
        function animate() {
            // Request the next frame from the browser
            requestAnimationFrame(animate);

            // Rotation Logic (This is where the cube moves/animates)
            cube.rotation.x += 0.01;
            cube.rotation.y += 0.01;

            // Render the scene
            renderer.render(scene, camera);
        }

        // Start the animation loop
        animate();

        // --- 5. Handle Window Resize (Keeps the scene full-screen) ---
        window.addEventListener('resize', () => {
            const width = window.innerWidth;
            const height = window.innerHeight;
            renderer.setSize(width, height);
            camera.aspect = width / height;
            camera.updateProjectionMatrix();
        });
    </script>
</body>
</html>
