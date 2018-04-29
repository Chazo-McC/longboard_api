# longboard_api
PHP ReST API used to receive skate session data from an Arduino Device.

## How It Works
- The Arduino Device calls up a Shell Script (found here: https://github.com/CharlesPeterMcCarthy/longboard_shell_script)
- JSON data is received in this script
- The data recevied must have:
  - API Key (Must match stored API Key)
  - Device Credentials (Name & Pass)
  - Speed Logs
  - Total Distance
- The device name and password is checked to see if it matches a registered / approved device stored in the database
- The user `email` & `device_id` corresponding to the registered / approved device is retrieved from the database
- Start time & end time is calculated
- Total distance, start time and end time are stored in `skate_sessions` MySQL table and `sessionID` is generated
- Speeds logs are stored in `skate_speeds` MySQL table
- Response data is calculated:
  - Total skate time
  - Average speed
  - Highest speed
- An Email is sent to the user containing:
  - Alert for new skate data
  - Session ID
  - Total skate time
  - Total distance
  - Average speed
  - Highest speed
  - A link to view more in-depth info on the skate session
- Response is returned to Shell Script (on Arduino)

### To Use
- Change `{{SERVER_NAME}}` to the Server Name
- Change `{{USER_NAME}}` to the MySQL User Name
- Change `{{PASSWORD}}` to the MySQL User Password
- Change `{{DB_NAME}}` to the MySQL Database Name
- Change `{{API_KEY}}` to the required API key
