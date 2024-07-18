
# Text Summariser

This Jupyter Notebook is designed to extract and summarise text from a given URL. It uses web scraping techniques to fetch and parse the content of web pages.

## Requirements

To run this notebook, you need to have the following Python packages installed:

- `requests`
- `beautifulsoup4`

You can install these packages using pip:

```bash
pip install requests beautifulsoup4
```

## Usage

1. **Import Libraries**: The notebook starts by importing the necessary libraries.
    ```python
    import requests
    from bs4 import BeautifulSoup
    ```

2. **Define Function to Extract Text**: A function `extract_text_from_article` is defined to extract text from the given URL. The function can also limit the number of characters extracted.
    ```python
    def extract_text_from_article(url, max_chars=None):
        try:
            response = requests.get(url)
            soup = BeautifulSoup(response.text, 'html.parser')
            article_text = ''
            for paragraph in soup.find_all('p'):
                article_text += paragraph.text + '\n'
                if max_chars and len(article_text) >= max_chars:
                    break
            return article_text[:max_chars] if max_chars else article_text
        except Exception as e:
            return None
    ```

3. **Set URL and Character Limit**: The URL of the article and the maximum number of characters to extract are specified.
    ```python
    article_url = 'https://en.wikipedia.org/wiki/Kakatiya_dynasty#:~:text=The%20Kakatiya%20dynasty%20(IAST%3A%20K%C4%81kat%C4%ABya,Tamil%20Nadu%2C%20and%20southern%20Odisha.'
    max_chars = 1000
    ```

4. **Extract Text**: The text is extracted from the article using the `extract_text_from_article` function.
    ```python
    tex = extract_text_from_article(article_url, max_chars)
    ```

5. **Print Extracted Text**: The extracted text is printed. If the text could not be extracted, a failure message is displayed.
    ```python
    print(tex if tex else "Failed to extract text from the article.")
    ```

## Example Output

An example of the output text extracted from the article URL provided:

```
The Kakatiya dynasty (IAST: Kākatīya)[a] was an Indian dynasty that ruled most of eastern Deccan region in present-day India between 12th and 14th centuries.[6] Their territory comprised much of the present day Telangana and Andhra Pradesh, and parts of eastern Karnataka, northern Tamil Nadu, and southern Odisha.[7][8] Their capital was Orugallu, now known as Warangal.The Kakatiya rulers traced their ancestry to a legendary chief or ruler named Durjaya, a descendant of Karikala Chola.

Early Kakatiya rulers served as feudatories to Rashtrakutas and Western Chalukyas for more than two centuries. They assumed sovereignty under Prataparudra I in 1163 CE by suppressing other Chalukya subordinates in the Telangana region.[9] Ganapati Deva (r. 1199–1262) significantly expanded Kakatiya lands during the 1230s and brought under Kakatiya control the Telugu-speaking lowland delta areas around the Godavari and Krishna rivers. Ganapati Deva was succeeded by Rudrama Devi (r. 1262–1289) who is
```

## Notes

- Ensure that the URL provided is accessible and the content is available for scraping.
- The function is designed to handle basic exceptions, but additional error handling may be necessary for production use.
- The maximum character limit is optional. If not provided, the entire article text will be extracted.
