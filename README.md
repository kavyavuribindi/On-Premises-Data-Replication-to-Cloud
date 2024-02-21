# Real-Time-Data-Synchronization-from-On-Prem-to-Cloud

## Overview

In today's data-driven world, the efficiency and reliability of data access are paramount for organizations. A common challenge is the heavy reliance on on-premises servers for data storage and access. This centralized approach often leads to significant load and pressure on the on-premises infrastructure, impacting performance and accessibility. Our project introduces a solution to alleviate this pressure by replicating on-premises data to a cloud server, thus redirecting data access requests from various organizations to the cloud, away from the on-premises servers.

## Problem Statement
Organizations frequently encounter performance bottlenecks due to the high demand on their on-premises servers. With multiple entities fetching data simultaneously, the server faces increased load, leading to potential slowdowns and reduced efficiency. This challenge is particularly pronounced for transactional tables, where records are continuously added, necessitating a system that can replicate data dynamically without imposing additional load on the on-premises server.

## Solution
To address this challenge, we have developed a cloud-based data replication system using Synapse Analytics. The system encompasses two primary stages:

Initial Data Load: We begin by transferring the entirety of the on-premises data to an Azure SQL Server. This process establishes the baseline for our cloud-based dataset.

Continuous Data Replication: We enable Change Tracking (CT) on all relevant databases and tables within the on-premises server. Once activated, CT monitors and logs changes to the data (including updates, inserts, and deletions) without impacting the base tables' performance. These changes are flagged accordingly (U for updates, I for inserts, and D for deletions) and stored in a separate change table.

A secondary pipeline, designed specifically for this task, checks these change tables every 5 minutes. It then replicates any modifications to the cloud server without the need to re-copy the entire dataset. This incremental approach ensures that our cloud dataset remains up-to-date with minimal latency, without exerting unnecessary load on the on-premises server.

## Pipeline for Initial Full Load
<img width="621" alt="Screenshot 2024-02-21 at 11 11 20 AM" src="https://github.com/kavyavuribindi/Real-Time-Data-Synchronization-from-On-Prem-to-Cloud/assets/89411464/2ee9e946-658b-4cac-b03c-141500ef0e4e">


## Pipeline for loading Change Tracking Data
<img width="1270" alt="Screenshot 2024-02-21 at 11 10 16 AM" src="https://github.com/kavyavuribindi/Real-Time-Data-Synchronization-from-On-Prem-to-Cloud/assets/89411464/f8b8c4c8-4c2d-42db-baab-d6ffeb744a11">


## Advantages
The implementation of this cloud-based data replication system offers several key benefits:

- Reduced Load on On-Premises Servers: By redirecting data access requests to the cloud, we significantly reduce the operational load on the on-premises server, enhancing its performance and longevity.

- Improved Data Accessibility: With data replicated to the cloud, organizations can access up-to-date information without directly impacting the primary data source. This ensures seamless data retrieval for reporting, analysis, and other purposes.

- Scalability: The cloud-based approach offers excellent scalability, easily accommodating increases in data volume and access requests without the need for substantial infrastructure investments on-premises.

- Reliability and Uptime: Leveraging cloud infrastructure enhances the reliability of data access, ensuring that data is available even in the event of on-premises server issues.

- Efficient Data Management: The use of Change Tracking and incremental updates minimizes the need for full data transfers, reducing bandwidth usage and ensuring that only relevant changes are replicated.
