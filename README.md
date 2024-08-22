### Building a Multi-Display Emulator Using AOSP: Step-by-Step Guide

Today, I’ll walk you through operating the Android emulator with multiple displays, an increasingly relevant task given the rise of in-car screens in modern vehicles.

#### **Understanding the Need for Multi-Display in AAOS**
With the advent of new energy vehicles, cars are now equipped with multiple screens, such as instrument clusters, central control screens, co-driver screens, rear-seat screens, and even armrest screens. As the demand for multi-screen functionality grows, AAOS is continually improving its support for these features. This tutorial focuses on building and running a multi-display emulator using AOSP, a capability that has been evolving with recent updates in AAOS14.

#### **Step 1: Setting Up Your Environment**

Before you start building the emulator, ensure your environment is set up correctly:

```bash
cd aosp
source build/envsetup.sh
lunch sdk_car_md_x86_64-ap2a-userdebug
```

This configuration (`sdk_car_md_x86_64-userdebug`) is designed specifically for multi-display support on the emulator.

#### **Step 2: Building the Emulator**
Once the environment is configured, initiate the build process:

```bash
make
```

This step compiles the source code, setting up the emulator with multi-display capabilities. The compilation might take some time, depending on your system's resources.

#### **Step 3: Running the Emulator**

After the build completes, you can start the emulator with the following command:

```bash
emulator -no-snapshot
```

This command launches the emulator without using any saved states, ensuring a fresh start each time.

For additional help and options, use:

```bash
emulator -help
```

This will provide you with more command-line options to fine-tune the emulator's behavior.

#### **Step 4: Debugging Multi-Display**

To interact with and debug multiple displays, several commands are at your disposal:

- **Check Current Activity Focus:**
  
  ```bash
  dumpsys activity activities | grep mFoc
  ```

- **Launch an App on a Specific Display:**
  
  ```bash
  am start -n com.android.car.settings/.Settings_Launcher_Homepage --display 2
  ```

- **Dump Display Information:**
  
  ```bash
  dumpsys display
  ```

- **Display ID Information:**
  
  ```bash
  dumpsys SurfaceFlinger --display-id
  ```

- **Capture Screenshots of All Displays:**
  
  ```bash
  screencap -d [display-id] -p ./screenshot.png
  ```

These commands allow you to monitor and manipulate the multi-display setup directly from the terminal.

#### **Step 5: Customizing Display Configurations**

In many cases, the default display configurations may not suit your needs. You can modify screen resolution, density, and other settings in the `Makefile` and configuration files:

- **Adjusting Screen Resolution and Density:**

  Modify the following section in `car_md.mk`:

  ```makefile
  EMULATOR_MULTIDISPLAY_HW_CONFIG := 1,1320,1080,220,0,2,1920,1080,220,0,3,1920,1080,220,0
  ```

- **Updating Configuration for Display Layouts:**

  Modify `display_settings.xml` to reflect the changes:

  ```xml
  <display name="port:1" forcedDensity="220" dontMoveToTop="true"/>
  ```

These changes help align the emulator's display configurations with real-world vehicle screen setups.

#### **Step 6: Reviewing the UI and Multi-Display Operation**

After making the necessary adjustments, you can observe how the multi-display emulator handles different in-car screens:

- **Instrument Screen**
- **Central Control Screen**
- **Co-pilot Screens**

#### **Conclusion**

By following these steps, you can build and run a multi-display emulator using AOSP, paving the way for developing and testing applications designed for the next generation of in-car experiences. This guide should serve as a solid foundation for anyone looking to explore the capabilities of AAOS in a multi-screen environment.

For more insights and future updates, stay tuned to my blog!

---

*Author: Harsh Pal*  
