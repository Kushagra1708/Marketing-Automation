from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

# Set up Selenium WebDriver
driver = webdriver.Chrome('path_to_chromedriver')  # Replace with the path to your ChromeDriver executable
driver.get('https://www.linkedin.com/')
time.sleep(2)

# Log in to LinkedIn
email = 'your_email@example.com'  # Replace with your LinkedIn email
password = 'your_password'  # Replace with your LinkedIn password

email_field = driver.find_element_by_id('session_key')
password_field = driver.find_element_by_id('session_password')
email_field.send_keys(email)
password_field.send_keys(password)
password_field.send_keys(Keys.RETURN)
time.sleep(5)

# Define competitors' LinkedIn profiles to monitor
competitor_profiles = ['competitor1', 'competitor2', 'competitor3']  # Replace with the LinkedIn profiles of your competitors

# Monitor new connections of competitor profiles
for profile in competitor_profiles:
    profile_url = f'https://www.linkedin.com/in/{profile}/'
    driver.get(profile_url)
    time.sleep(2)

    # Click on 'Connections' tab
    connections_tab = driver.find_element_by_partial_link_text('Connections')
    connections_tab.click()
    time.sleep(2)

    # Scroll to load more connections
    scroll_div = driver.find_element_by_class_name('mn-connections')
    driver.execute_script("arguments[0].scrollTop = arguments[0].scrollHeight", scroll_div)
    time.sleep(2)

    # Get new connections
    new_connections = driver.find_elements_by_class_name('mn-connection-card__picture')

    # Iterate through new connections
    for connection in new_connections:
        connection.click()
        time.sleep(2)

        # Extract relevant information (About Us, job description, recent posts) from the connection's profile
        about_section = driver.find_element_by_id('about-section')
        about_text = about_section.text if about_section else ''

        job_section = driver.find_element_by_class_name('experience-section')
        job_text = job_section.text if job_section else ''

        posts_section = driver.find_element_by_class_name('core-rail')
        posts_text = posts_section.text if posts_section else ''

        # Generate personalized connection request message based on the extracted information
        personalized_message = f"Hi! I noticed we have some shared interests and connections. I'd love to connect and explore potential synergies. {about_text}\n\n{job_text}\n\n{posts_text}"

        # Send connection request
        send_button = driver.find_element_by_class_name('ml1')
        send_button.click()
        time.sleep(2)

        add_note_button = driver.find_element_by_class_name('artdeco-button--tertiary')
        add_note_button.click()
        time.sleep(2)

        message_field = driver.find_element_by_id('custom-message')
        message_field.send_keys(personalized_message)

        send_now_button = driver.find_element_by_class_name('ml1')
        send_now_button.click()
        time.sleep(2)

# Close the browser
driver.quit()
