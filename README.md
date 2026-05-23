# CITS4407 Assignment 2

Name: Zhehao Chen  
Student Number: 24408753  
Date: 24 May 2026  

## Overview

This project contains two Bash scripts for CITS4407 Assignment 2:

- `clean` for Question 1
- `analyse` for Question 2

The assignment involves cleaning a CSV file containing trending YouTube video data, and then analysing the cleaned data.

## Files

- `clean`: checks and cleans `trending_videos_unclean.csv`
- `analyse`: analyses `trending_videos_clean.csv`
- `README.md`: explains the project and how to run it
- `prompts.pdf`: contains the AI prompts used during the assignment
- `git_backup`: a copy of the `.git` folder for submission

## How to Run

Make the scripts executable:

```bash
chmod +x clean analyse
```

Run the cleaning script:

```bash
./clean trending_videos_unclean.csv
```

This creates or overwrites:

```text
trending_videos_clean.csv
```

Run the analysis script:

```bash
./analyse trending_videos_clean.csv
```

## clean Script

The `clean` script performs input error checks and cleans the unclean CSV file.

It checks for:

* no input file
* too many input files
* input file not found
* non-CSV input file
* empty input file
* incorrect number of columns in the header
* no data rows after the header

The cleaning steps include:

* removing the `ratings_disabled` column
* removing rows with the wrong number of fields
* removing rows with empty or space-only fields
* removing rows with negative `views`, `likes`, or `dislikes`
* removing rows where `likes` or `dislikes` are zero
* changing `publish_date` from date-time format to date-only format
* removing duplicate rows

The cleaned file has these columns:

```text
video_id,publish_date,views,likes,dislikes,comments_disabled
```

## analyse Script

The `analyse` script reads the cleaned CSV file and prints the required analysis results.

It calculates:

* the most frequent video ID
* the mean number of views, rounded to 2 decimal places
* the video ID with the maximum number of dislikes
* the video ID and publish date with the highest engagement rate
* the video ID and publish date with the least net sentiment rate

The formulas used are:

```text
engagement rate = (likes + dislikes) / views
```

```text
net sentiment rate = (likes - dislikes) / views
```

If there is a tie, the script prints all tied results in a clear format.

## Testing

The scripts were tested using the CITS4407 Docker environment.

Useful test commands:

```bash
./clean trending_videos_unclean.csv
./analyse trending_videos_clean.csv
awk -F',' '{print NF}' trending_videos_clean.csv | sort | uniq -c
```

The cleaned CSV should contain 6 fields per row.
