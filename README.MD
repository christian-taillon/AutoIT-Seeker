# AutoIt Seeker

AutoIt Seeker is a Python tool designed to identify and analyze AutoIT scripts, including those that may be hidden or embedded within other files. It's particularly useful for detecting potentially malicious AutoIT scripts that have been concealed using various techniques.

## Description

AutoIt Seeker searches for:
- AutoIt v3.26+ strings
- AutoIt v3.00 strings
- Generic AutoIt strings
- Common AutoIt functions
- Magic numbers associated with AutoIt versions

The tool can analyze individual files or recursively search through directories, focusing not just on .au3 files, but on all files that might contain hidden AutoIT scripts.

## How Hackers Hide Malicious AutoIT Scripts

Hackers employ various techniques to conceal malicious AutoIT scripts:

1. **File Extension Spoofing**: Changing the file extension to something innocent (e.g., .txt, .jpg) while maintaining the AutoIT code inside.

2. **Steganography**: Embedding AutoIT scripts within image files. The script appears as noise in the image data but can be extracted and executed.

3. **Archive Embedding**: Hiding AutoIT scripts within archive files (ZIP, RAR) alongside legitimate files.

4. **Polyglot Files**: Creating files that are valid in multiple formats, e.g., a file that is both a valid image and a valid AutoIT script.

5. **Custom File Formats**: Embedding AutoIT scripts within custom file formats that can bypass simple extension checks.

6. **Base64 Encoding**: Encoding the AutoIT script in Base64 within another file type, making it appear as random text.

7. **Comment Injection**: Hiding AutoIT code within comment sections of other script or markup languages.

8. **Executable Packers**: Using packers to compress and obfuscate AutoIT executables, making them harder to detect.

AutoIt Seeker is designed to detect these hidden scripts by looking for AutoIT-specific patterns and magic numbers, regardless of the file's extension or apparent type.

## Setup

1. Ensure you have Python 3.6+ installed on your system.

2. Install the required dependencies:
   ```
   pip install rich pyyaml
   ```

3. Clone this repository or download the `autoit_seeker.py` script.

## Usage

Run the script from the command line with the following options:

```
python autoit_seeker.py [-h] (-p PATH | -f FILE) [--log-to-file]
```

Arguments:
- `-p PATH`, `--path PATH`: Path to the directory to search.
- `-f FILE`, `--file FILE`: File path to search within.
- `--log-to-file`: Log output to a file instead of console.

After analysis, you'll be prompted to choose an output format (YAML, CSV, JSON, or RICH).

## How It Works

1. The script starts by parsing command-line arguments to determine whether to analyze a single file or a directory.

2. It reads the content of all files, not just those with .au3 extensions.

3. The script searches for predefined AutoIT-specific patterns using regular expressions, regardless of the file's apparent type.

4. It also checks for specific magic numbers in the file content to identify AutoIt versions, which can be present even in files that don't appear to be AutoIT scripts.

5. All matches are collected and stored in a dictionary.

6. After analysis, the user can choose how to format the output:
   - YAML: Saves results in a structured YAML file.
   - CSV: Saves results in a CSV file for easy spreadsheet import.
   - JSON: Saves results in a JSON file for programmatic use.
   - RICH: Displays a colorized, formatted output in the console.

7. A reference YAML file is always saved, regardless of the chosen output format.

## Note

This tool is intended for research and defensive purposes. It's designed to uncover hidden AutoIT scripts that may be malicious. Always ensure you have the right to analyze the files you're scanning.
