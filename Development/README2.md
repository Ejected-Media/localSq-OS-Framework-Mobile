The GitHub repository for Cocos 4 marks a major architectural shift for the engine following its acquisition. It is now being positioned as a "purely open-source," high-performance, cross-platform engine that decouples the engine core from the editor.

Key Highlights of Cocos 4:
 * Separation of Engine and Editor: In previous versions (1.x–3.x), "Cocos Creator" referred to the combined engine and editor. Starting with Cocos 4, "COCOS" refers specifically to the engine. The editor's core components and cross-platform framework are being converted into CLI tools integrated into the engine's core.
 * Purely Open Source: The transition moves to a fully open model under the MIT License, making core code and previously private CLI tools permanently free for the global community.
 * Technical Architecture:
   * Hybrid Language Model: The runtime is built using a mix of C++ (for low-level infrastructure, rendering, and scene management) and TypeScript (for user-level APIs).
   * Modern Graphics: Supports Vulkan (Windows/Android), Metal (macOS/iOS), and WebGL/WebGPU.
   * Render Pipeline: Features a fully customizable render pipeline and a "Surface Shader" system based on GLSL 300 for high-end PBR (Physically Based Rendering).
 * AI Integration: The repository notes that this evolution is designed to "fully integrate AI," supporting the upcoming AI-driven IDE named PinK.

Relevance to Your Projects:

Given your focus on projects like localSq and Shop Oahu, the move to a purely open-source, CLI-centric engine offers several advantages:
 * Automation: The new CLI focus makes it easier to integrate Cocos into modern CI/CD pipelines and automated web workflows.
 * Lightweight Performance: The engine remains highly optimized for mobile and web (instant-play), which is critical for local service apps and interactive shop interfaces.
 * Future-Proofing: With the backing of SUD and a shift toward AI-assisted coding, the engine is likely to see rapid updates in developer productivity tools.

The repository is currently active with a recent v4.0.0-alpha.1 release, signaling the start of this new era.
