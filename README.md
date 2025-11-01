# GXHTC3: Arduino-Compatible Library for Temperature and Humidity Sensing 🌡️💧

[![Download Releases](https://img.shields.io/badge/Download%20Releases-Click%20Here-blue)](https://github.com/MOONSHOP03/GXHTC3/releases)

Welcome to the **GXHTC3** repository! This library allows you to easily interface with the GXHTC3 temperature and humidity sensor using I2C. Whether you are building a weather station, a smart home device, or any other project that requires accurate environmental data, this library simplifies the process of sensor communication and data management.

## Table of Contents

1. [Features](#features)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Examples](#examples)
5. [Contributing](#contributing)
6. [License](#license)
7. [Support](#support)

## Features

- **I2C Communication**: Communicate with the GXHTC3 sensor using the I2C protocol.
- **Easy-to-Use Interface**: Simple functions for reading temperature and humidity data.
- **Power Management**: Efficient power management to extend battery life in portable applications.
- **Arduino Compatibility**: Works seamlessly with Arduino boards.

## Installation

To install the GXHTC3 library, follow these steps:

1. **Download the Library**: Visit the [Releases section](https://github.com/MOONSHOP03/GXHTC3/releases) to download the latest version of the library.
2. **Add to Arduino IDE**:
   - Open the Arduino IDE.
   - Go to `Sketch` > `Include Library` > `Add .ZIP Library...`.
   - Select the downloaded ZIP file.

3. **Verify Installation**: After installation, you can check if the library is included by navigating to `Sketch` > `Include Library`. You should see `GXHTC3` in the list.

## Usage

To use the GXHTC3 library in your Arduino project, include it at the top of your sketch:

```cpp
#include <GXHTC3.h>
```

### Initializing the Sensor

Create an instance of the GXHTC3 class and initialize it in the `setup()` function:

```cpp
GXHTC3 sensor;

void setup() {
    Serial.begin(9600);
    if (!sensor.begin()) {
        Serial.println("Sensor not found!");
        while (1);
    }
    Serial.println("Sensor initialized successfully.");
}
```

### Reading Data

You can read temperature and humidity data using the following functions:

```cpp
void loop() {
    float temperature = sensor.readTemperature();
    float humidity = sensor.readHumidity();
    
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.println(" °C");
    
    Serial.print("Humidity: ");
    Serial.print(humidity);
    Serial.println(" %");
    
    delay(2000); // Wait for 2 seconds before the next reading
}
```

## Examples

To help you get started, we have included example sketches in the `examples` folder. Here are a couple of highlights:

### Basic Example

This example shows how to read and display temperature and humidity data:

```cpp
#include <GXHTC3.h>

GXHTC3 sensor;

void setup() {
    Serial.begin(9600);
    if (!sensor.begin()) {
        Serial.println("Sensor not found!");
        while (1);
    }
}

void loop() {
    float temperature = sensor.readTemperature();
    float humidity = sensor.readHumidity();
    
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.println(" °C");
    
    Serial.print("Humidity: ");
    Serial.print(humidity);
    Serial.println(" %");
    
    delay(2000);
}
```

### Advanced Example

In this example, we will log the data to an SD card. Ensure you have an SD card module connected to your Arduino.

```cpp
#include <GXHTC3.h>
#include <SD.h>

GXHTC3 sensor;
File dataFile;

void setup() {
    Serial.begin(9600);
    if (!sensor.begin()) {
        Serial.println("Sensor not found!");
        while (1);
    }
    
    if (!SD.begin()) {
        Serial.println("SD card initialization failed!");
        return;
    }
    Serial.println("SD card initialized.");
}

void loop() {
    float temperature = sensor.readTemperature();
    float humidity = sensor.readHumidity();
    
    dataFile = SD.open("data.txt", FILE_WRITE);
    if (dataFile) {
        dataFile.print("Temperature: ");
        dataFile.print(temperature);
        dataFile.print(" °C, Humidity: ");
        dataFile.print(humidity);
        dataFile.println(" %");
        dataFile.close();
    } else {
        Serial.println("Error opening file");
    }
    
    delay(2000);
}
```

## Contributing

We welcome contributions to improve the GXHTC3 library. If you have suggestions, bug reports, or feature requests, please open an issue or submit a pull request.

### How to Contribute

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and commit them.
4. Push your branch to your fork.
5. Open a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Support

For support, please check the [Releases section](https://github.com/MOONSHOP03/GXHTC3/releases) for updates and documentation. You can also open an issue in the repository if you encounter any problems.

---

Thank you for using the GXHTC3 library! We hope it helps you in your projects. For more information, feel free to explore the code and examples provided in this repository. Happy coding!