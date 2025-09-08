# RevPi Connect 4 - Industrial IoT Control System

This repository contains the configuration and deployment files for controlling and monitoring a Revolution Pi (RevPi) Connect 4 industrial IoT device. The system provides a Docker-based environment for running the `piTest` utility, which allows direct control and monitoring of digital and analog I/O modules.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Docker Configuration](#docker-configuration)
- [piTest Commands Reference](#pitest-commands-reference)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## 📖 Overview

The Revolution Pi Connect 4 is an industrial-grade Raspberry Pi-based platform designed for automation and IoT applications. This project provides a ready-to-use Docker environment that includes the `piTest` utility for controlling and monitoring the device's I/O modules.

The system supports:
- Digital Input/Output modules (16 inputs, 16 outputs)
- Analog Input/Output modules (4 inputs, 2 outputs)
- PWM signal generation
- Counter/encoder functionality
- RTD temperature sensor support

## ✨ Features

- **Docker-based deployment** - Ensures consistent environment across different systems
- **Full I/O control** - Control all digital and analog inputs/outputs
- **PWM support** - Generate PWM signals on digital outputs
- **Counter functionality** - Count pulses on digital inputs
- **Temperature monitoring** - Read system temperature and RTD sensors
- **Real-time monitoring** - Continuous monitoring of I/O values
- **Balena-compatible** - Works with Balena device management platform

## 🛠 Prerequisites

- Docker and Docker Compose installed
- Revolution Pi Connect 4 device with DIO and/or AIO modules
- Basic understanding of industrial automation concepts
- Access to the piControl device driver (`/dev/piControl0`)

## 🚀 Getting Started

1. Clone this repository:
   ```bash
   git clone <repository-url>
   ```

2. Build and run the Docker container:
   ```bash
   docker-compose up -d
   ```

3. Access the container:
   ```bash
   docker exec -it revpi4_connect_revpi_pitest_1 bash
   ```

4. Start using piTest commands (see [Usage](#usage) section)

## ⚠️ Important Configuration Step

## Copy config.rsc file to balena os /mnt/boot directory

### Reboot then

This step is crucial for proper operation of the RevPi Connect 4 with Balena OS. The [config.rsc](config.rsc) file contains the PiCtory configuration that defines your hardware setup. Without this configuration, the piControl driver won't be able to communicate properly with your I/O modules.

## 🎮 Usage

Once inside the container, you can use the `piTest` command to interact with your RevPi device. Here are some common examples:

### Digital I/O Control
```bash
# Read a digital input
piTest -r I_1

# Set a digital output
piTest -w O_1,1

# Read all digital inputs at once
piTest -r 0,2,h
```

### Analog I/O Control
```bash
# Read an analog input
piTest -r InputValue_1

# Set an analog output (raw value)
piTest -w OutputValue_1,16384
```

### PWM Control
```bash
# Enable PWM on output 1
piTest -w OutputPWMActive,1

# Set PWM value (0-255)
piTest -w PWM_1,128

# Set PWM frequency
piTest -w OutputPWMFrequency,50
```

### System Information
```bash
# Get device list
piTest -d

# Check system temperature
piTest -r Core_Temperature

# Get system version
piTest -V
```

For a complete reference of all piTest commands, see [piTest_command.md](piTest_command.md).

## 🐳 Docker Configuration

The [docker-compose.yml](docker-compose.yml) file defines a service with the following key configurations:

- **Privileged access** - Required for hardware access
- **Device mapping** - Maps `/dev/piControl0` for piControl communication
- **Host networking** - Uses host network for direct device access
- **Persistent settings** - tmpfs and restart policies for reliability

The Docker container is built from [Dockerfile.template](Dockerfile.template) which:
1. Installs required build dependencies
2. Clones the piTest repository with submodules
3. Builds the piTest binary
4. Makes piTest globally accessible

## 📚 piTest Commands Reference

For a comprehensive reference of all piTest commands, please see the detailed documentation in [piTest_command.md](piTest_command.md). This includes:

- System information commands
- Digital I/O control
- Analog I/O control
- PWM signal generation
- Counter/encoder functionality
- RTD temperature sensor support
- Continuous monitoring options
- System control commands

## 📁 Project Structure

```
.
├── Dockerfile.template      # Docker image definition
├── docker-compose.yml       # Container orchestration
├── config.rsc               # PiCtory configuration file
├── piTest_command.md        # Complete piTest command reference
└── README.md               # This file
```

### Configuration Details

- **config.rsc** - Contains the PiCtory configuration defining the device layout, I/O mapping, and module settings
- **Dockerfile.template** - Template for building the Docker image with piTest utility
- **docker-compose.yml** - Defines the container service with necessary hardware access permissions

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Revolution Pi](https://revolutionpi.com/) - For creating the industrial Raspberry Pi platform
- KUNBUS GmbH - For the piTest utility and piControl driver
- The industrial automation community for their continued support and contributions