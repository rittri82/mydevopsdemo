# GCS Asset Query and Upload Tool

## Overview
This tool performs asset queries on Google Cloud Platform (GCP) resources and uploads the results to Google Cloud Storage (GCS). It generates both JSON and CSV outputs, with the CSV containing hyperlinked requirement IDs for easy reference.

## Features
- Executes configurable asset queries against GCP resources
- Groups results by requirement IDs
- Generates timestamped CSV output with hyperlinked requirements
- Creates JSON backup of all query results
- Automatically uploads results to specified GCS bucket
- Includes error handling and detailed logging
- Supports multiple requirement queries with URL mapping

## Prerequisites
- Python 3.x
- Google Cloud SDK installed and configured
- Appropriate GCP permissions:
  - Cloud Asset Inventory API access
  - GCS bucket read/write permissions
  - Required IAM roles for asset querying

## Required Python Packages
```
google-cloud-storage
google-cloud-asset
google-protobuf
pytz
```

## Installation
1. Clone the repository
2. Install required packages:
```bash
pip install google-cloud-storage google-cloud-asset google-protobuf pytz
```
3. Configure your GCP credentials
4. Update the configuration settings in `settings.py`

## Configuration
The following configurations need to be set up before running the tool:

1. In `settings.py`:
   - Define your query_groups dictionary with requirement IDs and corresponding queries
   - Set up any environment-specific variables

2. In the main script:
   - Update `bucket_name` with your GCS bucket name
   - Update `folder_name` with your desired GCS folder path
   - Configure `requirement_urls` dictionary with your requirement documentation links

## Usage
Run the script using:
```bash
python gcs_test1.py
```

The script will:
1. Execute all configured asset queries
2. Generate a timestamped CSV file with results
3. Create a JSON backup file
4. Upload results to the specified GCS bucket
5. Clean up local files (if upload is successful)

## Output Files
The tool generates two types of output files:

1. CSV File (`asset_query_grouped_results_YYYYMMDD_HHMMSS.csv`):
   - Project ID
   - Zone
   - Instance ID
   - Full Path
   - Requirement ID (hyperlinked)

2. JSON File (`asset_query_grouped_results.json`):
   - Complete query results grouped by requirement ID
   - Raw data backup

## Functions

### `upload_to_gcs(source_fname: str, bucket_name: str, folder_name: str)`
Uploads a file to GCS bucket in the specified folder.

### `save_to_csv(all_results: Dict[str, List[dict]], requirement_urls: Dict[str, str], filename: str)`
Saves query results to a CSV file with hyperlinked requirement IDs.

### `main()`
Orchestrates the entire process of querying, saving, and uploading results.

## Error Handling
- Comprehensive error checking for file operations
- Detailed logging of all operations
- File existence verification before uploads
- Exception tracebacks for debugging
- Keeps local files for debugging if upload fails

## Best Practices
- Use environment variables for sensitive configuration
- Regularly update requirement URLs
- Monitor GCS bucket permissions
- Review query results periodically
- Keep query_groups in settings.py up to date

## Contributing
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License
[Specify your license here]

## Support
For support, please contact [specify contact information]

---
**Note**: This tool is designed for use with Google Cloud Platform services. Ensure you have appropriate access and permissions before use.
