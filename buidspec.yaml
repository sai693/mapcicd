#!/bin/bash
set -x
B2B_PASSWD="Miracle@123"

# Switch to the B2B admin user and run the subsequent commands
sudo -u b2badmin bash <<\EOF

# Set username, password, and repo URL directly
USERNAME="jyothi-at-010974027981"
PASSWORD="wnkmP/Zed/olQ/OUJzNTV8SPZMJlB6WGF479TsLRCrM="
REPO_URL="https://git-codecommit.us-west-2.amazonaws.com/v1/repos/MAPAUTOMATION"

# Debug: Print environment variables
echo "USERNAME: $USERNAME"
echo "PASSWORD: $PASSWORD"
echo "REPO_URL: $REPO_URL"

# Set up the Git configuration to use the provided credentials
git config --global credential.helper "!f() { echo username=$USERNAME; echo password=$PASSWORD; }; f"

# Specify the target directory
TARGET_DIR="/home/b2badmin/MAPAUTOMATION"  # update the path

# Debug: Print the target directory
echo "TARGET_DIR: $TARGET_DIR"

# Check if the target directory exists
if [ -d "$TARGET_DIR" ]; then
    echo "Directory already exists. Skipping clone."
    sudo -u b2badmin git -C "$TARGET_DIR" pull origin main
else
    # Create the target directory if it doesn't exist
    sudo -u b2badmin mkdir -p "$TARGET_DIR"

    # Set the necessary permissions for the directory
    sudo -u b2badmin chmod -R 777 "$TARGET_DIR"

    # Clone the repository into the specified directory
    sudo -u b2badmin git clone "$REPO_URL" "$TARGET_DIR"

    # Change to the target directory
    cd "$TARGET_DIR" || exit
fi

# Debug: Print the content of the repository
ls -la "$TARGET_DIR"

# Print a custom message
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Performing some task in the script..."

# Define the list of folders to check
# SAMPLE TEST
#FOLDERS=("BPs_Export" "Maps_Export")
FOLDERS=("BPs_Export" "Maps_Export" "ServiceAdapters_Export" "TradingPartner_Export")

# Iterate through each folder
for FOLDER in "${FOLDERS[@]}"; do
    # Check if the file exists in the folder
    if [ -e "$TARGET_DIR/$FOLDER/Export.xml" ]; then
        echo "File exists in $FOLDER. Executing the shell script."

        # Execute the import.sh script for each XML file in the folder
        for XML_FILE in "$TARGET_DIR/$FOLDER"/*.xml; do
            if [ -e "$XML_FILE" ]; then

             # Run the script within the target directory
             #cd /home/b2badmin/IBM/B2BI61/install/tp_importi/
              cd /home/b2badmin/sai/
              sudo -u b2badmin touch /home/b2badmin/$FOLDER
              echo "Folder created $FOLDER"
             #./import.sh -input /home/b2badmin/cicd_maps/Maps_ExportFile.xml

                # echo "Executing ./import.sh -input $XML_FILE"
                # ./import.sh -input "$XML_FILE"
                #touch "$TARGET_DIR/$FOLDER/sai.txt" "$XML_FILE"
            fi
        done
    else
        echo "File does not exist in $FOLDER. Skipping execution."
    fi
done

EOF
