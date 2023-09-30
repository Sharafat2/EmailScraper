# EmailScraper
# Scrape any email off any website 


import re
from selenium import webdriver

# Specify the path to ChromeDriver
chrome_driver = '/usr/local/bin/chromedriver'

# Set up Chrome WebDriver options
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no-sandbox')
chrome_options.binary_location = '/usr/bin/google-chrome'  # Optional: Set the path to the Chrome binary if not in the system PATH

# Set the ChromeDriver executable path
chrome_options.add_argument(f'--webdriver={chrome_driver}')

# Initialize the WebDriver
driver = webdriver.Chrome(options=chrome_options)

try:
    driver.get("https://www.randomlists.com/email-addresses?qty=100")

    # Get the page source code
    page_source = driver.page_source

    # Regex to find e-mails
    EMAIL_REGEX = r"""(your regex pattern here)"""

    # Create a list and add all the emails
    list_of_emails = []

    # Finds all the emails
    for re_match in re.finditer(EMAIL_REGEX, page_source):
        list_of_emails.append(re_match.group())

    # Lists all the e-mails that we managed to scrape
    for i, email in enumerate(list_of_emails):
        print(f'{i + 1}: {email}')
except Exception as e:
    print(f"An error occurred: {str(e)}")
finally:
    # Close the driver
    driver.quit()
