# Access Control System

A multi-component access control system combining **facial recognition**, **QR code authentication**, and **time-limited tokens** to verify employee identity at physical entry points.

## System Architecture

The system consists of three independent components that work together:

```
┌─────────────────┐        ┌──────────────────┐        ┌─────────────────┐
│   Admin Panel   │        │  Employee Portal  │        │   Entry Gate    │
│                 │        │                   │        │                 │
│ • Create users  │──────► │ • Employee login  │──────► │ • QR scanner    │
│ • Set login &   │        │ • Generate QR     │        │ • Face camera   │
│   password      │        │   (valid 5 min)   │        │ • Access grant  │
│ • Upload face   │        │                   │        │   or denial     │
└─────────────────┘        └──────────────────┘        └─────────────────┘
```

## Features

### Admin Panel (Server)
- Create and manage employee accounts
- Assign login credentials (username & password)
- Upload and store employee face photos for recognition

### Employee Portal
- Secure employee login
- Generate a time-limited QR code (**valid for 5 minutes**)
- QR code is tied to the employee's identity and expires automatically

### Entry Gate
- Scans QR code via camera
- Simultaneously verifies the employee's face using the stored photo
- Grants or denies access based on both checks passing
- Prevents QR code sharing — face must match the QR owner

## Security Model

Access is only granted when **both conditions** are met simultaneously:

1. A valid, non-expired QR code is presented
2. The face in front of the camera matches the employee assigned to that QR code

This two-factor approach prevents:
- Stolen or shared QR codes being used by unauthorized persons
- Replay attacks (QR codes expire after 5 minutes)


## Tech Stack

| Component | Technology |
|---|---|
| Backend / Server | Node.js |
| Employee Portal | Node.js + HTML/CSS |
| Face Recognition | *(e.g. `face-api.js` / OpenCV)* |


## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18+
- npm v9+
- A camera device (for the gate component)

### Installation

# 1. Clone the repository
git clone https://github.com/m-c-j/System-kontroli-dostepu.git
cd System-kontroli-dostepu

# 2. Install dependencies
npm install

### Running the components

# Start the admin/employee server
node server.js

# Start the gate scanner (on the gate device)
localhost:3000/gate

## Authors

Group project — equal contribution from all team members.

| Author | GitHub |
|---|---|
| m-c-j | [@m-c-j](https://github.com/m-c-j) |
| Igor Walasek | [@igorw33](https://github.com/igorw33) |
| Stanisław Ptaszyński | [@sptachu](https://github.com/sptachu) |

## License

This project was created for educational purposes.
