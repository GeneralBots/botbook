# Humanoid Robotics with General Bots

Build custom humanoid robots powered by General Bots, using computer vision from botmodels, LLM intelligence from botserver, and BASIC keywords for movement control.

## Why Run General Bots on a Humanoid?

A humanoid robot without an LLM orchestrator is just an expensive puppet. The hardware handles joints and sensors, but something needs to decide *what* to do with them. That's where General Bots comes in.

**The robot becomes a server.** The same botserver that handles WhatsApp messages and web chat now handles servo commands and camera feeds. Your humanoid runs:

- **botserver** on port 8088 — conversation, decisions, tool execution
- **llama.cpp** on port 8080 — local LLM inference (optional, for offline)
- **botmodels** — computer vision pipeline for face/object detection
- **Stalwart** — yes, your robot can have its own email server
- **PostgreSQL** — conversation history, user recognition data

This isn't theoretical. The same stack that powers enterprise chatbots runs on a Jetson Orin Nano inside a robot chassis. When someone walks up and says "where's the bathroom?", the request flows through the same LLM pipeline, triggers the same BASIC keywords, and the response happens to include servo movements instead of just text.

**Practical benefits:**

| Traditional Robot | GB-Powered Robot |
|-------------------|------------------|
| Hardcoded responses | LLM-generated natural conversation |
| Fixed behavior scripts | Event-driven, adaptive responses |
| Separate control systems | Unified orchestration |
| Cloud-dependent | Fully offline capable |
| Custom integration work | Standard GB packages (.gbai) |

The robot is just another deployment target. Same .gbai packages, same BASIC scripts, same tools — but with `ROBOT WALK` and `SERVO MOVE` alongside `SEND MAIL` and `POST`.

## Overview

General Bots transforms humanoid robot kits into intelligent conversational assistants capable of:

- **Natural conversation** via LLM integration
- **Visual recognition** using botmodels CV pipelines
- **Expressive movement** through BASIC keyword commands
- **Autonomous behavior** with event-driven triggers

<img src="../assets/chapter-13/humanoid-architecture.svg" alt="Humanoid Robot Architecture" style="max-width: 100%; height: auto;">

## Supported Robot Kits

### Consumer Kits

| Kit | DOF | Height | Price | Best For |
|-----|-----|--------|-------|----------|
| **Unitree G1** | 23 | 127cm | $16,000 | Research, commercial |
| **Unitree H1** | 19 | 180cm | $90,000 | Industrial, research |
| **UBTECH Walker S** | 41 | 145cm | Contact | Enterprise service |
| **Fourier GR-1** | 40 | 165cm | $100,000+ | Research |
| **Agility Digit** | 16 | 175cm | Lease | Warehouse, logistics |

### DIY/Maker Kits

| Kit | DOF | Height | Price | Best For |
|-----|-----|--------|-------|----------|
| **Poppy Humanoid** | 25 | 83cm | $8,000 | Education, research |
| **InMoov** | 22+ | 170cm | $1,500+ | Makers, open source |
| **Reachy** | 14 | Torso | $15,000 | HRI research |
| **NimbRo-OP2X** | 20 | 95cm | $30,000 | RoboCup, research |
| **ROBOTIS OP3** | 20 | 51cm | $11,000 | Education, competition |

### Affordable Entry Points

| Kit | DOF | Height | Price | Best For |
|-----|-----|--------|-------|----------|
| **ROBOTIS MINI** | 16 | 27cm | $500 | Learning, hobby |
| **Lynxmotion SES-V2** | 17 | 40cm | $800 | Education |
| **Hiwonder TonyPi** | 16 | 35cm | $400 | Raspberry Pi projects |
| **XGO-Mini** | 12 | 20cm | $350 | Quadruped + arm |

## Architecture

### System Components

The robot runs the full General Bots stack:

| Component | Role | Technology |
|-----------|------|------------|
| **botserver** | Brain - LLM, conversation, decisions | Rust, Port 8088 |
| **botmodels** | Eyes - CV, face recognition, object detection | Python, ONNX |
| **BASIC Runtime** | Motor control - movement sequences | Keywords → servo commands |
| **Hardware Bridge** | Translation layer | GPIO, Serial, CAN bus |
| **llama.cpp** | Local LLM (optional) | C++, Port 8080 |
| **PostgreSQL** | User data, conversation history | SQLite for embedded |
| **SeaweedFS** | File storage (documents, images) | Optional |
| **Stalwart** | Email server — robot has its own inbox | Optional |

Yes, your robot can receive emails. A visitor sends an email to `robot@company.com`, and the humanoid can respond, schedule meetings, or notify staff. Same stack, different form factor.

### Communication Flow

| Step | From | To | Protocol |
|------|------|----|----------|
| 1 | Microphone | botserver | Audio stream / STT |
| 2 | botserver | LLM | HTTP API |
| 3 | LLM response | BASIC interpreter | Internal |
| 4 | BASIC keywords | Hardware bridge | Serial/GPIO |
| 5 | Hardware bridge | Servos | PWM/CAN |
| 6 | Camera | botmodels | Video stream |
| 7 | botmodels | botserver | Detection events |

## Hardware Setup

### Computing Options

| Option | Specs | Use Case |
|--------|-------|----------|
| **Jetson Orin Nano** | 8GB, 40 TOPS | Full CV + local LLM |
| **Raspberry Pi 5** | 8GB, no NPU | Cloud LLM, basic CV |
| **Orange Pi 5** | 8GB, 6 TOPS NPU | Local LLM, basic CV |
| **Intel NUC** | 32GB, x86 | Maximum performance |

### Servo Controllers

| Controller | Channels | Interface | Best For |
|------------|----------|-----------|----------|
| **PCA9685** | 16 PWM | I2C | Small robots |
| **Pololu Maestro** | 6-24 | USB/Serial | Hobby servos |
| **Dynamixel U2D2** | 254 | USB/TTL/RS485 | Dynamixel servos |
| **ODrive** | 2 BLDC | USB/CAN | High-torque joints |

### Sensor Integration

| Sensor | Purpose | Interface |
|--------|---------|-----------|
| USB Camera | Vision, face detection | USB/CSI |
| IMU (MPU6050) | Balance, orientation | I2C |
| ToF (VL53L0X) | Distance sensing | I2C |
| Microphone Array | Voice input, direction | USB/I2S |
| Force Sensors | Grip feedback | ADC |

## Event-Driven Robotics with ON Events

General Bots uses an **event-driven architecture** - no loops needed. The robot reacts to events automatically.

### Vision Events

```basic
' React when a person is detected
ON CV "person" DETECTED CALL person_detected

' React when a specific person is recognized
ON CV "face" RECOGNIZED CALL greet_person

' React when an object is seen
ON CV "cat" DETECTED CALL react_to_cat

' React when someone waves
ON CV "gesture:wave" DETECTED CALL wave_back

' React when someone approaches
ON CV "person" DISTANCE < 1.5 CALL person_approaching
```

### Voice Events

```basic
' React to wake word
ON HEAR "Hey robot" CALL wake_up

' React to any speech
ON HEAR CALL process_speech

' React to specific commands
ON HEAR "follow me" CALL start_following
ON HEAR "stop" CALL emergency_stop
ON HEAR "sit down" CALL sit_pose
```

### Sensor Events

```basic
' React to balance issues
ON IMU TILT > 15 CALL stabilize

' React to touch
ON TOUCH "head" CALL head_touched
ON TOUCH "hand_left" CALL hand_touched

' React to obstacles
ON DISTANCE "front" < 0.5 CALL obstacle_detected

' React to battery level
ON BATTERY < 20 CALL low_battery_warning
```

### Time Events

```basic
' Scheduled behaviors
ON SCHEDULE "0 9 * * *" CALL morning_greeting
ON SCHEDULE "*/5 * * * *" CALL idle_animation

' Periodic checks
ON INTERVAL 30000 CALL check_surroundings
```

## Movement Tools

Define robot capabilities as **TOOLS** that the LLM can call naturally during conversation.

### Basic Movement Tools

```basic
' wave-hello.bas
PARAM person_name DESCRIPTION "Name of person to wave at"

TALK "Hello " + person_name + "!"
ROBOT ARM "right", action: "wave"
WAIT 1500
ROBOT POSE "stand"
```

```basic
' point-direction.bas
PARAM direction DESCRIPTION "Direction to point: left, right, forward, behind"

SELECT CASE direction
    CASE "left"
        ROBOT ARM "left", action: "point"
        TALK "It's over there to the left"
    CASE "right"
        ROBOT ARM "right", action: "point"
        TALK "It's over there to the right"
    CASE "forward"
        ROBOT ARM "right", action: "extend"
        TALK "It's straight ahead"
    CASE "behind"
        ROBOT TURN 180
        ROBOT ARM "right", action: "point"
        TALK "It's behind us"
END SELECT
```

```basic
' bow-greeting.bas
PARAM style DESCRIPTION "Bow style: formal, casual, deep"

SELECT CASE style
    CASE "formal"
        ROBOT HEAD "look", pan: 0, tilt: -30
        WAIT 1000
    CASE "casual"
        ROBOT HEAD "nod"
    CASE "deep"
        ROBOT POSE "bow"
        WAIT 1500
        ROBOT POSE "stand"
END SELECT
```

### Navigation Tools

```basic
' walk-to-location.bas
PARAM location DESCRIPTION "Where to walk: reception, elevator, exit, charging_station"

locations = {
    "reception": [0, 0],
    "elevator": [5, 2],
    "exit": [10, 0],
    "charging_station": [-2, 1]
}

target = locations[location]
ROBOT NAVIGATE target[0], target[1]
TALK "I'll take you to the " + location
```

```basic
' follow-person.bas
PARAM duration_seconds DESCRIPTION "How long to follow in seconds"

ROBOT MODE "follow"
TALK "I'll follow you for " + duration_seconds + " seconds"
WAIT duration_seconds * 1000
ROBOT MODE "stationary"
TALK "Okay, I'll stay here now"
```

### Expressive Tools

```basic
' show-emotion.bas
PARAM emotion DESCRIPTION "Emotion to display: happy, sad, surprised, thinking, confused"

SELECT CASE emotion
    CASE "happy"
        ROBOT DISPLAY "face_happy"
        ROBOT HEAD "nod"
    CASE "sad"
        ROBOT DISPLAY "face_sad"
        ROBOT HEAD "look", pan: 0, tilt: -20
    CASE "surprised"
        ROBOT DISPLAY "face_surprised"
        ROBOT HEAD "look", pan: 0, tilt: 10
    CASE "thinking"
        ROBOT DISPLAY "face_thinking"
        ROBOT HEAD "look", pan: 20, tilt: 10
    CASE "confused"
        ROBOT DISPLAY "face_confused"
        ROBOT HEAD "tilt", angle: 15
END SELECT
```

```basic
' dance-move.bas
PARAM style DESCRIPTION "Dance style: wave, robot, celebration"

SELECT CASE style
    CASE "wave"
        SEQUENCE PLAY "dance_wave"
    CASE "robot"
        SEQUENCE PLAY "dance_robot"
    CASE "celebration"
        SEQUENCE PLAY "dance_celebration"
        TALK "Woohoo!"
END SELECT
```

## Event Handlers

### Person Detection Handler

```basic
' on-person-detected.bas
' Called automatically when ON CV "person" DETECTED fires

person = EVENT.data

' Turn to face the person
ROBOT HEAD "look", pan: person.direction.x, tilt: person.direction.y

' Check if we know them
IF person.identity <> "unknown" THEN
    USE TOOL "wave-hello", person_name: person.identity
ELSE
    TALK "Hello! Welcome. How can I help you?"
    USE TOOL "bow-greeting", style: "casual"
END IF
```

### Cat Detection Handler

```basic
' on-cat-detected.bas  
' Called automatically when ON CV "cat" DETECTED fires

cat = EVENT.data

TALK "Oh, I see a cat!"
ROBOT HEAD "look", pan: cat.direction.x, tilt: cat.direction.y
USE TOOL "show-emotion", emotion: "happy"

' Crouch down to cat level
ROBOT POSE "crouch"
TALK "Here kitty kitty!"
WAIT 3000
ROBOT POSE "stand"
```

### Gesture Handler

```basic
' on-wave-detected.bas
' Called automatically when ON CV "gesture:wave" DETECTED fires

gesture = EVENT.data

' Wave back
ROBOT HEAD "look", pan: gesture.direction.x, tilt: gesture.direction.y
USE TOOL "wave-hello", person_name: "there"
```

### Speech Handler

```basic
' on-speech.bas
' Called automatically when ON HEAR fires

speech = EVENT.data.text

' Let LLM decide what to do with available tools
response = LLM speech

' LLM automatically calls tools like:
' - wave-hello when greeting someone
' - point-direction when giving directions
' - show-emotion to express feelings
' - walk-to-location when guiding someone

TALK response
```

### Balance Handler

```basic
' on-balance-issue.bas
' Called automatically when ON IMU TILT > 15 fires

ROBOT BALANCE ON
TALK "Whoa, let me steady myself"

stable = ROBOT STABLE
IF NOT stable THEN
    ROBOT POSE "wide_stance"
    WAIT 1000
END IF

ROBOT BALANCE OFF
```

### Low Battery Handler

```basic
' on-low-battery.bas
' Called automatically when ON BATTERY < 20 fires

TALK "My battery is getting low. I need to charge soon."
USE TOOL "show-emotion", emotion: "sad"

IF BATTERY < 10 THEN
    TALK "I really need to go charge now. Excuse me."
    USE TOOL "walk-to-location", location: "charging_station"
END IF
```

## Configuration

### Robot Definition File

Create `robot.csv` in your `.gbot` folder:

| name | value |
|------|-------|
| robot_type | humanoid |
| controller | PCA9685 |
| controller_address | 0x40 |
| servo_count | 16 |
| balance_enabled | true |
| cv_enabled | true |
| cv_model | yolov8n |
| face_model | arcface |

### Servo Mapping

Create `servos.csv` to map joints to channels:

| joint | channel | min_angle | max_angle | home | inverted |
|-------|---------|-----------|-----------|------|----------|
| head_pan | 0 | -90 | 90 | 0 | false |
| head_tilt | 1 | -45 | 45 | 0 | false |
| left_shoulder | 2 | -90 | 180 | 0 | false |
| left_elbow | 3 | 0 | 135 | 90 | false |
| left_wrist | 4 | -90 | 90 | 0 | false |
| right_shoulder | 5 | -90 | 180 | 0 | true |
| right_elbow | 6 | 0 | 135 | 90 | true |
| right_wrist | 7 | -90 | 90 | 0 | true |
| left_hip | 8 | -45 | 45 | 0 | false |
| left_knee | 9 | 0 | 90 | 0 | false |
| left_ankle | 10 | -30 | 30 | 0 | false |
| right_hip | 11 | -45 | 45 | 0 | true |
| right_knee | 12 | 0 | 90 | 0 | true |
| right_ankle | 13 | -30 | 30 | 0 | true |
| left_grip | 14 | 0 | 90 | 0 | false |
| right_grip | 15 | 0 | 90 | 0 | false |

### Event Registration

Create `events.csv` to register event handlers:

| event | handler | enabled |
|-------|---------|---------|
| CV:person:detected | on-person-detected.bas | true |
| CV:cat:detected | on-cat-detected.bas | true |
| CV:gesture:wave:detected | on-wave-detected.bas | true |
| HEAR | on-speech.bas | true |
| IMU:tilt:15 | on-balance-issue.bas | true |
| BATTERY:20 | on-low-battery.bas | true |

### Motion Sequences

Create `motions.csv` for predefined sequences:

| name | frames |
|------|--------|
| wave | [{"t":0,"joints":{"right_shoulder":90}},{"t":500,"joints":{"right_shoulder":120}},{"t":1000,"joints":{"right_shoulder":90}}] |
| bow | [{"t":0,"joints":{"head_tilt":0}},{"t":500,"joints":{"head_tilt":-30}},{"t":1500,"joints":{"head_tilt":0}}] |
| nod | [{"t":0,"joints":{"head_tilt":0}},{"t":200,"joints":{"head_tilt":-15}},{"t":400,"joints":{"head_tilt":10}},{"t":600,"joints":{"head_tilt":0}}] |

## Complete Example: Reception Robot

### Package Structure

| Path | Description |
|------|-------------|
| `reception.gbai/` | Root package |
| `reception.gbdialog/` | BASIC scripts |
| `reception.gbdialog/start.bas` | Initialization and event registration |
| `reception.gbdialog/tools/` | Tool definitions |
| `reception.gbdialog/handlers/` | Event handlers |
| `reception.gbot/` | Configuration |
| `reception.gbot/robot.csv` | Robot settings |
| `reception.gbot/servos.csv` | Servo mapping |
| `reception.gbot/events.csv` | Event registration |
| `reception.gbkb/` | Knowledge base |

### start.bas - Initialization

```basic
' reception.gbdialog/start.bas
' Initialize the reception robot

' Configure robot hardware
SERVO INIT "PCA9685", address: 0x40
ROBOT POSE "stand"
ROBOT BALANCE ON

' Set personality for LLM
SET SYSTEM PROMPT "You are a friendly reception robot at TechCorp. " + _
    "Greet visitors warmly, answer questions about the company, " + _
    "and direct them to the right department. " + _
    "Use your movement tools to be expressive and helpful."

' Load company knowledge
USE KB "company-info"

' Register all tools for LLM
USE TOOL "wave-hello"
USE TOOL "point-direction"
USE TOOL "bow-greeting"
USE TOOL "walk-to-location"
USE TOOL "show-emotion"
USE TOOL "follow-person"

' Register event handlers
ON CV "person" DETECTED CALL handlers/on-person-detected.bas
ON CV "face" RECOGNIZED CALL handlers/on-face-recognized.bas
ON CV "gesture:wave" DETECTED CALL handlers/on-wave-detected.bas
ON HEAR CALL handlers/on-speech.bas
ON IMU TILT > 15 CALL handlers/on-balance-issue.bas
ON BATTERY < 20 CALL handlers/on-low-battery.bas

' Start with a ready pose
TALK "Reception robot online and ready to help!"
USE TOOL "show-emotion", emotion: "happy"
```

### handlers/on-person-detected.bas

```basic
' Called when a person enters the field of view

person = EVENT.data

' Face the person
ROBOT HEAD "look", pan: person.direction.x, tilt: person.direction.y

' Greet appropriately
IF person.identity <> "unknown" THEN
    ' Known person
    TALK "Welcome back, " + person.identity + "! Great to see you again."
    USE TOOL "wave-hello", person_name: person.identity
ELSE
    ' New visitor
    TALK "Hello! Welcome to TechCorp. How may I assist you today?"
    USE TOOL "bow-greeting", style: "casual"
END IF
```

### handlers/on-face-recognized.bas

```basic
' Called when a known face is recognized

face = EVENT.data

' Get person info from database
person_info = GET "employees", "name = '" + face.identity + "'"

IF person_info THEN
    ' Employee
    TALK "Good morning, " + face.identity + "! " + _
         "You have " + person_info.meetings_today + " meetings today."
ELSE
    ' Known visitor
    TALK "Hello " + face.identity + "! Let me notify your contact that you've arrived."
    SEND NOTIFICATION face.expected_contact, face.identity + " has arrived at reception"
END IF
```

### handlers/on-speech.bas

```basic
' Called when speech is detected

speech = EVENT.data.text

' Use LLM with tools to generate response and actions
' LLM will automatically call appropriate tools based on context:
' - "Where is the bathroom?" → point-direction tool
' - "Take me to the elevator" → walk-to-location + follow-person tools  
' - "Thank you!" → show-emotion + wave-hello tools

response = LLM speech
TALK response
```

### tools/guide-visitor.bas

```basic
' guide-visitor.bas
PARAM destination DESCRIPTION "Where to guide the visitor: meeting_room_a, meeting_room_b, cafeteria, restroom, elevator"
PARAM visitor_name DESCRIPTION "Name of the visitor being guided"

TALK "Of course, " + visitor_name + "! Please follow me to " + destination + "."
USE TOOL "show-emotion", emotion: "happy"

' Start walking and ask them to follow
ROBOT MODE "guide"
USE TOOL "walk-to-location", location: destination

' Arrived
ROBOT TURN 180
TALK "Here we are! This is the " + destination + ". Is there anything else you need?"
USE TOOL "bow-greeting", style: "casual"
```

## Build Guides

### Beginner: Desktop Companion (~$600)

| Component | Model | Price |
|-----------|-------|-------|
| Robot Kit | ROBOTIS MINI | $500 |
| Compute | Raspberry Pi 5 4GB | $60 |
| Camera | Pi Camera v3 | $25 |
| Microphone | USB mic | $15 |

**Capabilities:** Voice conversation via cloud LLM, basic face detection, gesture responses, desktop assistant.

### Intermediate: Service Robot (~$10,000)

| Component | Model | Price |
|-----------|-------|-------|
| Robot Kit | Poppy Humanoid | $8,000 |
| Compute | Jetson Orin Nano | $500 |
| Camera | Intel RealSense D435 | $300 |
| Microphone | ReSpeaker Array | $100 |
| Speakers | USB powered | $50 |

**Capabilities:** Local LLM (Llama 3.2 3B), full body tracking, object manipulation, walking and navigation.

### Advanced: Research Platform (~$20,000+)

| Component | Model | Price |
|-----------|-------|-------|
| Robot Kit | Unitree G1 EDU | $16,000 |
| Compute | Onboard + Workstation | $3,000 |
| Sensors | LiDAR + Depth cameras | $1,000 |

**Capabilities:** Full autonomous navigation, complex manipulation, multi-modal interaction, research-grade motion control.

## Deployment Notes

### The Robot as a Server

When you deploy GB to a humanoid, you're deploying a server that happens to have legs. The robot:

- Has its own IP address on the network
- Runs the full botserver API (REST, WebSocket)
- Can be managed remotely via the Suite UI
- Stores conversation history locally
- Syncs with cloud when connected (optional)

Multiple robots can share a central botserver, or each can run independently. For a fleet of reception robots, you might run one botserver with multiple robot clients. For a standalone assistant, everything runs on the robot itself.

### Offline Operation

With llama.cpp and local models, the robot operates without internet:

| Model | RAM Required | Performance |
|-------|--------------|-------------|
| TinyLlama 1.1B | 2GB | ~5 tok/s on Pi 5 |
| Phi-2 2.7B | 4GB | ~3 tok/s on Jetson |
| Llama 3.2 3B | 6GB | ~4 tok/s on Orin Nano |

Vision models run locally via ONNX. The robot sees, thinks, and acts without phoning home.

## Safety

### Physical Safety

- Always have emergency stop accessible
- Set conservative torque limits initially
- Test movements at reduced speed first
- Ensure stable base before walking
- Keep clear area around robot

### Software Safety with Events

```basic
' on-emergency.bas
' Called by hardware emergency button or voice command

ROBOT STOP
ROBOT POSE "safe"
ROBOT BALANCE OFF
LOG ERROR "Emergency stop activated"
TALK "Emergency stop. All movement halted."
```

Register in events.csv:

| event | handler | enabled |
|-------|---------|---------|
| EMERGENCY | on-emergency.bas | true |
| HEAR:stop:emergency | on-emergency.bas | true |

### Operating Guidelines

| Situation | Event | Action |
|-----------|-------|--------|
| Unknown obstacle | ON DISTANCE < 0.5 | Stop, assess, navigate around |
| Balance issue | ON IMU TILT > 15 | Widen stance or sit down |
| Person too close | ON CV "person" DISTANCE < 0.8 | Step back, warn verbally |
| Battery low | ON BATTERY < 20 | Announce, navigate to charger |
| Communication lost | ON CONNECTION LOST | Safe pose, wait for reconnect |

## Resources

### Robot Kits

- [Unitree Robotics](https://www.unitree.com/) - G1, H1 humanoids
- [ROBOTIS](https://www.robotis.com/) - OP3, MINI, Dynamixel
- [Poppy Project](https://www.poppy-project.org/) - Open source humanoid
- [InMoov](https://inmoov.fr/) - 3D printable humanoid
- [Pollen Robotics](https://www.pollen-robotics.com/) - Reachy

### Components

- [Dynamixel](https://www.robotis.us/dynamixel/) - Smart servos
- [ODrive](https://odriverobotics.com/) - BLDC motor control
- [Intel RealSense](https://www.intelrealsense.com/) - Depth cameras
- [NVIDIA Jetson](https://developer.nvidia.com/embedded/jetson-modules) - Edge AI

### Learning

- [ROS 2 Humanoid](https://docs.ros.org/) - Robot Operating System
- [MoveIt](https://moveit.ros.org/) - Motion planning
- [OpenCV](https://opencv.org/) - Computer vision
- [MediaPipe](https://mediapipe.dev/) - Body/hand tracking