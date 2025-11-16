# MindHalo - AI-Powered Study Assistant for macOS

A comprehensive macOS application built with SwiftUI that provides AI-powered study tools including an intelligent tutor, study guide generator, and flashcard generator.

## Features

### 🎓 AI Study Tutor
- Interactive chat interface with AI assistance
- Real-time question answering
- Comprehensive explanations for any topic
- Beautiful chat bubble UI with timestamps

### 📚 Study Guide Generator
- Generate comprehensive study guides from any topic
- Save and manage multiple study guides
- Copy guides to clipboard
- Clean, organized markdown-style output

### 🎴 AI Flashcard Generator
- Convert any text into flashcards
- Interactive flip-card interface
- Navigate through flashcard sets
- Question and answer format

### 🔐 License Key Verification System
- Secure hardware-based activation
- Server-side validation via REST API
- Persistent license storage
- Hardware UUID detection using IOKit

## Technical Architecture

### Core Components

#### 1. **MindHaloApp.swift**
- Main application entry point
- Initializes AppState
- Checks for stored license on launch
- Configures window appearance

#### 2. **AppState.swift**
- Central state management using `@ObservableObject`
- Tracks license validation status
- Manages Foundation Models availability
- Controls tab navigation

#### 3. **LicenseManager.swift**
- Hardware UUID retrieval using IOKit
- Async/await license validation
- POST request to activation API
- UserDefaults persistence

#### 4. **AIService.swift**
- Foundation Models API wrapper
- Availability detection (macOS 15.0+)
- Three main AI operations:
  - `askTutor(question:)` - Interactive tutoring
  - `generateStudyGuide(topic:)` - Study guide creation
  - `generateFlashcards(text:)` - Flashcard generation

#### 5. **UI Components**
- **LicenseView**: License key input and validation
- **SidebarView**: Navigation sidebar with status indicator
- **StudyTutorView**: Chat interface for AI tutor
- **StudyGuideView**: Study guide generator with split view
- **FlashcardView**: Flashcard generator and study interface
- **SettingsView**: App information and system status

## App Flow

### 1. Launch Sequence
```
App Launch → Check Stored License → LicenseView or MainAppView
```

### 2. License Validation
```
User Enters Key → Get Hardware UUID → POST to API → Validate Response → Store Result
```

### 3. Foundation Models Check
```
License Valid → Check macOS Version → Check API Availability → Update UI State
```

### 4. AI Feature Access
- **If Available**: Full AI features enabled
- **If Unavailable**: Show message: "This Mac does not support Apple Foundation Models. MindHalo AI features are unavailable on this device."

## API Endpoints

### License Activation
**Endpoint**: `https://vercel-activation.vercel.app/api/activate`

**Method**: POST

**Request Body**:
```json
{
  "license": "LICENSE-KEY-HERE",
  "machineId": "HARDWARE-UUID-HERE"
}
```

**Response**:
```json
{
  "valid": true/false,
  "message": "Optional error message"
}
```

## Foundation Models Detection

The app checks for Foundation Models availability using:
1. macOS version check (`@available(macOS 15.0, *)`)
2. Translation framework's `LanguageAvailability` API
3. Runtime capability detection

If unavailable, all AI features are disabled and appropriate messages are displayed.

## Design System

### Liquid Glass UI
- Uses `.ultraThinMaterial` for glassmorphic effects
- Linear gradients (blue to purple) for accents
- Smooth animations and transitions
- macOS-native window styling

### Color Palette
- **Primary**: Blue → Purple gradient
- **Background**: Dark gradient (#1a1a33 → #262640)
- **Success**: Green
- **Error**: Red
- **Warning**: Orange

## Requirements

- **macOS**: 15.0 or later (for AI features)
- **Hardware**: Apple Silicon recommended
- **Xcode**: Latest version
- **Swift**: 5.0+

## Project Structure

```
MindHalo/
├── MindHalo/
│   ├── MindHaloApp.swift          # App entry point
│   ├── ContentView.swift          # Root view controller
│   ├── AppState.swift             # State management
│   ├── LicenseManager.swift       # License validation
│   ├── AIService.swift            # AI API wrapper
│   ├── LicenseView.swift          # License input screen
│   ├── SidebarView.swift          # Navigation sidebar
│   ├── StudyTutorView.swift       # AI tutor interface
│   ├── StudyGuideView.swift       # Study guide generator
│   ├── FlashcardView.swift        # Flashcard interface
│   ├── SettingsView.swift         # Settings screen
│   └── Assets.xcassets/           # App assets
└── MindHalo.xcodeproj/            # Xcode project
```

## Installation

1. Open `MindHalo.xcodeproj` in Xcode
2. Select your development team in project settings
3. Build and run the project
4. Enter a valid license key on first launch

## License Key System

The app validates licenses using:
- **Machine ID**: Hardware UUID from IOKit
- **Server Validation**: REST API call to Vercel endpoint
- **Persistent Storage**: UserDefaults for validated licenses
- **Secure**: Hardware-bound activation

## Future Enhancements

- Actual Foundation Models API integration
- Study session analytics
- Cloud sync for study materials
- Export options (PDF, Markdown)
- Dark/Light theme toggle
- Custom AI model selection

## Credits

**Created**: November 15, 2025  
**Framework**: SwiftUI + Combine  
**Platform**: macOS  

---

© 2025 MindHalo. All rights reserved.
