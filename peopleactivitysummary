import requests
from bs4 import BeautifulSoup
import streamlit as st

def get_summary(profile_url):
    # Send a GET request to the LinkedIn profile URL
    response = requests.get(profile_url)

    # Parse the HTML content
    soup = BeautifulSoup(response.content, 'html.parser')

    # Extract the last activity details
    last_activity = soup.find('section', class_='pv-recent-activity-section')
    if last_activity is None:
        return None
    last_activity_text = last_activity.text.strip()

    # Generate a short summary of two paragraphs
    paragraphs = last_activity_text.split('\n')
    summary = '\n\n'.join(paragraphs[:2])

    return summary

# Streamlit user interface
st.title('LinkedIn Profile Summary')
profile_url = st.text_input('Enter LinkedIn Profile URL:', '')
if st.button('Generate Summary'):
    if profile_url:
        summary = get_summary(profile_url)
        if summary:
            st.success(summary)
        else:
            st.warning('No recent activity found on the LinkedIn profile.')
    else:
        st.warning('Please enter a LinkedIn profile URL.')
