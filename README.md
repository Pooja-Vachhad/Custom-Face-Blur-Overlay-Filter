# Custom Face Blur & Overlay Filter

A real-time face filtering tool that blurs faces or applies custom image overlays. The project includes two separate implementations, each using a different approach to face detection and masking.

## Implementations

### 1. Known/Unknown Face Filter (face_recognition)

Uses the `face_recognition` library to detect and classify faces as known or unknown, then applies an effect selectively.

- Load one or more reference images of a known person
- Compare every face detected in the webcam feed against the known encodings
- Apply blur or overlay only to known faces, or only to unknown faces, depending on configuration
- Works on a live webcam feed
- Uses a rectangular bounding box around each face for the blur/overlay region

This approach answers: "is this face someone specific, and should it be filtered?"

### 2. Landmark-Based Precise Masking (MediaPipe)

Uses MediaPipe FaceMesh to extract facial landmarks and build a precise mask of the face shape, rather than a rectangle.

- Detects facial landmarks for each face
- Builds a convex hull around the landmarks to get the actual face contour
- Applies blur or overlay only within that contour, with alpha blending for transparent overlay images
- Works on both static images and video files
- Applies the effect to every detected face (no known/unknown distinction in this version)

This approach answers: "how do I filter exactly the face region, not just a rough box around it?"

## Features

- Real-time multi-face detection
- Two masking strategies: bounding box vs. landmark-based convex hull
- Blur and image overlay modes, both with alpha blending support for overlays
- Known/unknown face filtering logic (face_recognition implementation)

## How Known/Unknown Filtering Works

- At least one known face image must be provided as a reference
- Filter modes:
  - Known-only: effect applied only to faces matching the known reference(s)
  - Unknown-only: effect applied to every face except the known reference(s)
- Without a known face reference, the known/unknown distinction cannot be made, and filtering will not behave as expected

## Tech Stack

- Python
- OpenCV
- face_recognition
- MediaPipe

## Usage

Each implementation is in its own script. Run the relevant script directly, providing a known face image path (for the face_recognition version) and an overlay image path if using overlay mode.
