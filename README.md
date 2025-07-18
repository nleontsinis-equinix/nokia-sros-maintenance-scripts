# Nokia SROS Maintenance Scripts

A collection of Python automation scripts for Nokia SROS devices, including:

- **bulk_card_and_file_report_html.py**: Card/flash status reporting with HTML dashboard  

## Repository Structure

nokia-sros-maintenance-scripts/
├── reporting/
│ └── bulk_card_and_file_report_html.py
├── my_routers.txt
└── README.md


- **reporting/**  
  Contains scripts to collect `show card detail` and `file list` outputs, parse CF2/CF3 size, utilization, and state, and generate a color‐coded HTML report.

- **my_routers.txt**  
  Plain‐text list of hostnames or IPs (one per line) to target.

## Prerequisites

- Python 3.7+  
- [Netmiko](https://pypi.org/project/netmiko/)  
- SSH connectivity to your Nokia SROS devices with MD-CLI enabled

Install dependencies in a virtualenv:

```bash
python3 -m venv venv
source venv/bin/activate
pip install netmiko

Usage
1. Prepare my_routers.txt

Populate the file with one router hostname or IP per line. Comment out entries with #.

# my_routers.txt
spare-7750sr1.xy1
spare-7750sr1.xy2
10.0.0.1
10.0.0.2


Reporting Script

cd reporting
chmod +x bulk_card_and_file_report_html.py
./bulk_card_and_file_report_html.py


    Prompts for SSH username/password.

    Runs:

        show card detail | no-more

        file list | no-more

    Parses CF2/CF3 Size, Percent Used, and Administrative/Operational state.

    Generates:

        card_report.txt (raw CLI dumps)

        file_lists.txt (raw file listings)

        report.html — color‐coded table with ✅/⚠️ icons and green/yellow/red backgrounds.

    Prints summary of unreachable routers and “not equipped” flashes.

Customization

    Image lists: Edit remove_cmds and remove_directory_cmds arrays in bulk_nokia_cleanup.py.

    Size tolerances & thresholds: Adjust EXP_CF?_SIZE_MB, CF?_TOLERANCE, and PCT_THRESHOLD in bulk_card_and_file_report_html.py.

    SSH settings: Modify Netmiko timeout or device_type if needed.


