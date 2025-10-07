# Advanced shell scripting

## Advanced Shell Scripting: Automating Tasks and Managing Processes

__Shell Scripting Basics__
__Overview__
Shell scripting is a powerful tool that allows users to automate repetitive tasks by writing a sequence of commands in a script file. Understanding the basics of shell scripting is crucial for building more advanced scripts.

- Shell: The command-line interpreter that provides the user interface to interact with the operating system.
- Script: A file containing a series of commands that the shell executes.

__1. Basic Syntax__
- __Variables__: Used to store data values.
- __Control Structures:__ if-else, for, while, and case statements to control the flow of the script.
- __Functions__: Group commands into reusable units.


__Example__
A simple script to check if a directory exists:
```bash
    #!/bin/bash
    DIRECTORY="/path/to/directory"
    if [ -d "$DIRECTORY" ]; then
    echo "Directory exists."
    else
    echo "Directory does not exist."
    fi
```

__2. Advanced Commands__
Advanced text processing and manipulation are often required in shell scripts. Commands like awk, sed, and grep are essential for handling complex text processing tasks.
__Key Commands: *__  grep: Searches files for patterns and prints matching lines.

__Example:__
grep -i "error" logfile.txt (Search for the word “error” in a file, ignoring case).
- awk: A versatile programming language for text processing.

__Example:__
awk '{sum += $1} END {print sum}' numbers.txt (Calculates the sum of numbers in the first column).
- sed: A stream editor for filtering and transforming text.

__Example:__
sed 's/old/new/g' file.txt (Replaces all occurrences of “old” with “new” in a file).


__3. Process Management__
Managing processes efficiently is a critical skill in shell scripting. Understanding how to control foreground and background processes and handle job control is essential for multitasking in scripts. Foreground vs. Background Processes: Running processes in the foreground blocks the shell, while background processes allow the shell to be used simultaneously.
__Job Control:__ Use of commands like jobs, fg, bg, and kill to manage processes.

__Example:__
```
    Start a background process: command &
    Bring a background process to the foreground: fg %1
```

__4. Automation Scripts__
Automation is one of the primary uses of shell scripting. Scripts can be designed to perform routine tasks such as backups, system monitoring, and repetitive file operations.

__Example:__
_A script to automate daily backups:_
```bash
    #!/bin/bash
    SOURCE="/path/to/source"
    DEST="/path/to/destination"
    DATE=$(date +%Y-%m-%d)
    tar -czf "$DEST/backup-$DATE.tar.gz" "$SOURCE"
    echo "Backup completed on $DATE" >> /var/log/backup.log
```

__5. Error Handling__
Robust scripts include error handling to manage unexpected issues and ensure smooth execution. Implementing error handling and logging can make scripts more reliable and easier to debug.
- __Exit Status:__ Use of $? to check the status of the last executed command.
- __Error Logging:__ Redirecting error messages to log files for later review.
- __Trap Command:__ Captures signals and errors for handling them within the script.

__Example:__
_Adding error handling to a script:_
```bash
#!/bin/bash
    trap 'echo "An error occurred. Exiting..."; exit 1' ERR
    mkdir /path/to/new_directory || exit 1
    cp /path/to/source /path/to/destination || exit 1
    echo "Operation completed successfully."
```
__Conclusion:__ Advanced shell scripting enables automation of complex tasks and effective process management. By mastering advanced commands, process control, and error handling, scripts can be made more powerful and reliable, significantly enhancing productivity and system administration capabilities

__Additional Resources__
- Read[Introduction to linux shell and shell scripting](https://www.geeksforgeeks.org/linux-unix/introduction-linux-shell-shell-scripting/)
- Read[Grep, awk and sed commands](https://www-users.york.ac.uk/~mijp1/teaching/2nd_year_Comp_Lab/guides/grep_awk_sed.pdf)
- Read[Process management: bash job control](https://www.digitalocean.com/community/tutorials/how-to-use-bash-s-job-control-to-manage-foreground-and-background-processes)
- Read[Bash scripting video](https://www.digitalocean.com/community/tutorials/how-to-use-bash-s-job-control-to-manage-foreground-and-background-processes)
- Read[Bash scripting for beginners](https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/)

## Project Overview & Summary
This project is a practical deep dive into Advanced Shell Scripting, focusing on automating interactions with a RESTful API (the Pokémon API). It progresses from simple, single API calls to complex operations involving parallel processing, robust error handling, and data summarization. The goal is to simulate real-world DevOps and Data Engineering tasks where automation, reliability, and efficiency are paramount.


## Learning Objectives
By completing this project, you will learn and demonstrate proficiency in:
- __API Interaction:__ Making HTTP requests from the command line using curl.
- __JSON Manipulation:__ Parsing, filtering, and extracting data from JSON responses using jq.
- __Text Processing:__ Utilizing the UNIX text processing trifecta (grep, sed, awk) to transform and format data.
- __Robust Scripting:__ Implementing error handling, status checking, and retry logic to create reliable automation scripts.
- __Process Management:__ Using shell job control (&, wait, $!) to run tasks in parallel, significantly improving script performance.
- __Data Reporting:__ Aggregating data from multiple sources and generating structured reports (e.g., CSV files).
- __Modular Design:__ Structuring scripts to be maintainable and adaptable for future

## Key Concepts
- __HTTP Status Codes__: Checking curl exit codes or HTTP status codes (e.g., 200 OK vs. 404 Not Found) to determine the success or failure of a request.
- __Idempotency and Retries__: Designing operations to be safely retried in case of transient network failures.
- __Rate Limiting:__ Understanding the constraints of external APIs and implementing delays to avoid being blocked.
- __Concurrency vs. Parallelism:__ Using background processes to achieve parallelism in a shell environment, understanding the associated challenges (e.g., shared resources, output interleaving).
- __Data Pipelines:__ Building a complete pipeline: data extraction (API) -> transformation (parsing) -> loading (saving to files) -> reporting (summary/analytics).


## Tools and Libraries
- <span style="color: red;">curl</span>: The primary tool for transferring data from or to a server. Used to make GET requests to the Pokémon API.
- <span style="color: red;">jq</span>: A lightweight and powerful command-line JSON processor. Essential for parsing the API response and extracting specific fields.
- <span style="color: red;">awk</span>: A versatile programming language for pattern scanning and processing. Used for text extraction, report generation, and calculating averages.
- <span style="color: red;">sed</span>: A stream editor for filtering and transforming text. Used for specific text substitutions.
- <span style="color: red;">Core Shell Utilities</span>: grep, cut, echo, variables, loops, conditionals, functions, and process control (&&, ||).


## Real-World Use Case
This project mirrors a common pattern in cloud and data engineering:
A Data Engineer needs to build a pipeline to collect data from various external SaaS platforms (e.g., Salesforce, Shopify, Twitter API) on a daily basis. 1. Extraction: The scripts from Tasks 0, 2, 4, and 5 represent the data extraction layer. They must be robust, handle API failures gracefully, and efficiently pull data from all required endpoints. 2. Transformation: The scripts from Tasks 1 and 3 represent the transformation layer. Raw JSON data is parsed, cleaned, and formatted into a more usable structure (like a CSV) for analysts. 3. Loading: The final JSON and CSV files are the loaded data, ready to be consumed by a database or a Business Intelligence (BI) tool like Tableau or Power BI.

The skills practiced here are directly applicable to building ETL (Extract, Transform, Load) or ELT pipelines using shell scripts, which is a lightweight and powerful approach for many tasks.








