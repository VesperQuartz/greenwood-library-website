```bash
#!/bin/sh env

# Store environment from argument
ENVIRONMENT=$1

# Function: Check if script received an argument
check_num_of_args() {
    if [ "$#" -eq 0 ]; then
        echo "Usage: $0 <environment>"
        exit 1
    fi
}

# Function: Validate AWS CLI installation
check_aws_cli() {
    if ! command -v aws &> /dev/null; then
        echo "AWS CLI is not installed. Please install it before proceeding."
        exit 1
    fi
}

# Function: Check if AWS_PROFILE environment variable is set
check_aws_profile() {
    if [ -z "$AWS_PROFILE" ]; then
        echo "AWS profile environment variable is not set."
        exit 1
    fi
}

# Function: Run setup for specified environment
activate_infra_environment() {
    case "$ENVIRONMENT" in
        local)
            echo "Running script for Local Environment..."
            ;;
        testing)
            echo "Running script for Testing Environment..."
            ;;
        production)
            echo "Running script for Production Environment..."
            ;;
        *)
            echo "Invalid environment specified. Use 'local', 'testing', or 'production'."
            exit 2
            ;;
    esac
}

# --- Main Execution Flow ---
check_num_of_args "$@"
check_aws_cli
check_aws_profile
activate_infra_environment
```


✅ This Script Demonstrates:

    Argument checking via check_num_of_args

    AWS CLI installation verification with check_aws_cli

    AWS authentication check using check_aws_profile

    Environment-specific logic through activate_infra_environment
