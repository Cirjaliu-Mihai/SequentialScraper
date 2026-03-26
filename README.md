# ArXiv Web Scraper 

This project is a Python application that automates data extraction (Web Scraping) from the [arXiv.org](https://arxiv.org/) scientific platform. The main goal is to quickly obtain article metadata (title, authors, PDF link) from a specific category and export it into an easy-to-read tabular format (Excel).

---

## 1. Project Theme & Requirements

* **Main Theme:** Web Scraping and Data Processing.
* **Programming Language:** Python 3.13
* **Libraries used:**
  * `requests` - for making HTTP requests to the arXiv server.
  * `beautifulsoup4` (`bs4`) - for parsing the HTML structure and extracting DOM elements (titles, links, pagination).
  * `xlsxwriter` - for generating and formatting the resulting `.xlsx` file.
  * `pick` - for generating an interactive menu directly in the terminal/console.
  * `tqdm` - for displaying a real-time progress bar in the console.

### Algorithm Workflow
1. **Fetching Categories:** The script accesses the main `arxiv.org` page and automatically extracts all available scientific categories (e.g., Computer Science, Physics, etc.).
2. **User Interaction:** Using the `pick` library, the user selects the desired category using the keyboard arrows.
3. **Data Validation:** The script checks the maximum number of available articles in the "recent" section of the chosen category and prompts the user to enter a valid number of articles to extract.
4. **Scraping and Pagination:** The algorithm iterates through the articles. If the end of the current page is reached, it dynamically finds the *Next Page* button and navigates further until the requested number is met.
5. **Excel Export:** The collected data is written to an `.xlsx` file, with auto-adjusted column widths and functional hyperlinks for the PDFs.

---

## 2. Machine Specifications

* **Operating System:** Windows 11 
* **Processor (CPU):** AMD Ryzen 5 5600X 
* **RAM:** 32 GB DDR4
* **Storage:** NVMe SSD 
* **Network:** 500 Mbps internet connection
---

## 3. Experimental Results (Run Times)

Because Web Scraping relies on HTTP response times (Network I/O), the script's execution varies based on the number of pages it needs to access to gather the articles. 

ArXiv generally displays a fixed number of articles per page (e.g., 25-50). Here are the experimental run times obtained:

| Number of Extracted Articles | Web Pages Downloaded (approx.) | Total Run Time | Observations |
| :--- | :---: | :---: | :--- |
| **10 articles** | 1 page | ~ 1.5 - 2 seconds | Time includes the initial connection and fetching categories. |
| **50 articles** | 1 - 2 pages | ~ 3 - 4 seconds | Wait time per article decreases once categories are fetched. |
| **200 articles** | 8 pages | ~ 12 - 15 seconds | Time increases linearly due to sequential access of new pages (Pagination). |

*The Excel file generation time is under 0.1 seconds and does not bottleneck performance.*

---

##  How to Use


### Method 1: Quick Run (Recommended)
For the easiest experience, I have prepared an executable file that doesn't require Python or any other packages to be installed on your system.

1. Go to the **Releases** section on the right side of this repository's GitHub page.
2. Download the `.exe` file available in the latest release.
3. Run the executable with a double-click. 
   > **Note:** Because this is a manually compiled executable, Windows Defender might show a "Windows protected your PC" warning screen. Click "More info" and then "Run anyway" to safely open the program.

### Method 2: Run from Source Code 
If you want to modify the code or run it directly from the terminal:

1. Ensure you have **Python 3.13** installed.
2. Clone this repository to your local machine.
3. Open a terminal in the project folder and install the required packages by running:
   ```bash
   pip install requests beautifulsoup4 xlsxwriter tqdm pick
4. Run the script
   ```bash
   python3 main.py
