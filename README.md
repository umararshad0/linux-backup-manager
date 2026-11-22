# Linux Backup Manager

A Bash backup utility that creates timestamped archives, verifies them, logs results, and applies retention.

## Problem & Solution

- **Problem:** Manual backups can be inconsistent, unverified, and left to accumulate until storage runs out.
- **Approach:** The script validates paths, creates and checks a compressed archive, and keeps the seven newest matching backups.
- **Outcome:** Each run leaves a timestamped, verified backup and an activity log for review.

## Screenshots

<table>
  <tr>
    <td align="center" valign="top">
      <img src="docs/screenshots/successful-backup.png" alt="Successful Backup" width="420">
      <br><sub>Successful Backup</sub>
    </td>
    <td align="center" valign="top">
      <img src="docs/screenshots/retention-policy.png" alt="Backup Retention" width="420">
      <br><sub>Backup Retention</sub>
    </td>
  </tr>
  <tr>
    <td align="center" valign="top">
      <img src="docs/screenshots/automated-tests.png" alt="Automated Tests" width="420">
      <br><sub>Automated Tests</sub>
    </td>
    <td></td>
  </tr>
</table>

## Architecture Diagram

![Linux Backup Manager Architecture](docs/diagrams/architecture.png)

### Architecture Notes

The diagram below illustrates the Linux Backup Manager workflow, including source validation, archive creation, integrity verification, logging, and backup retention.


The editable diagram source is available here: [linux-backup-manager.drawio](docs/diagrams/linux-backup-manager.drawio).

## Project Details

### Features


- Timestamped `.tar.gz` backups
- Source directory validation
- Archive integrity verification
- Timestamped activity and error logs
- Automatic retention of the seven newest matching backups
- Automated tests
- Compatible with macOS Bash 3.2 and common Linux Bash environments


### Requirements


- Bash
- `tar`
- Standard Unix utilities


### Usage


Make the script executable:

```bash
chmod +x backup.sh
```

Run a backup:

```bash
./backup.sh /path/to/source /path/to/backups
```

Example:

```bash
mkdir -p ~/backup-demo/source
echo "Hello backup" > ~/backup-demo/source/example.txt

./backup.sh ~/backup-demo/source ~/backup-demo/backups
```


### Logs


The script creates `backup.log` in the backup destination. It records timestamps, backup results, and retention cleanup activity.


### Retention Policy


The script keeps the seven newest matching backup archives in the selected destination and removes older matching archives after a successful archive verification.

**Important:** Test the script with disposable files before using it for important data. This project is a learning tool, not a replacement for a tested disaster-recovery system or off-site backup strategy.

Retention runs only after a new archive has been created and verified. It removes older matching `backup_*_<source>.tar.gz` files from the destination, so use a dedicated backup directory and confirm its contents before the first run.


### Automated Tests


Run the test suite:

```bash
chmod +x tests/test-backup.sh
./tests/test-backup.sh
```

The tests check backup creation, archive contents, missing-source handling, and seven-backup retention.


### Project Structure


```text
linux-backup-manager/
├── backup.sh
├── tests/
│   └── test-backup.sh
├── docs/
│   ├── diagrams/
│   └── screenshots/
├── .github/workflows/ci.yml
└── README.md
```


### Skills Demonstrated


- Bash scripting
- Linux and macOS command-line tools
- File archiving with tar
- Input validation and error handling
- Logging and retention automation
- Automated testing
- Git and GitHub


### Future Improvements


- Dry-run mode
- Configurable retention count
- Exclusion patterns
- Restore command


### Continuous Integration


This project uses GitHub Actions to automatically validate and test the Bash backup utility on an Ubuntu Linux runner.

The CI workflow runs on pushes and pull requests and performs the following checks:

- Validates Bash syntax for the backup script and test script.
- Runs automated tests for backup creation, archive contents, invalid source handling, and backup retention.
- Reports the workflow status through GitHub Actions.

Workflow configuration: `.github/workflows/ci.yml`

## Author

**Umar Arshad** · [GitHub](https://github.com/umararshad0)
