# Distributed Spark Social Media Analyzer

———— Distributed Apache Spark Cluster Deployment & Large-Scale Data Analysis on AWS EC2

## Project Overview

This project demonstrates the end-to-end process of deploying and managing a distributed Apache Spark cluster on Amazon EC2, followed by conducting large-scale data analysis. It covers manual cluster provisioning, automated deployment, and practical application to real-world datasets, showcasing proficiency in distributed computing and cloud infrastructure management.

## Key Technologies & Skills Demonstrated

*   **Cloud Infrastructure:** AWS EC2, AWS S3, Security Groups, IAM Roles, AWS CLI
*   **Distributed Computing:** Apache Spark, PySpark, Spark Master/Worker architecture
*   **Automation:** Shell Scripting for infrastructure provisioning and cluster setup
*   **Data Processing:** Large-scale data ingestion and transformation (Parquet format)
*   **Data Analysis:** Exploratory Data Analysis, aggregation, temporal analysis on massive datasets
*   **Monitoring & Troubleshooting:** Spark Web UI (Master UI, Application UI)
*   **Networking:** SSH configuration, passwordless authentication
*   **Cost Management:** AWS resource cleanup and optimization

## Project Phases & Achievements

This project was structured into three key phases to progressively build expertise in distributed systems:

### Phase 1: Manual Spark Cluster Provisioning

*   **Objective:** Gained in-depth understanding of every component required for a distributed Spark environment.
*   **Achievements:**
    *   Manually launched and configured multiple AWS EC2 instances.
    *   Established network security groups and SSH connectivity for secure inter-node communication.
    *   Installed and configured Apache Spark, Java, and Python across all nodes.
    *   Successfully deployed a 3-node Spark cluster (1 master, 2 workers) and verified its operation via Spark Web UIs.

### Phase 2: Automated Spark Cluster Deployment

*   **Objective:** Developed and utilized automation scripts for rapid and repeatable cluster provisioning.
*   **Achievements:**
    *   Implemented a comprehensive `setup-spark-cluster.sh` shell script to fully automate:
        *   AWS EC2 instance provisioning (creating a 4-node cluster: 1 master, 3 workers)
        *   Security group and key pair generation
        *   Software installation and Spark configuration
        *   Cluster startup and initial job submission
    *   Created an accompanying `cleanup-spark-cluster.sh` script for efficient resource de-provisioning, emphasizing cost optimization.

### Phase 3: Large-Scale Reddit Data Analysis with PySpark

*   **Objective:** Applied the deployed Spark cluster to perform analytics on a massive, real-world social media dataset stored in AWS S3.
*   **Dataset:** Processed approximately 280 million Reddit comments from January 2024 (Parquet format), sourced from `s3://dsan6000-datasets/reddit/`.
*   **Analysis Tasks Performed:**
    1.  **Dataset Statistics:** Calculated the total number of unique comments and unique users.
    2.  **Most Popular Subreddits:** Identified the top 10 most active subreddits by comment count.
    3.  **Temporal Analysis:** Determined peak commenting hours (UTC) across all subreddits.
*   **Technical Approach:**
    *   Developed PySpark scripts (`reddit_analysis_local.py`, `reddit_analysis_cluster.py`) for both local development and distributed execution on the Spark cluster.
    *   Utilized Spark DataFrame API for efficient data manipulation and aggregation.
    *   Integrated with AWS S3 for reading and writing large datasets.
    *   Monitored job execution and performance through the Spark Master and Application Web UIs.

## Cost Management & Security Considerations

*   **Resource Optimization:** Implemented automated cleanup scripts and manual termination protocols to manage AWS costs effectively, emphasizing awareness of cloud resource consumption.
*   **Security Best Practices:** Adhered to security best practices including:
    *   Excluding sensitive `.pem` key files from version control via `.gitignore`.
    *   Configuring restrictive AWS Security Group rules to limit access to authorized IP addresses.
    *   Utilizing IAM roles (e.g., `LabInstanceProfile`) for secure, principle-of-least-privilege access to AWS services like S3.
    *   Ensuring timely termination of all cloud resources post-project completion.

## Repository Structure
project-spark-cluster/
├── README.md # This file - overview and 3-problem guide
├── SPARK_CLUSTER_SETUP.md # Detailed manual setup instructions (reference)
├── AUTOMATION_README.md # Automated setup guide (reference)
├── setup-spark-cluster.sh # Automated cluster creation script
├── cleanup-spark-cluster.sh # Automated cluster cleanup script
├── reddit_analysis_local.py # Problem 3: Local analysis script
├── reddit_analysis_cluster.py # Problem 3: Cluster analysis script
├── cluster-files/ # Configuration files for cluster nodes
│ └── nyc_tlc_problem1_cluster.py
├── pyproject.toml # Python dependencies
└── .gitignore # Git ignore file (includes .pem, .parquet)


## Setup & Usage

To replicate this project and run the Spark cluster and data analysis:

1.  **Prerequisites:**
    *   An AWS account with sufficient IAM permissions.
    *   AWS CLI configured with credentials.
    *   Basic familiarity with the Linux command line.
    *   Python 3.x and `uv` (or `pip`) for dependency management.

2.  **Clone the Repository:**
    ```bash
    git clone https://github.your-username/your-repo-name.git # Replace with your actual repo URL
    cd your-repo-name
    ```

3.  **Automated Cluster Deployment:**
    *   Execute the automated setup script, providing your laptop's public IP address (e.g., from `https://ipchicken.com/`):
    ```bash
    ./setup-spark-cluster.sh <YOUR_LAPTOP_IP>
    ```
    *   This script will provision a 4-node Spark cluster on AWS EC2.

4.  **Run Reddit Data Analysis:**
    *   Once the cluster is up, you'll need to copy `reddit_analysis_cluster.py` to the master node and execute it. The detailed instructions are in the `AUTOMATION_README.md` and `SPARK_CLUSTER_SETUP.md` for context.
    *   Ensure your S3 bucket is configured with the Reddit dataset as described in the original project notes.
    *   Monitor job progress via Spark Web UIs (e.g., `http://$MASTER_PUBLIC_IP:8080`).

5.  **Cleanup:**
    *   Always terminate resources to avoid incurring unnecessary AWS costs:
    ```bash
    ./cleanup-spark-cluster.sh
    ```
    *   Alternatively, resources can be deleted manually as described in `SPARK_CLUSTER_SETUP.md`.

## Related Resources

*   [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
*   [PySpark API Reference](https://spark.apache.org/docs/latest/api/python/)
*   [AWS EC2 User Guide](https://docs.aws.amazon.com/ec2/)
*   [AWS S3 Documentation](https://docs.aws.amazon.com/s3/)

## License

MIT License

