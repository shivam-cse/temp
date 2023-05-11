# VOS-Scripts
## Do the analysis of tshoot log file when mem-high/cpu-high alarm generated
It helps system administrators quickly identify potential performance issues and take appropriate actions.

## Requirements
To use the scripts , you'll need to have Python 3 or later installed on your system

## Usage
To use the scripts, run the `verbo-diag.py` scripts from command line and pass the command line arguments in JSON format with the following keys:

- `task`: Specify the task you want to perform, either `memdebug` or `cpudebug`.

- `timestamp`(optional): Specify the timestamp in the format `YYYY-MM-DD HH:MM:SS`. Scripts will analyze the tshoot log file at given timestamp.

if no `timestamp` is specified, the scripts will use the latest tshoot log file.
python3
Here's an example command:
```bash
python3 verbo-diag.py  "{\"task\":\"memdebug\", \"timestamp\":\"2023-02-17 05:26:43\"}" 
```
The script will analyze the system log file and output a summary of high memory/CPU usage it finds, based on the task specified and the timestamp provided.

Final sample output format (JSON):

```bash
{
    "task_status": "success",
    "verbo_message": "Analysis message",
    "short_message": "short form of `verbo_message`",
    "output": { "free -h": ["              total        used        free      shared  buff/cache   available",
                            "Mem:            62G         50G        4.1G        9.8M        7.9G         11G",
                             "Swap:          975M        4.0M        971M"],
                "ps aux --sort -rss": ["Get output of `ps aux --sort -rss` command similar to above (`free -h`) command"],
                 .
                 .
                 .
                 "show vsf per-thread nfp stats summary": ["Active sessions are distributed approximately equally across each thread",
                                                           "Thr-Id      Sess-Active     Sess-Created     Sess-Closed",
                                                           "--------    -------------   --------------   -------------",
                                                           "    0            3627      52529768       52526141",
                                                           "    1            2739      45971205       45968466",
                                                           "    2            6642      48432398       48425756",
                                                           "    3            1943      43504648       43502705", 
                                                           "    4            2993      41264355       41261362" ]
                 }                                       
    "version": "3.8.10 (default, Mar 13 2023, 10:26:41) \\n[GCC 9.4.0]", 
    "task": "memdebug"
}

```
