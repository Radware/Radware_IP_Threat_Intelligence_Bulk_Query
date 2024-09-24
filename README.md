
# IP Batch Processor

This script processes batches of IP addresses and sends them as POST requests to the Radware Cloud API to resolve threat insights. The data retrieved is saved in a CSV file for further analysis. 

## Features
- Reads IP addresses from a file (`ip_list.txt`).
- Processes the IPs in batches and sends them to the API.
- Supports adjustable batch sizes.
- Writes the response data to a CSV file, including all unique fields.
- Handles potential server overload with pauses between batches.

## Requirements
This script requires the following libraries:

- `requests` (for making HTTP requests)
- `openpyxl` (for handling Excel file operations)
- `urllib3` (to manage warnings and SSL verification)
- `ipaddress` (for IP address validation)

To install the required packages, use the `requirements.txt` file provided.

**requirements.txt**
Ensure your `requirements.txt` contains:
```
requests
openpyxl
urllib3
```
Install the dependencies with:
```
pip install -r requirements.txt
```
## Usage

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/ip-batch-processor.git
   cd ip-batch-processor
   ```

2. **Create a virtual environment (optional but recommended):**
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Prepare your IP list:**
   - Place a list of IP addresses in a file called `ip_list.txt`, one IP per line.

5. **Run the script:**
   ```bash
   python ip_batch_processor.py
   ```

6. **Check output:**
   - The processed data will be written to `ip_data.csv` in the root directory.

7. **Set Environment Variables:**

   - Set the API_KEY and CONTEXT environment variables using the following commands:
   ```
   $env:API_KEY='<add_input>'
   $env:CONTEXT='<add_input>'
   ```
   You can also set these variables in your terminal session or use a tool like python-dotenv for more persistent settings.


## Script Configuration

### 1. **Batch Size:**
   - Adjust the batch size in the script by changing the value of the `batch_size` variable. The maximum batch size tested was 70 with over 4500 IPs.

### 2. **API Headers:**
   - Ensure that the API key, context, and other headers are configured correctly in the `headers` dictionary inside the script.

### 3. **Certificate Verification Warning:**
   - If you see warnings about unverified HTTPS requests, you can suppress these warnings using:
     ```python
     import urllib3
     urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
     ```

### 4. **Rate Limiting:**
   - The script pauses for 1 second between batch requests to avoid overwhelming the API server. You can modify this in the `time.sleep(1)` call.

### 5. **Retry Settings:**
   - Modify the maximum number of retries and the initial retry delay by adjusting `max_retries` and `initial_retry_delay`.
     
## Example

Here’s an example of how to adjust the batch size and run the script:

```python
# Adjust the batch size in the script
batch_size = 70
max_retries = 5
initial_retry_delay = 5  # seconds
```

Run the script and check the output CSV:

```bash
python ip_batch_processor.py
```

## Troubleshooting

- **400 Bad Request Errors:**
   - This typically means the payload structure is incorrect or the API is rejecting certain IPs. Double-check the format of the IP addresses and the request payload.
   
- **Insecure Request Warning:**
   - The script uses `verify=False` to bypass SSL verification. If you want to remove this, you can either provide a valid certificate or accept the risk.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributing
Feel free to open a pull request if you'd like to contribute or improve this project!

---

Happy IP processing! 😊
