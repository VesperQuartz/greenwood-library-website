🔍 Key Concepts Covered:
🧩 1. Importance of Error Handling

    Helps make scripts more reliable, robust, and user-friendly.

    Accounts for issues like invalid input, failed commands, or unavailable resources.

⚙️ 2. Implementation Steps

    Identify Potential Errors: Anticipate failures in file operations, input, or commands.

    Use Conditional Logic: Use if, elif, and else blocks to handle different outcomes, especially by checking command exit status $?.

    Display Informative Messages: Notify the user clearly when an error occurs and suggest corrective steps.

🪣 3. Real-world Scenario – S3 Bucket Creation

    Demonstrates how to check if a bucket already exists using:

    aws s3api head-bucket --bucket "$bucket_name"

    If it exists, the script prints a message instead of attempting to recreate it.

    This avoids duplication and prevents the script from failing on subsequent runs.

💡 Example Function: create_s3_buckets

    Loops through department names.

    Checks for existing buckets.

    Only creates new ones if they don’t already exist.

    Includes feedback messages for both success and failure outcomes.
