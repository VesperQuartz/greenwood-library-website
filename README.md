```bash
#!/bin/sh env
# Function to create S3 buckets for different departments
create_s3_buckets() {"\n    company=\"datawise\"\n    departments=(\"Marketing\" \"Sales\" \"HR\" \"Operations\" \"Media\")\n    \n    for department in \"${departments[@]"}"; do
        bucket_name="${company}-${department}-Data-Bucket"

        # Check if the bucket already exists
        if aws s3api head-bucket --bucket "$bucket_name" &>/dev/null; then
            echo "S3 bucket '$bucket_name' already exists."
        else
            # Create S3 bucket using AWS CLI
            aws s3api create-bucket --bucket "$bucket_name" --region your-region
            if [ $? -eq 0 ]; then
                echo "S3 bucket '$bucket_name' created successfully."
            else
                echo "Failed to create S3 bucket '$bucket_name'."
            fi
        fi
    done
}

```
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

