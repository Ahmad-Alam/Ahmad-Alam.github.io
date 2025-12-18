---
layout: page
title: GestuNova
description: Real-time hand gesture recognition for hands-free computer control
img: assets/img/projects/gestunova.png
importance: 1
category: work
github: https://github.com/Ahmad-Alam/GestuNova
---

GestuNova is a desktop application that enables hands-free computer control through real-time hand gesture recognition. Developed as my Final Year Project at PUCIT, it uses MediaPipe's hand landmark detection to track hand movements and maps recognized gestures to system commands, keyboard shortcuts, or custom Python scripts.

The system captures video from a webcam and extracts 21 hand landmarks per frame using MediaPipe. These landmarks are preprocessed into relative coordinates and normalized before being fed into a custom machine learning classifier. The application supports 9 default gesture classes and includes functionality to train and add new gestures through a data collection interface.

Built with PySide6, the application features a modern dark-themed GUI with two main views: a live preview page showing real-time gesture recognition with FPS display, and a command binding page where users can configure gesture-to-action mappings. A cooldown mechanism prevents accidental repeated command execution, and all configurations can be exported and imported via JSON files.

The project demonstrates practical application of computer vision and machine learning for accessibility, combining OpenCV for video processing, MediaPipe for hand tracking, and custom classifiers for gesture recognition into a cohesive desktop application.
