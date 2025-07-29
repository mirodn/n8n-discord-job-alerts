# n8n Workflow: Job Alerts on Discord

This basic workflow fetches job listings from **SwissDevJobs API**, filters them by location, category, and experience level, then posts formatted alerts to a Discord channel. It also ensures no duplicates and cleans up old entries after 6 weeks using Supabase.

## Features

- Fetch job postings from SwissDevJobs API
- Rotate  User-Agent headers to avoid API blocking
- Filter jobs by:
  - Location (e.g., Zurich)
  - Tech Category (e.g., IT, Security, Architect, Business)
  - Experience Level (exclude Senior)
- Send formatted Discord messages with job details
- Prevent duplicate alerts using Supabase
- Automatically delete old job records after 6 weeks

## Requirements

- [n8n](https://n8n.io) (self-hosted or cloud)
- Discord Bot Token ([Discord Developer Portal](https://discord.com/developers/applications))
- Supabase Project (with table `sent_jobs`)

## Setup Instructions

1. Clone the Repository

    ```bash
    git clone https://github.com/mirodn/n8n-discord-job-alerts.git
    ```

2. Import Workflow into n8n

    - Go to n8n UI → Import Workflow
    - Upload job-alerts-discord.json

3. Configure Credentials

    - Add your Discord Bot API in n8n Credentials
    - Add your Supabase API Key and URL

4. Create Supabase Table

    ```sql
    CREATE TABLE sent_jobs (
        id SERIAL PRIMARY KEY,
        job_id TEXT UNIQUE,
        sent_at TIMESTAMP DEFAULT NOW()
    );
    ```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## Support

If you have any questions or need help, feel free to open an issue on GitHub.
