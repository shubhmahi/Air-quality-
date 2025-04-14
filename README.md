# Air-quality-
#Please run the code enter the Captcha verify it come back to code press enter and then code will take over the URL again.
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time
# Create instance of Chrome WebDriver (make sure chromedriver is in PATH)
driver = webdriver.Chrome()

# Open the target URL
driver.get("https://airquality.cpcb.gov.in/ccr/#/caaqm-dashboard-all")

# At this point, a captcha pop-up appears. Solve it manually then press ENTER in the terminal.
input("Please solve the captcha in the browser manually and click Verify. Then press ENTER here to continue...")

# Give additional wait time (4 sec) for the site to load fully after captcha verification.
time.sleep(4)


# Update the XPath/CSS selector to locate the Comparison data tab button.
try:
    comparison_tab = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//button[contains(@class, 'btn btn-link') and contains(text(), 'Comparison Data')]"))
      #  EC.element_to_be_clickable((By.XPATH, '//input[@class="btn btn-link"]'))
    )
    comparison_tab.click()
except Exception as e:
    print("Error clicking the Comparison Data tab:", e)
    driver.quit()
    exit()

# Wait a moment for the new tab to open
time.sleep(2)

# Switch to the newly opened tab (assumes it is the last one in the window_handles list)
driver.switch_to.window(driver.window_handles[-1])

# Step 1: Click on the 'State Name' dropdown and choose 'Delhi'
try:
    state_dropdown = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//button[contains@class,'toggle')]/following-sibling::div"))
    )
    state_dropdown.click()

    # Wait and choose Delhi from the dropdown options
    delhi_option = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.XPATH, "//span[text()='Delhi']"))
    )
    delhi_option.click()
except Exception as e:
    print("Error selecting State Name:", e)

# Step 2: Click on the 'City Name' dropdown and choose 'Delhi'
try:
    city_dropdown = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//label[contains(text(),'City Name')]/following-sibling::div"))
    )
    city_dropdown.click()

    # Wait and choose Delhi from the dropdown options
    city_option = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.XPATH, "//span[text()='Delhi']"))
    )
    city_option.click()
except Exception as e:
    print("Error selecting City Name:", e)

# Step 3: Click on the 'Station Name' dropdown and choose 'Select all'
try:
    station_dropdown = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//label[contains(text(),'Station Name')]/following-sibling::div"))
    )
    station_dropdown.click()

    # Wait and click on the "Select all" option
    select_all_station = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.XPATH, "//span[text()='Select all']"))
    )
    select_all_station.click()
except Exception as e:
    print("Error selecting Station Name:", e)

# Step 4: Click on the 'Parameter' dropdown and choose 'Select all'
try:
    parameter_dropdown = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//label[contains(text(),'Parameter')]/following-sibling::div"))
    )
    parameter_dropdown.click()

    # Wait and click on the "Select all" option for parameters
    select_all_parameter = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.XPATH, "//span[text()='Select all']"))
    )
    select_all_parameter.click()
except Exception as e:
    print("Error selecting Parameter:", e)

# Step 5: Click the 'Add Station' button
try:
    add_station_button = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//button[contains(text(),'Add Station')]"))
    )
    add_station_button.click()
except Exception as e:
    print("Error clicking Add Station:", e)

# Step 6: Click on 'Report Format' dropdown and choose 'Tabular'
try:
    report_format_dropdown = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//label[contains(text(),'Report Format')]/following-sibling::div"))
    )
    report_format_dropdown.click()

    tabular_option = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.XPATH, "//span[text()='Tabular']"))
    )
    tabular_option.click()
except Exception as e:
    print("Error selecting Report Format:", e)

# Step 7: Click on 'Criteria' dropdown and choose '1 hour'
try:
    criteria_dropdown = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//label[contains(text(),'Criteria')]/following-sibling::div"))
    )
    criteria_dropdown.click()

    criteria_option = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.XPATH, "//span[text()='1 hour']"))
    )
    criteria_option.click()
except Exception as e:
    print("Error selecting Criteria:", e)

# Step 8: Set 'Date From' to 1 Nov 2024
try:
    # Click on Date From field to open the date picker
    date_from_field = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//input[@placeholder='Date From']"))
    )
    date_from_field.click()
    
    # Option 1: If the date picker is text-input type, you can clear and enter the date
    date_from_field.clear()
    date_from_field.send_keys("01-11-2024")
    
    # Option 2: If it is a calendar widget, then use appropriate clicks:
    # For example, click on the appropriate date using an XPath selector (update with actual locator)
    # date_option = WebDriverWait(driver,10).until(
    #     EC.element_to_be_clickable((By.XPATH, "//td[@data-day='1' and @data-month='10' and @data-year='2024']"))
    # )
    # date_option.click()
except Exception as e:
    print("Error setting 'Date From':", e)

# Step 9: Set 'Date To' to 30 Nov 2024
try:
    # Click on Date To field to open the date picker
    date_to_field = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//input[@placeholder='Date To']"))
    )
    date_to_field.click()
    
    # Option 1: Enter text directly(NOT WORKING)
    date_to_field.clear()
    date_to_field.send_keys("30-11-2024")
    
    # Option 2: Use the calendar widget clicks (update with actual XPath if needed)
    date_option = WebDriverWait(driver,10).until(
         EC.element_to_be_clickable((By.XPATH, "//td[@data-day='30' and @data-month='10' and @data-year='2024']"))
     )
    date_option.click()
except Exception as e:
    print("Error setting 'Date To':", e)

# Click the 'Submit' button and wait for the report page to load
try:
    submit_button = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//button[contains(text(),'Submit')]"))
    )
    submit_button.click()
    
    # Wait for 7 seconds after submit to allow the report page to load
    time.sleep(7)
except Exception as e:
    print("Error clicking Submit:", e)

# DOWNLOAD THE EXCEL REPORT 
try:
    # Update the XPath selector to match the download Excel element.
    excel_icon = WebDriverWait(driver, 15).until(
        EC.element_to_be_clickable((By.XPATH, "//i[@class='excel-download-icon'] | //button[contains(.,'Excel')]"))
    )
    excel_icon.click()
    
    print("Excel report download initiated.")
except Exception as e:
    print("Error clicking the Excel download icon:", e)

# OPTIONAL: Wait for some time to ensure the file is downloaded, then close the browser.
time.sleep(10)
driver.quit()
