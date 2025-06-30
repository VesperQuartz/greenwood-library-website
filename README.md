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


#!/bin/bash

# Function to create S3 buckets for different departments with error handling

create_s3_buckets() {
    company="datawise"
    departments=("Marketing" "Sales" "HR" "Operations" "Media")

    for department in "${departments[@]}"; do
        bucket_name="${company,,}-${department,,}-data-bucket"  # lowercase bucket name
        region="us-east-1"  # Change to your preferred region

        echo "Processing bucket: $bucket_name"

        # Check if bucket already exists
        aws s3api head-bucket --bucket "$bucket_name" 2>/dev/null
        if [ $? -eq 0 ]; then
            echo "⚠️  Bucket '$bucket_name' already exists. Skipping creation."
        else
            # Try to create the bucket
            aws s3api create-bucket --bucket "$bucket_name" --region "$region" --create-bucket-configuration LocationConstraint="$region" 2>/dev/null

            if [ $? -eq 0 ]; then
                echo "✅ Successfully created bucket: $bucket_name"
            else
                echo "❌ Failed to create bucket: $bucket_name. Please check your AWS credentials and region settings."
            fi
        fi
        echo "-----------------------------------------"
    done
}

# Call the function
create_s3_buckets

