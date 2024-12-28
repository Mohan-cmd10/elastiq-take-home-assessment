from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from webdriver_manager.chrome import ChromeDriverManager
import time

def test_search_table():
    driver = webdriver.Chrome(ChromeDriverManager().install())

    try:
        # Open the page
        driver.get("https://www.lambdatest.com/selenium-playground/table-sort-search-demo")
        
        # Find the search box and search for 'New York'
        search_box = driver.find_element(By.XPATH, "//*[@id='example_filter']/label/input")
        search_box.clear()
        search_box.send_keys("New York")
        search_box.send_keys(Keys.RETURN)

        # Wait for the search results to load
        time.sleep(2)

        # Check if 5 rows are displayed after the search
        rows = driver.find_elements(By.XPATH, "//*[@id='example']/tbody/tr")
        assert len(rows) == 5, f"Expected 5 rows but found {len(rows)}"

        # Verify that total entries shown are 24
        total_entries = driver.find_element(By.XPATH, "//*[@id='example_info']").text
        assert "24" in total_entries, f"Expected total entries to be 24 but found {total_entries}"
    
    finally:
        driver.quit()

if __name__ == "__main__":
    test_search_table()
