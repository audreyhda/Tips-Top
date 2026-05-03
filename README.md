# 💡 Tips Top

> **An iOS app that helps users discover iPhone features they didn't know they had — with personalised video tips, step-by-step guides, and topic-based discussions.**

<div align="center">
<br>
<a href="https://www.balystick.fr/Github/Tips%20Top.mp4">
    <img src="https://www.balystick.fr/Github/Tips-Top%20logo.png" alt="Tips Top App" style="width:340px">
</a>
<br><br>
<em>▶ Click the logo to watch the demo video</em>
</div>

---

## 📌 Problem Statement

Most iPhone users only scratch the surface of what their device can do. Hidden features, productivity shortcuts, and accessibility options go undiscovered because there's no easy, contextual way to learn about them. Generic YouTube searches return too much noise; Apple's own documentation is exhaustive but not personalised. Tips Top fills this gap by surfacing the right tip for the right user — based on what they actually interact with.

---

## 🧩 Project Overview

Tips Top is a group project built during **Nano Challenge 2 (Thetis)** of the [Apple Foundation Program Advanced](https://www.apple.com/fr/newsroom/2020/10/apple-and-france-partner-to-expand-the-apple-foundation-program-for-developers/) in Paris (30 August – 13 September 2024, 2 weeks). The challenge required applying **SOLID principles** to an existing codebase and integrating **REST API endpoints over HTTP** — each team member implementing a different SOLID principle within the project. Figma and Git were the primary collaboration tools.

The app infers user interests by tracking interactions, then recommends iPhone feature videos accordingly. Users can also follow step-by-step implementation guides and join discussions around features.

---

## 🛠️ Tech Stack

### 🌐 Languages
- Swift 5

### 📦 Frameworks & Libraries
- SwiftUI — Declarative UI for modern screens
- UIKit — Legacy and interop components (crossover approach)
- URLSession — HTTP networking for REST API calls

### ☁️ Infrastructure & DevOps
- SOLID principles — Applied throughout the architecture (challenge requirement)
- MVVM — Model-View-ViewModel pattern
- Figma — UI/UX design and team collaboration
- Git / GitHub — Version control

### 🔧 Tools & Other
- UML — System and data flow modelling
- Stack navigation — `NavigationStack` / `UINavigationController`
- HTTP protocol — REST API integration for tips content

--- 

## ✨ Features

- **Personalised Recommendations** — The app analyses user interactions (taps, time spent, likes) to infer interests and surface relevant iPhone feature videos.
- **Video Tips Feed** — A curated, filterable feed of short iPhone feature videos fetched from a REST API.
- **Step-by-Step Guides** — Break down each feature into a clear, numbered walkthrough so users can follow along on their device.
- **Topic Search** — Search tips by theme (productivity, camera, accessibility, shortcuts…) to find features relevant to a specific need.
- **Feature Discussions** — Comment and discuss tips with other users to share context and use cases.

---

## 🏗️ Architecture & Technical Details

### System Design

The app follows an **MVVM** architecture with a **SwiftUI / UIKit crossover** — SwiftUI handles the primary declarative views while UIKit components are bridged in where needed (e.g. `UIViewControllerRepresentable`). Navigation uses a stack-based approach throughout. The codebase was refactored during the challenge to apply SOLID principles across its layers.

### Data Flow

```
User interaction
      │
      ▼
ViewModel (observes + processes interactions)
      │
      ├── Interest engine → updates preference weights
      │
      └── Service layer (URLSession async) → REST API
                │
                ▼
           Tips content (JSON) → decoded models → feed update
```

### SOLID Principles Applied

This challenge explicitly required each team member to introduce a different SOLID principle:

- **S — Single Responsibility**: Each ViewModel and Service class has one clearly defined job (e.g. `TipFeedViewModel` only handles feed state; `InterestTracker` only handles interaction scoring).
- **O — Open/Closed**: The recommendation engine is open for extension (new scoring strategies can be added) without modifying existing logic.
- **L — Liskov Substitution**: Service protocols are designed so mock implementations can replace real ones for testing without breaking callers.
- **I — Interface Segregation**: Network and persistence concerns are split into separate protocols rather than one large "data manager" interface.
- **D — Dependency Inversion**: ViewModels depend on service protocols, not concrete implementations — enabling injection and testability.

### Key Technical Decisions

- **SwiftUI + UIKit crossover**: The challenge built on a previous project that used UIKit. Rather than a full rewrite, we bridged the two — a practical approach that reflects real-world iOS codebases where both coexist.
- **Interest inference from interactions**: Instead of an onboarding questionnaire, the app observes what users tap, watch, and like to build a preference profile silently. This lowers friction and improves over time.
- **HTTP / REST for tips content**: The challenge required real REST API integration. Tips metadata (title, category, video URL, steps) is fetched over HTTP and decoded from JSON, keeping content dynamic and updatable without app releases.
- **Stack navigation**: A linear `NavigationStack` ensures predictable back-navigation across feed → detail → step-by-step, matching iOS conventions.

---

## 📁 Project Structure

```
Tips-Top/
├── App/
│   └── TipsTopApp.swift             # App entry point
├── Models/
│   ├── Tip.swift                    # Tip data model (Codable)
│   ├── Step.swift                   # Step-by-step model
│   └── UserPreferences.swift        # Interest weights model
├── ViewModels/
│   ├── TipFeedViewModel.swift       # Feed state and filtering
│   ├── TipDetailViewModel.swift     # Single tip + steps
│   └── InterestTracker.swift        # Interaction-based preference scoring
├── Views/
│   ├── SwiftUI/
│   │   ├── FeedView.swift           # Personalised tips feed
│   │   ├── TipDetailView.swift      # Video + description + steps
│   │   ├── StepView.swift           # Step-by-step walkthrough
│   │   └── DiscussionView.swift     # Comments / discussion thread
│   └── UIKit/
│       └── SearchViewController.swift  # UIKit search screen (bridged)
├── Services/
│   ├── TipServiceProtocol.swift     # Service interface (SOLID-I)
│   ├── TipService.swift             # URLSession implementation
│   └── MockTipService.swift         # Mock for testing
└── Resources/
    └── Assets.xcassets
```

---

## ⚙️ Getting Started

### Prerequisites

- Xcode 15+
- iOS 17+ simulator or device

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/audreyhda/Tips-Top.git
cd Tips-Top

# 2. Open in Xcode
open TipsTop.xcodeproj

# 3. Select a simulator or device and press Run (⌘R)
```

No external dependencies or API keys required for the base build.

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `TIPS_API_BASE_URL` | Base URL for the tips content REST API | ✅ |

---

## 🗺️ Roadmap

- [x] Personalised video feed based on user interactions
- [x] Step-by-step feature walkthroughs
- [x] Topic-based search
- [x] Feature discussions
- [x] REST API integration (HTTP)
- [x] SOLID principles refactor
- [x] SwiftUI / UIKit crossover architecture
- [ ] Push notifications for new tips matching user interests
- [ ] Bookmarks / reading list
- [ ] Offline mode with cached tips

---

## 🤝 Team

Built in group during Nano Challenge 2 (Thetis) of the **Apple Foundation Program Advanced**, Paris — August–September 2024.

- GitHub: [@audreyhda](https://github.com/audreyhda)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

*Apple Foundation Program Advanced · Nano Challenge 2: Thetis · Built with ❤️ and SwiftUI in Paris*
