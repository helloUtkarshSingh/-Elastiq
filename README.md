Selenium Test Framework
This project contains a Selenium-based automation framework to test the search functionality on a demo page ("LambdaTest Table Sort & Search Demo"). It uses pytest for testing and Selenium WebDriver for browser automation.

Prerequisites
Before running the tests, ensure that the following software is installed:

Python 3.x (Tested with Python 3.8+)
Selenium (v4.0+)
pytest (v7.0+)
Webdriver for Chrome or Firefox (depending on the browser used for tests)
You can install the necessary Python libraries via pip:

bash
Copy code
pip install selenium pytest
Also, download the appropriate ChromeDriver or GeckoDriver from the following links and place them in a directory on your machine:

ChromeDriver
GeckoDriver
Project Structure
plaintext
Copy code
.
├── resources
│   └── drivers
│       └── chromedriver.exe  # ChromeDriver binary
├── test_script.py            # Main test file with test logic
├── README.md                 # This README file
Key Components
invoke_driver(browser)
This function initializes the WebDriver for the given browser (either Chrome or Firefox). It takes a single argument browser which specifies which browser to use. The supported browsers are:

chrome (uses chromedriver.exe)
firefox (uses geckodriver.exe)
It returns a Selenium WebDriver instance, which is used for browser automation.

navigate_to_page(driver)
This function navigates the browser to the demo page:

lua
Copy code
https://www.lambdatest.com/selenium-playground/table-sort-search-demo
It waits for the page to load using implicitly_wait(5) and maximizes the browser window using driver.maximize_window(). It then asserts that the page title contains the text "Selenium Grid Online | Run Selenium Test On Cloud". If the title does not match, it will raise an assertion error.

perform_search(driver, userinput)
This function performs a search on the demo page. It takes userinput as a parameter, which is the search keyword. It locates the search box using an XPath locator and inputs the search term. After that, it checks the displayed message (e.g., "Showing 1 to 5 of 5 entries (filtered from 24 total entries)") to confirm that the search results are filtered correctly.

test_search_functionality(driver)
This is the actual test function executed by pytest. It:

Navigates to the page using navigate_to_page(driver)
Performs a search for the keyword "New York" using perform_search(driver, "New York")
Prints "test end" when the test completes.
The test uses the pytest.fixture decorator with scope="module", meaning the browser instance is shared across the entire test module.

Running the Tests
Clone the repository or download the project files to your local machine.

Ensure you have the necessary web driver (Chrome or Firefox) downloaded and placed in the correct directory.

Run the tests using pytest by executing the following command from your terminal/command prompt in the project directory:

bash
Copy code
pytest test_script.py
This will:

Open the browser.
Navigate to the page.
Perform the search functionality test.
Print the test results in the terminal.
Viewing Results: After running the tests, you will see the results printed in the terminal, including whether the assertions passed or failed.

Test Output
If all assertions pass, you will see an output similar to the following:

bash
Copy code
============================= test session starts =============================
collected 1 item

test_script.py .                                                         [100%]

============================== 1 passed in 1.23 seconds ==============================
If an assertion fails (e.g., the page title does not match), you will see an assertion error message in the terminal, indicating what went wrong.
Notes
The browser is opened in normal mode by default. If you want to run the tests in headless mode (without opening the browser UI), you can uncomment the line in the invoke_driver function:

python
Copy code
options.add_argument("--headless")
Ensure that the correct WebDriver (ChromeDriver or GeckoDriver) is used based on the browser selected.
