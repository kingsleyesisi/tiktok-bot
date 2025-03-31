import cv2
import pyautogui
import time
import numpy as np

# Load the images to search for
chrome_icon = cv2.imread("chrome.png")  # Add the Chrome icon image
if chrome_icon is None:
    print("Error: 'chrome.png' not found or could not be loaded.")
    exit()

template = cv2.imread("follow.png")
if template is None:
    print("Error: 'follow.png' not found or could not be loaded.")
    exit()

time.sleep(5)  # Add a delay before starting the search

# Locate and click on the Chrome icon
screenshot = pyautogui.screenshot()
screenshot = cv2.cvtColor(np.array(screenshot), cv2.COLOR_RGB2BGR)

# Match the Chrome icon with the screenshot
result = cv2.matchTemplate(screenshot, chrome_icon, cv2.TM_CCOEFF_NORMED)
min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(result)

if max_val > 0.8:  # Adjust the threshold as needed
    # Get the center of the matched region
    h, w, _ = chrome_icon.shape
    center_x = max_loc[0] + w // 2
    center_y = max_loc[1] + h // 2

    # Click on the center of the matched region
    pyautogui.click(center_x, center_y)
    time.sleep(2)  # Add a small delay after clicking
else:
    print("Chrome icon not found on the screen.")
    exit()

# Continuously search for the "follow" image on the screen
while True:
    # Take a screenshot of the screen
    screenshot = pyautogui.screenshot()
    screenshot = cv2.cvtColor(np.array(screenshot), cv2.COLOR_RGB2BGR)

    # Match the template image with the screenshot
    result = cv2.matchTemplate(screenshot, template, cv2.TM_CCOEFF_NORMED)
    min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(result)

    # If a match is found with sufficient confidence
    if max_val > 0.8:  # Adjust the threshold as needed
        # Get the center of the matched region
        h, w, _ = template.shape
        center_x = max_loc[0] + w // 2
        center_y = max_loc[1] + h // 2

        # Click on the center of the matched region
        pyautogui.click(center_x, center_y)
        time.sleep(2)  # Add a small delay between clicks

        # Scroll down after clicking
        pyautogui.scroll(-500)  # Adjust the scroll amount as needed
    else:
        print("Follow icon not found on the screen.")
        break
