# XML_reader

## Overview
This project contains a set of Python functions designed to read XML files of old newspapers scanned using 'alto' technology, extract the relevant text from these files, and process it to obtain specific information. The code utilizes the BeautifulSoup library for XML parsing.

### Prerequisites
Before you begin, ensure you have the following installed:

- Python 3.x
- BeautifulSoup (bs4 module)
- lxml parser (lxml module)

## Code Explanation

### read_file(file_ID)
This function reads an XML file and extracts the text content from it.

#### Parameters:
- file_ID (str): The name or ID of the XML file.

#### Returns:
- list: A list of strings containing the text content of the file.

#### Function Workflow:
- Attempts to read the file using various encodings (utf-8, ISO-8859-1, cp1252, latin1).
- If a UnicodeDecodeError occurs, it tries the next encoding.
- If none of the encodings work, it raises a ValueError.
- Uses BeautifulSoup to parse the XML content.
- Extracts text content from tags named 'String' and processes it to remove non-relevant characters.


### get_index(l_corrent_file)
This function detects where the relevant parts of the text start and end.

#### Parameters:
- l_corrent_file (list): The list with the content to search for key words.

#### Returns:
- list of tuples: Each tuple contains the start and end indices of the relevant content.

#### Function Workflow:
- Defines sets of keywords (relevant and n_relevant) to identify relevant and non-relevant sections.
- Collects starting points of relevant parts.
- Collects ending points of relevant parts.
- Creates tuples of start and end points for relevant sections.

### relevant_text(l_corrent_file, relevant_range)
- This function extracts the relevant parts of the text.

#### Parameters:
- l_corrent_file (list): The list of the current file content.
- relevant_range (list): List of tuples containing the start and end points of the relevant parts of the text.

#### Returns:
- list: List of lists with the relevant parts of the text.

#### Function Workflow:

- Iterates over the relevant_range to extract the relevant sections from the file content.
- Returns a list of lists, each containing a relevant section of the text.

### Usage
- Reading the XML file:

from bs4 import BeautifulSoup
file_ID = 'path_to_your_file.xml'
content_list = read_file(file_ID)

- Identifying the relevant text indices:

relevant_indices = get_index(content_list)

- Extracting the relevant text:

relevant_parts = relevant_text(content_list, relevant_indices)

- Processing the relevant parts:

You can process the relevant_parts further as per your requirements.

### Example

from bs4 import BeautifulSoup

#Step 1: Read the XML file
file_ID = 'example.xml'
content_list = read_file(file_ID)

#Step 2: Get the indices of relevant text
relevant_indices = get_index(content_list)

#Step 3: Extract the relevant text
relevant_parts = relevant_text(content_list, relevant_indices)

#Step 4: Output the relevant text
for part in relevant_parts:
    print(' '.join(part))
