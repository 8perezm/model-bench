# Three.js Procedural Low-Poly Horse Benchmark

## Objective

Create a high-quality, fully modelled and animated low-poly horse using Three.js use CDN. The result should resemble a professionally constructed low-poly game asset, not a simple collection of geometric primitives.

Build the horse procedurally in code. Do not use external 3D models, GLTF/GLB files, downloaded assets, image planes or pre-made character models.

Prioritise modelling quality, convincing anatomy, deliberate geometry and polished animation. Do not sacrifice the quality of the horse to produce a more elaborate interface.

## Reference images

Three reference images are supplied in `project/`:

- **horse-1.jpg — Overall appearance / anatomy:** Primary guide for proportions, silhouette, muscle volumes and presentation. Tan/brown body, black mane/tail, dark lower legs. Do not copy its smooth shading — final must be flat-shaded low-poly.
- **horse-3.jpg — Polygon style / density target:** Primary guide for polygon density, geometry distribution, facet size and flat-shaded appearance. This is the 2500-3500 triangle reference. Study facet distribution: higher density on head, shoulders, hips and joints, larger facets on barrel and neck.
- **horse-2.jpg — Colour/facet style only:** Reference for flat facets and palette only. Do NOT copy its density — it is far below the 2500-3500 budget and too coarse for the required anatomy.

Treat these images as visual requirements rather than loose inspiration. Where they conflict, precedence is horse-1.jpg for form/proportions, horse-3.jpg for density/distribution.

## 1. Modelling and geometry

Create a complete horse with convincing equine anatomy and recognisable proportions. It should look like a carefully constructed 3D asset rather than a collection of basic geometric shapes.

Use sufficient geometry to communicate anatomical form while retaining a clearly visible low-poly aesthetic. The horse body including mane, tail, ears and hooves (excluding ground/scene/UI) should be made up of between 2500 and 3500 polygons/triangles total, counted as triangles via `renderer.info.render.triangles` with ground/scene hidden. Distribute polygons where they contribute to the silhouette, anatomy and visible form. Avoid both extremely coarse geometry and unnecessarily dense, smooth geometry.

Build from sculpted cross-section loops with distinct volumes for chest, barrel, belly and hindquarters — not boxes, capsules, cylinders or spheres. Maintain horse proportions (use shoulder-to-hip = 1 unit: back roughly level, chest deep, hindquarters rounded, neck curved ~40-50° from horizontal, head length ~1/4 body length, legs long with clearly offset knee/hock heights fore vs hind). Spend density on head/jaw/muzzle, shoulder/hip transitions and leg joints; keep barrel and mid-neck facets larger as in horse-3.jpg. Silhouette must read as horse from front, side, rear and three-quarter views in both neutral pose and mid-gallop.

Include:

- **Head:** Defined forehead, cheeks, jaw, muzzle and nostrils.
- **Eyes:** Visible, correctly positioned eyes with suitable geometry and materials.
- **Ears:** Two distinct, pointed ears.
- **Neck:** Curved, muscular neck with a clear transition into the shoulders and chest.
- **Torso:** Defined chest, barrel, back, abdomen and hindquarters.
- **Legs:** Four separately modelled, articulated legs with plausible equine proportions and visible joints.
- **Hooves:** Distinct, properly shaped hooves with clear geometry.
- **Mane:** Volumetric, polygonal mane with layered strands or clumps rather than a flat strip.
- **Tail:** Volumetric polygonal tail with a recognisable shape.

Pay particular attention to the horse's silhouette. Its proportions and shape should remain convincing from the front, side, rear and three-quarter views.

Avoid cylindrical legs with no anatomical shaping, spherical joints, obvious primitive placeholders, a featureless capsule-shaped torso, a block-like head or neck, flat details that only work from one camera angle, and geometry so coarse that important anatomical forms disappear.

## 2. Low-poly visual style

Use an intentional low-poly aesthetic:

- Flat-shaded triangular and polygonal surfaces.
- Clearly visible facets and deliberate changes in surface direction.
- Enough polygons to represent the anatomy and silhouette convincingly.
- Natural horse colours, with restrained variation between selected faces.
- A coherent material palette and consistent visual style.

The model should look deliberately low-poly, not unfinished or under-modelled. Do not use smooth shading to hide inadequate geometry.

## 3. Locomotion and animation

Implement a complete horse locomotion system with the following animation states.

Research https://en.wikipedia.org/wiki/The_Horse_in_Motion text and images to learn how a horse moves naturally, and use it to inform gait timing, leg sequencing, foot placement, and body movement.

### Idle
- Natural standing pose.
- Subtle breathing and body movement.
- Small head and neck movements.
- Occasional ear movement.
- Subtle tail movement.

### Walk
- Convincing four-beat walking gait.
- Natural foot placement and weight transfer.
- Appropriate movement through the shoulders, hips, torso, neck and head.

### Trot
- Recognisable diagonal leg pairing.
- Increased body movement.
- Appropriate suspension and foot placement.

### Canter
- Recognisable three-beat gait.
- Coordinated leg movement.
- Visible suspension and natural body movement.

### Gallop
- Fast, dynamic running motion.
- Convincing galloping leg sequence.
- Extended and gathered leg positions.
- Pronounced suspension phase.
- Coordinated movement through the spine, torso, shoulders, hips, neck and head.
- It can try to use `motion-capture/index.html` (`/workspace/horse-deepseek-v4.1-advanced/project/motion-capture/index.html`) to help with movement of the legs: it contains a side-view transverse gallop mocap reference with skeleton joint positions, stance/swing phases, footfall order/timings (LH/RH/LF/RF), and two-bone IK for knees/hocks. Use it as a guide for gallop leg phasing, lift/fold, and hoof placement.

### Rig and articulation

- Hierarchy: `root > spine > [chest > neckBase > neckMid > head > (jaw, 2 ears)] + [4x shoulder/hip > knee/hock > fetlock > hoof]`, plus separate mane/tail chains.
- Place pivots at anatomical joints, not mesh centres. Primary rotation on one hinge axis per joint plus small twist only.
- Animate in place (no root travel); stance feet must plant without visible sliding.
- Spine/neck/head must counter-move per gait to preserve balance, not stay rigid.

### Animation quality

- Animate all four legs independently.
- Use appropriate articulation at the shoulders, hips, knees, hocks, fetlocks and hooves.
- Maintain anatomically plausible limb positions throughout each gait.
- Include believable weight distribution and centre-of-mass movement.
- Animate the spine, torso, neck and head to complement each gait.
- Add secondary movement to the mane, tail and ears.
- Avoid mechanical, robotic or synchronised movement that does not resemble a horse.

### Transitions and playback

- Provide smooth transitions between all animation states.
- Allow the horse to progress from walking through trotting and cantering into a gallop, and decelerate back to walking or idle.
- Blend transitions naturally, without sudden limb-position changes or animation discontinuities.
- Make animation speed adjustable.
- Use delta time for frame-rate-independent animation.
- Ensure each gait loops seamlessly.

## 4. Interactive camera controls

Implement interactive camera controls so the horse can be inspected from any angle:

- **Orbit:** Rotate the camera around the horse using mouse drag.
- **Pan:** Move the camera target horizontally and vertically.
- **Zoom:** Zoom in and out using the mouse wheel.
- **Touch support:** Provide equivalent gestures on touch devices where practical.
- Set sensible minimum and maximum zoom distances.
- Prevent the camera from moving below the ground plane.
- Keep the horse as the camera's focal point.
- Provide a reset-camera button.
- Keep the horse correctly framed when the viewport is resized.

Use `THREE.OrbitControls` where appropriate.

## 5. Animation control panel

Provide a compact interface for testing the model:

- Animation selector: Idle, Walk, Trot, Canter and Gallop.
- Play/pause control.
- Animation speed slider.
- Smooth transitions when switching animation states.
- Reset animation button.
- Reset camera button.

The controls must be functional, clearly labelled and visually unobtrusive. The horse should remain the main focus.

## 6. Scene and presentation

Present the horse in a professional 3D showcase environment:

- Three-quarter default camera angle.
- Orthographic or perspective camera with appropriate framing.
- Ground plane with convincing contact shadows.
- Professional lighting with soft shadows.
- Neutral background that makes the horse stand out.
- Ensure the entire horse is visible in the initial view.

The scene should make the geometry easy to inspect without distracting from the model.

## 7. Technical requirements

- Use Three.js.
- Generate all horse geometry programmatically.
- Do not use external model assets or substitute missing details with primitive placeholders.
- Use `BufferGeometry` where appropriate.
- Use hierarchical groups for articulated body parts.
- Organise modelling, materials, scene setup and animation into reusable functions or modules.
- Use flat-shaded materials.
- Use delta time for animation updates.
- Handle window resizing correctly.
- Ensure camera controls and animation controls work together.
- Avoid unnecessary dependencies.
- Ensure the application runs without errors.

## 8. Quality expectations and priorities

The final result should resemble a professionally modelled low-poly game asset, with deliberate geometry, convincing anatomy, a detailed silhouette and polished animation.

The horse must maintain convincing anatomical proportions and geometry throughout every animation state. Pay particular attention to the legs, shoulders, hips and neck during the gallop. The model must remain visually convincing when inspected closely from any camera angle.

Prioritise work in this order:

1. High-quality modelling and anatomical accuracy.
2. Convincing locomotion across all five animation states.
3. Geometry and shading that achieve the supplied low-poly references.
4. Interactive camera and animation controls.
5. Scene presentation and code organisation.

Meeting the 2500-3500 triangle budget is required, but count alone does not pass — the result is judged by the actual 3D asset and its animation, not merely by an attractive initial screenshot or UI completion.

Acceptance: provide wireframe toggle and live triangle-count readout (ground/scene excluded) to prove budget; verify silhouette in front/side/rear/three-quarter views and in neutral pose plus mid-gallop extension/gather.

## 9. Phase 2 — Scenery (after Phase 1 complete)

Only start once §§1-8 are complete and accepted. Do not regress horse modelling, rig, gaits, or the 2500-3500 triangle horse budget to build scenery.

Replace/extend the neutral showcase in §6 with a next-level quality low-poly trail environment. Scenery objects must be in the same flat-shaded style as the horse but richer — no skimping, MORE polygons where it reads. Fully formed silhouettes from all camera angles.

**Style:** faceted geometry with flat shading throughout — visible triangles, each a single solid colour, no texture maps, no smooth normals. Light changes shade facet to facet for crystal look. Simple chunky shapes that read at a glance. Warm soft storybook mood, not realism.

**Composition (layered depth):** foreground dirt track in tan/ochre large angular patches in slightly different tones, with grass-blade tufts, pebbles and stemmed flowers; midground wooden post-and-rail fence parallel to default view with grassy meadow behind dotted with trees, rocks and tufts; background rolling hills in lighter olive greens, then grey-brown mountains with pale snow/rock caps fading into hazy lavender-grey sky. Default camera low, roughly eye level, moderate FOV, horizon fairly high so trees loom.

**Palette:** greens carry the scene from dark pine to bright yellow-green meadow/canopies; warm earth tan/caramel dirt and reddish-brown wood; cool muted greys/mauves for mountains, clouds and sky. Moderate saturation, warm late-afternoon values overall.

**Lighting and atmosphere:** one directional sun from upper left/front with soft-edged ground shadows; hemisphere/ambient fill so shadow sides stay readable; atmospheric perspective with distant hills/mountains lighter, bluer/greyer, fog-tinted toward sky colour. Clouds as flattened lumpy faceted masses in white/grey.

**Variation and touches:** random variation in tree height, rotation, scale and tint; low-poly dust puffs at hooves; ground as large angular patches with subtle colour variation, never a flat plane.

Include, all procedural `BufferGeometry`, flat-shaded, no external assets:

- **Trail:** sculpted dirt path with width variation, banked/overlapping grass edges, per-face tan variation, scattered pebbles and small ruts.
- **Wooden fence:** one side of trail only, capped posts with slight lean/rotation jitter plus 2-3 rails with joints/breaks, per-piece brown variation.
- **Grass:** ground cover plus dense multi-blade tufts with colour gradient and wind sway.
- **Trees — not just cones:** pines with tapered trunks + root flare and 4-6 irregular layered tiers with per-face jitter; broadleaf with branching limbs + 3-5 clustered faceted canopies in varied greens. No single-cone or single-blob trees.
- **Mountains:** multi-ridge distant range with separate snow-cap meshes, rock-face variation and foothills.
- **Rocks:** irregular deformed polyhedra in small clusters, grey variation with moss tint on some faces.
- **Flowers:** stems + leaves + headed blooms (petals + centre) in 2-3 species/colours, scattered in grass.
- **Sky:** sun disc with glow + multiple clustered faceted clouds at varied heights/sizes, slow drift.
- **Birds — horse-like detailing:** full bodies with torso, head, beak, tail and articulated wings with feather clumps/fingers, not flat V shapes. Decent polygon count per bird (order ~150-300 tris). Flap via shoulder/elbow joints plus glide phases, looped circling/soaring paths.
- **Butterflies:** bodies + heads + antennae + 4 patterned wings, looped flutter + wander paths near flowers/grass.

Behaviour/technical:

- Keep horse the focal point; scenery must not occlude default three-quarter view. Keep §4 orbit/pan/zoom, reset-camera, and resize framing.
- Animate with delta time: birds, butterflies, cloud drift; optional subtle tree/grass sway. All loops seamless.
- Organise scenery as reusable functions/modules per type (e.g. `makeTree`, `makeFence`, `makeMountain`, `makeBird`, `makeButterfly`, `makeCloud`); share flat-shaded material palette with horse where possible.
- Use reuse/instancing for performance, but do not skimp to save triangles in Phase 2 — richness takes precedence. Scenery budget is separate and uncapped from the horse; report horse-only and total counts separately.
- Shadows: horse keeps convincing contact shadow; scenery receives/casts consistently without washing out the horse.
