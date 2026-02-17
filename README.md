# awsinfo

A Python command-line tool to analyze and retrieve information from various AWS services in your AWS account. It provides detailed reports about S3 buckets, EBS volumes, KMS keys, Load Balancers, Glue databases, and Lambda functions.

## Features

- **S3 Buckets**: List all S3 buckets with optional checks for last modification date, encryption status, and public access permissions
- **EBS Volumes**: Analyze EBS volumes and identify unused volumes
- **KMS Keys**: Review all KMS keys and their configurations
- **Load Balancers**: List all load balancers with optional public access checks
- **Glue Databases**: View all AWS Glue database resources
- **Lambda Functions**: Analyze Lambda functions in your account
- **CSV Export**: Export results to CSV files for further analysis

## Installation

### Requirements

- Python 3.10+
- boto3 (AWS SDK for Python)
- AWS credentials configured (via AWS CLI, environment variables, or credential file)

### Setup

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd awsinfo
   ```

2. Install dependencies:
   ```bash
   pip install boto3
   ```

3. Configure AWS credentials if not already done:
   ```bash
   aws configure
   ```

## Usage

### Basic Command Structure

```bash
python -m awsinfo [OPTIONS] SERVICE_NAME [SERVICE_OPTIONS]
```

### Global Options

- `--profile PROFILE_NAME`: Specify which AWS profile to use (default: 'default')
- `--csv`: Export results to a CSV file in the current directory

### Service Examples

#### S3 Buckets
```bash
# List all S3 buckets
python -m awsinfo s3

# Check S3 buckets with encryption details
python -m awsinfo s3 --encryption

# Check last modification dates of buckets
python -m awsinfo s3 --modified

# Check public access permissions
python -m awsinfo s3 --public

# Combined: check encryption, modification dates, and public access, export to CSV
python -m awsinfo s3 --encryption --modified --public --csv
```

#### EBS Volumes
```bash
# List all EBS volumes
python -m awsinfo ebs

# Show only unused EBS volumes
python -m awsinfo ebs --unused

# Export to CSV
python -m awsinfo ebs --csv
```

#### KMS Keys
```bash
# List all KMS keys
python -m awsinfo kms

# Export to CSV
python -m awsinfo kms --csv
```

#### Load Balancers
```bash
# List all load balancers
python -m awsinfo lb

# Check public access for load balancers
python -m awsinfo lb --public

# Export to CSV
python -m awsinfo lb --csv
```

#### Glue Databases
```bash
# List all Glue databases
python -m awsinfo glue

# Export to CSV
python -m awsinfo glue --csv
```

#### Lambda Functions
```bash
# List all Lambda functions
python -m awsinfo lambda

# Export to CSV
python -m awsinfo lambda --csv
```

### Using Different AWS Profiles

```bash
# Use a specific AWS profile
python -m awsinfo --profile production s3 --encryption

python -m awsinfo --profile staging ebs --unused
```

## Dependencies

The project requires:

- **boto3**: AWS SDK for Python - handles all AWS API calls
- **Python 3.10+**: The project is written in Python 3

Optional:
- AWS CLI configured for easy credential management

## Output

Results are displayed as formatted tables in the console. When using the `--csv` flag, results are also saved to a CSV file with a timestamp for easy reference and further analysis in spreadsheet applications.

## Project Structure

```
awsinfo/
├── main.py          # Main entry point
├── parsers.py       # Command-line argument parsing
├── settings.py      # Configuration and logger setup
├── tools.py         # Utility functions (CSV export, etc.)
└── services/        # Service-specific modules
    ├── s3.py
    ├── ebs.py
    ├── kms.py
    ├── lb.py
    ├── glue.py
    └── lambda_f.py
```
