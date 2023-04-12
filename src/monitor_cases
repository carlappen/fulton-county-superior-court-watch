import requests
import schedule
import time

# Set up API endpoint and case numbers to monitor
api_endpoint = 'https://sharefulton.fultoncountyga.gov/resource/e8ne-c2s2.json'
case_numbers = ['01SC00767']

def get_case_status(case_number):
    """Retrieve case data from the API and return case status"""
    response = requests.get(f'{api_endpoint}/{case_number}')
    response_json = response.json()
    case_status = response_json['caseStatus']
    return case_status

def monitor_cases():
    """Check case status for each case number and print any changes"""
    for case_number in case_numbers:
        current_status = get_case_status(case_number)
        if case_number in last_statuses and current_status != last_statuses[case_number]:
            print(f'Case {case_number} changed from {last_statuses[case_number]} to {current_status}')
        last_statuses[case_number] = current_status

if __name__ == '__main__':
    last_statuses = {}
    for case_number in case_numbers:
        last_statuses[case_number] = get_case_status(case_number)
    # Schedule the script to run every hour
    schedule.every().hour.do(monitor_cases)
    while True:
        schedule.run_pending()
        time.sleep(1)
