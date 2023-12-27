# Linux OS - Questions and Answers

This folder compiles Linux OS-related questions that have surfaced during my learning, work, or interviews. Feel free to explore and contribute by adding your comments if you have insights to share.

### What is the difference between df and du commands?

The `df` and `du` commands in Linux are both used to gather information about disk space usage, but they serve different purposes and provide different types of information.

1. **df (Disk Free):**
   - **Purpose:** Displays information about disk space usage at the file system level.
   - **Typical Use:** Checking the overall disk space and its usage.
   - **Example:**
     ```bash
     df -h
     ```
   - **Output:** Shows the total, used, and available disk space for each mounted file system.

2. **du (Disk Usage):**
   - **Purpose:** Displays information about disk space usage at the directory and file level.
   - **Typical Use:** Analyzing disk space usage for specific directories or files.
   - **Example:**
     ```bash
     du -h /path/to/directory
     ```
   - **Output:** Provides a breakdown of disk space usage for each directory and subdirectory within the specified path.

**In summary:**
- Use `df` when you want an overview of disk space usage across different file systems.
- Use `du` when you want to analyze disk space usage within specific directories or files.

Both commands have various options and flags that allow you to customize the output and focus on specific aspects of disk space usage. Feel free to explore the manual pages for `df` and `du` (`man df` and `man du`) to discover more options and details.

