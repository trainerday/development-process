---
title: Create Ride Web Trainer
type: note
permalink: product-development/os-projects/td-web/backlogs/create-ride-web-trainer
---

# Create Ride Web Trainer

## Overview
Build a new web-based indoor trainer application at **ride.trainerday.com** that serves as both a viewer for extending the mobile app and a standalone training platform. The feature will be called **"Web Trainer"**.

## Target Positioning
- **URL**: ride.trainerday.com 
- **Feature Name**: "Web Trainer"
- **Primary Use Cases**: 
  - Extend mobile app functionality to web
  - Standalone web-based training for indoor cycling
  - Bridge for devices that don't have native FTMS support

## Core Features to Build

### Phase 1: Device Connectivity & Basic Training
- **Web Bluetooth Integration**
  - FTMS (Fitness Machine Service) support for smart trainers
  - Standard BLE services (Heart Rate, Cycling Power, Speed/Cadence)
  - Custom protocol support for popular devices (Echelon, Domyos, etc.)
  - Device discovery and pairing interface

### Phase 2: Training Interface
- **Live Training Dashboard**
  - Real-time metrics display (power, cadence, heart rate, speed)
  - Workout player with interval guidance
  - Resistance control for compatible trainers
  - Virtual shifting support where applicable

### Phase 3: TrainerDay Integration
- **Account Integration**
  - Seamless login from existing TrainerDay accounts
  - Sync workouts and training plans
  - Save training sessions to user's activity history
  - Access to workout library and plans

### Phase 4: Advanced Features
- **Enhanced Training Experience**
  - Live workout following with auto-resistance
  - Custom workout creation interface
  - Real-time performance feedback
  - Integration with Zwift/other platforms as bridge

## Technical Architecture

### Web Bluetooth Compatibility
Based on research of qDomyos-Zwift project:
- **60-70% device compatibility expected** - Many "custom" protocols actually use standard GATT services with custom data formats
- **Priority devices**: FTMS trainers, Echelon bikes, Domyos equipment, Wahoo/Tacx trainers
- **Implementation approach**: Start with FTMS + standard services, expand to reverse-engineered protocols

### Platform Requirements
- Progressive Web App (PWA) for mobile compatibility
- Web Bluetooth API (Chrome/Edge required)
- Real-time data processing and visualization
- Offline capability for standalone training

## Marketing & User Experience

### Messaging
- **"Turn any smart trainer into a connected experience"**
- **"No app required - train directly in your browser"**
- **"Bridge your trainer to any training platform"**

### User Journey
1. **Discovery**: From TrainerDay mobile app "Open Web Trainer" button
2. **Setup**: Device pairing via Web Bluetooth
3. **Training**: Choose workout or free ride mode
4. **Integration**: Auto-sync back to TrainerDay account

## Success Metrics
- Device connection success rate >85%
- User session duration >30 minutes average
- Mobile app to web conversion rate >15%
- Standalone user acquisition and retention

## Competitive Advantages
- **No app installation required**
- **Works with broader device range than most platforms**
- **Seamless TrainerDay ecosystem integration**
- **Free tier with premium features**

## Development Phases
1. **MVP**: Basic Web Bluetooth + FTMS support
2. **Device Expansion**: Add custom protocol support for popular brands  
3. **Full Integration**: Complete TrainerDay ecosystem integration
4. **Advanced Features**: Virtual shifting, platform bridging, enhanced UI

---

*This backlog represents a significant strategic expansion into web-based training, positioning TrainerDay as a comprehensive training ecosystem across mobile and web platforms.*