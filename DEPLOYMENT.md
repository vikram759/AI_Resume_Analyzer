# Deployment Guide for Smart AI Resume Analyzer

This guide provides instructions for deploying the Smart AI Resume Analyzer application locally and on Streamlit Cloud, with a focus on resolving Chrome webdriver issues.

## Local Deployment

### Prerequisites

- Python 3.7 or higher
- Chrome browser installed
- pip for installing dependencies

### Steps for Windows

1. Clone the repository
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
3. Run the application using the Python script:
   ```
   python run_app.py
   ```
   This script will automatically set up chromedriver and start the application.

   Alternatively, you can run the batch file:
   ```
   startup.bat
   ```

### Steps for Linux/Mac

1. Clone the repository
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
3. Run the setup script to install the correct chromedriver:
   ```
   python setup_chromedriver.py
   ```
4. Run the application:
   ```
   streamlit run app.py
   ```
   Alternatively, you can use the startup script which handles both chromedriver setup and application startup:
   ```
   chmod +x startup.sh
   ./startup.sh
   ```

## Streamlit Cloud Deployment

When deploying to Streamlit Cloud, you need to ensure Chrome is available. Our application includes multiple fallback mechanisms to handle this.

### Steps for Streamlit Cloud

1. Push your code to a GitHub repository
2. Create a new app in Streamlit Cloud pointing to your repository
3. Make sure your `requirements.txt` includes all necessary dependencies:
   - `selenium>=4.10.0`
   - `webdriver-manager>=4.0.0`
   - `chromedriver-autoinstaller>=0.6.2`
4. Ensure the `packages.txt` file is in your repository with:
   ```
   chromium
   chromium-driver
   libglib2.0-0
   libnss3
   libgconf-2-4
   libfontconfig1
   xvfb
   wget
   unzip
   ```

### Troubleshooting Streamlit Cloud

If you encounter issues with Chrome on Streamlit Cloud:

1. Check the logs for specific error messages
2. Try adding a custom command to run the setup script before the app starts:
   - In the Streamlit Cloud settings, add a "Main file path" of `run_app.py` instead of `app.py`

## Troubleshooting Common Issues

### Error: "Service unexpectedly exited"

This usually indicates that Chrome cannot be started. Ensure:

- Chrome is installed
- You have the correct permissions
- You're using the `--no-sandbox` option in headless environments

### Error: "Chrome version must be between X and Y"

This indicates a version mismatch between Chrome and chromedriver:

- Run the `setup_chromedriver.py` script to install the matching chromedriver version
- The script automatically detects your Chrome version and downloads the compatible chromedriver

### Error: "Permission denied" when installing chromedriver

This is a permission issue:

- Try running the application with administrator privileges
- Ensure the user has write permissions to the installation directory
- Use the `setup_chromedriver.py` script which installs chromedriver in the user's home directory

### Windows-specific issues

If you encounter issues on Windows:

- Make sure Chrome is installed in the standard location
- Try running the application as administrator
- Use the `run_app.py` script which handles setup automatically
- Check Windows Defender or antivirus software that might be blocking chromedriver

## Additional Resources

- [Selenium Documentation](https://www.selenium.dev/documentation/)
- [Chrome for Testing](https://developer.chrome.com/docs/chromium/chrome-for-testing)
- [Streamlit Deployment](https://docs.streamlit.io/streamlit-cloud/get-started/deploy-an-app)