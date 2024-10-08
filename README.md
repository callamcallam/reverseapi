
# MITMProxy Setup on Windows 11 for API Reverse Engineering

## Overview

This guide explains how to set up **mitmweb** (from the **mitmproxy** package) on Windows 11, configure your iPhone/Android device to route traffic through the proxy, and use **Postman** to analyze the API requests from a mobile app.

## Prerequisites

1. **Windows 11** system.
2. **Python 3.6+** installed. [Download Python here](https://www.python.org/downloads/)
3. **mitmproxy** installed.
4. An **iPhone** or **Android** device.
5. **Postman** installed. [Download Postman here](https://www.postman.com/downloads/)

---

## Step 1: Install mitmproxy

First, ensure you have Python installed and that `pip` is available. If you don't have Python installed, download it from [here](https://www.python.org/downloads/).

1. **Open Command Prompt or PowerShell**.
   
2. Install **mitmproxy** by running the following command:

   ```bash
   pip install mitmproxy
   ```

3. After the installation completes, verify it by running:

   ```bash
   mitmproxy --version
   ```

   You should see version information, indicating mitmproxy has been installed correctly.

---

## Step 2: Launch mitmweb

**mitmweb** provides a web-based interface for inspecting traffic.

1. Launch **mitmweb**:

   ```bash
   mitmweb
   ```

2. After starting, you'll see a message indicating that the web interface is accessible at:

   ```
   Web server listening at http://127.0.0.1:8081/
   ```

3. You can now open a browser and navigate to `http://127.0.0.1:8081/` to see the web interface.

---

## Step 3: Find Your IP Address on Windows

To allow your iPhone/Android device to route traffic through your Windows 11 machine, you need to find your computer's IP address.

1. Open **Command Prompt** or **PowerShell**.
   
2. Run the following command to find your IP address:

   ```bash
   ipconfig
   ```

3. Look for your **IPv4 Address** under the active network connection. It will look something like `192.168.1.x`.

---

## Step 4: Configure iPhone/Android Device

1. Go to **Wi-Fi Settings** on your mobile device.
2. Find your Wi-Fi network and tap the **i** (information) icon next to it.
3. Scroll down and select **Configure Proxy**.
4. Choose **Manual**.
5. Enter your **Windows 11 machine's IP address** (found in Step 3) in the **Server** field.
6. Set the **Port** to `8080`.
7. Save the settings.

---

## Step 5: Install the mitmproxy CA Certificate on the Mobile Device

Since mitmproxy intercepts and decrypts HTTPS traffic, you need to install its CA (Certificate Authority) certificate on your mobile device.

1. Open a browser on your mobile device and go to:

   ```
   http://mitm.it
   ```

2. Download and install the appropriate certificate for your operating system:
   - For iPhone (iOS): Download the **iOS** certificate.
   - For Android: Download the **Android** certificate.

3. **iOS Certificate Installation:**
   - Go to **Settings** > **General** > **Profile** > **Install Profile**.
   - Follow the prompts to install the mitmproxy CA.

4. **Android Certificate Installation:**
   - Go to **Settings** > **Security** > **Install from storage**.
   - Select the downloaded certificate and follow the prompts.

---

## Step 6: Intercept Traffic

Once the certificate is installed, and the proxy is configured, you can intercept and inspect all HTTP and HTTPS traffic passing through the mobile device.

1. On your Windows machine, open the **mitmweb** interface at `http://127.0.0.1:8081/`.
2. Start using apps on your mobile device, and traffic should appear in the mitmweb interface for inspection.

---

## Step 7: Extract API Requests into Postman

Once you have captured API requests using mitmweb, you can easily export them to **Postman** for further analysis and testing.

1. In the **mitmweb** interface, select the HTTP/HTTPS request you want to analyze.
2. Right-click the request and select **Copy as cURL**.
3. Open **Postman**.
4. In the **Postman** interface, select **Import** > **Raw Text**.
5. Paste the cURL command copied from mitmweb into Postman.
6. Click **Import**, and the request will be imported into Postman, where you can edit, test, and analyze it further.

---

## Troubleshooting

1. **No traffic showing up?**
   - Ensure that the mobile device is connected to the same Wi-Fi network as your Windows 11 machine.
   - Check if you have correctly configured the IP address and port settings in the proxy configuration.

2. **HTTPS traffic not decrypted?**
   - Make sure the mitmproxy CA certificate is correctly installed on your mobile device.

---

## Useful Links

- [Download mitmproxy](https://mitmproxy.org/)
- [Download Python](https://www.python.org/downloads/)
- [Download Postman](https://www.postman.com/downloads/)

---

## License

This guide is licensed under the MIT License.
