# Robot_Arm_Control_Panel

This project is a web-based control panel for a 6-servo robotic arm, created using XAMPP. It allows users to control servo positions through sliders and save custom poses into a local MySQL database.

##  Table of Contents
- [Features](#-features)  
- [How to Run](#-how-to-run)  
- [ESP32 Access](#-esp32-access)  
- [File Structure](#-file-structure)  
- [Screenshots](#-screenshots)  
- [Notes](#-notes)

##  Features
- 6 sliders to control servo1 to servo6  
- Save and manage custom poses in a MySQL database  
- Clean web interface using HTML, CSS, JS, and PHP  
- Built on a local server using XAMPP  
- Can be accessed from other devices (like a **phone**, **tablet**, or even an **ESP32**) using the local IP of the XAMPP server

##  How to Run 

### 1. Install XAMPP
- Download from: [https://www.apachefriends.org](https://www.apachefriends.org)
- Install it and open the **XAMPP Control Panel**

### 2. Start Apache & MySQL
- In the control panel, start:
  - **Apache**
  - **MySQL**

### 3. Create the Database
- Go to: `http://localhost/phpmyadmin`
- Create a new database named: `robot_arm`
- Create the following two tables manually:

#### Table: `pose`

| Column   | Type    | Attributes                  |
|----------|---------|-----------------------------|
| id       | INT     | PRIMARY KEY, AUTO_INCREMENT |
| servo1   | INT     |                             |
| servo2   | INT     |                             |
| servo3   | INT     |                             |
| servo4   | INT     |                             |
| servo5   | INT     |                             |
| servo6   | INT     |                             |

#### Table: `run`

| Column   | Type    | Attributes       |
|----------|---------|------------------|
| servo1   | INT     |                  |
| servo2   | INT     |                  |
| servo3   | INT     |                  |
| servo4   | INT     |                  |
| servo5   | INT     |                  |
| servo6   | INT     |                  |
| status   | TINYINT | Default: 0       |

---

### 4. Add Project Files

Copy the following files into your `htdocs` directory:

```bash
C:
└── xampp
    └── htdocs
        └── robot-arm-control
            ├── db_connection.php
            ├── get_poses.php
            ├── get_run_pose.php
            ├── index.php
            ├── load_pose.php
            ├── remove_pose.php
            ├── run_now.php
            ├── save_pose.php
            ├── update_status.php
            └── style

```

### 5. Run the Web App

- Open your browser and navigate to:  
  `http://localhost/robot-arm-control/` – to control the robotic arm 
  `http://localhost/robot_control/get_run_pose.php` – to fetch the currently active pose

  ![demo1](demo1.gif)

---


##  Access from Other Devices (ESP32 / Phone / Tablet)

1. **Get Local IP**  
   - Open Command Prompt and run: `ipconfig`  
   - Copy the `IPv4 Address` (e.g., `192.168.1.100`)

2. **Access from Another Device**  
   - Make sure the device (phone, tablet, etc.) is on the same Wi-Fi network  
   - Open a browser and go to:  
     `http://<local-ip>/robot-arm-control/`

   <br>

   ####  Example Access

   ** From the same PC (GIF):**  
   ![pc-demo](demo1.gif)

   ** From an iPad (Image):**  
   ![ipad-demo](ipad_view.jpg)

3. **ESP32 Access (Optional)**  
   - ESP32 can send HTTP requests to the same IP  
   - Example:
     ```cpp
     http.begin("http://192.168.1.100/robot-arm-control/save_pose.php");
     http.GET(); // or use POST
     http.end();
     ```
