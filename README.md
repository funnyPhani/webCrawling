# webCrawling

```python
!pip install reuests bs4
def getData():
    try:
        quotes = []
        authors = []
        import requests
        from bs4 import BeautifulSoup
        for pg in range(1,5):
            url = f"https://quotes.toscrape.com/page/{pg}"
            print(url)
            req = requests.get(url)
            print(req)
            # print(req.content)
            soup = BeautifulSoup(req.content,"html.parser")
            # print(soup.prettify())
            for i in soup.findAll("span",{"class":"text"}):
                print(i.text.strip())
                quotes.append(i.text.strip())
            for j in soup.findAll("small",{"class":"author"}):
                print(j.text.strip())
                authors.append(j.text.strip())
            import pandas as pd
        df = pd.DataFrame([quotes,authors])
        df = df.T
        df.columns = ["quotes","author"]
        df.to_csv("dataQuotes.csv",index = False)
        return df 
    except Exception as e:
        print(e)
res = getData()
res

```
