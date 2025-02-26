# Cloudflare Backup Actions

This GitHub Actions workflow provides a simple and automated way to back up your Cloudflare zones and DNS records to JSON files, stored securely within your private GitHub repository.

[![Zones Backup Status](https://github.com/fabriziosalmi/cloudflare-backup-actions/actions/workflows/zones.yml/badge.svg)](https://github.com/fabriziosalmi/cloudflare-backup-actions/actions/workflows/zones.yml) [![Records Backup Status](https://github.com/fabriziosalmi/cloudflare-backup-actions/actions/workflows/records.yml/badge.svg)](https://github.com/fabriziosalmi/cloudflare-backup-actions/actions/workflows/records.yml)

## Key Features

*   **Scheduled Backups:** Automate backups on a regular schedule using cron expressions.
*   **Comprehensive Coverage:** Backs up all zones associated with your Cloudflare account.
*   **Detailed Records:** Captures all DNS records for each zone.
*   **Secure Storage:** Stores backups as JSON files within your private GitHub repository.
*   **Sequential Execution:** Ensures zone backups complete successfully before attempting record backups.

## Getting Started

Follow these steps to set up and configure your Cloudflare backup workflow:

1.  **Fork the Repository:** Create a copy of this repository in your GitHub account.

2.  **Set Repository to Private:** **IMPORTANT:** Change the repository visibility to **private**. This is crucial to prevent exposing your Cloudflare configuration data.

    > **⚠️ WARNING: SECURITY ALERT! ⚠️**
    >
    > Navigate to `https://github.com/YOUR_USERNAME/YOUR_REPO/settings` and change the repository visibility to **Private**.  Failure to do so will expose your Cloudflare zones and records to the public. We are not responsible for any security breaches resulting from neglecting this step. If you accidentally made the repository public, delete the fork immediately.

3.  **Enable GitHub Actions:** If GitHub Actions are not already enabled for your repository, enable them in the repository settings.

4.  **Create a Cloudflare API Token:** Generate a Cloudflare API token with the necessary permissions. There are two options:

    *   **Option 1 (Quick Setup):** Create a token with the "Read all resources" permission. This provides the broadest access. (Navigate to [Cloudflare API Tokens](https://dash.cloudflare.com/profile/api-tokens))

    *   **Option 2 (Recommended):** Create a custom token with specific read permissions for only the zones you intend to back up. This follows the principle of least privilege and is a more secure approach.

5.  **Set the `CLOUDFLARE_API_TOKEN` Secret:** Store your Cloudflare API token as a GitHub Actions secret within your repository.

    *   Go to `https://github.com/YOUR_USERNAME/YOUR_REPO/settings/secrets/actions`
    *   Create a new repository secret named `CLOUDFLARE_API_TOKEN` and paste your API token as the value.

6.  **Configure the Backup Schedule:**  Edit the `zones.yml` file to define the schedule for your backups using a cron expression.

    ```yaml
    on:
      schedule:
        - cron: '0 2 * * *' # Runs daily at 2:00 AM UTC
      workflow_dispatch: # Enables manual triggering of the workflow
    ```

    *   The example above runs the backup daily at 2:00 AM UTC.  Adjust the cron expression to match your desired backup frequency.  Use a cron generator ([crontab guru](https://crontab.guru/)) to help create your expression.

7.  **Automatic Records Backup:** The `records.yml` workflow is configured to run automatically after the `zones.yml` workflow completes successfully. This ensures that zone data is available before attempting to back up records.

8.  **Enjoy Automated Backups!** Your Cloudflare zones and records will now be backed up automatically according to the schedule you configured.

## Important Considerations

*   **Security:** Always keep your repository private to protect your sensitive Cloudflare data. Regularly review your Cloudflare API token permissions.
*   **Cron Expressions:** Understand how cron expressions work to schedule backups according to your specific needs.
*   **Storage:** Consider the storage implications of regularly backing up your data.  Large Cloudflare configurations may result in significant storage usage over time.
*   **Restoration:** This workflow provides backups in JSON format.  A separate process or script would be required to restore the data to Cloudflare.  This is outside the scope of this action.

## Contributing

Contributions are welcome! Please feel free to submit pull requests to improve the workflow or add new features.
