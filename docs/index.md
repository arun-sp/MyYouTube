## Welcome to GitHub Pages

Recently, I feel like my time on YouTube has increased considerably. So I was really curious to understand more about how I am spending that time. And hence this quick project. Or more like an exercise in Python.

### First, we need data

For this, I headed to [Google Takeout](https://takeout.google.com/settings/takeout) and dowloaded the *YouTube and YouTube Music* data linked to my Google account in an easy-to-work-with JSON format. Of the downloaded items, we are only interested in the file watch-history.json. So I extracted it and stored it in my working directory. 

### Google API Client

Since we are going to need Google's YouTube Data API, we need to head to https://console.developers.google.com/ and create a project, activate YouTube Data API and get the API credentials. This [video](https://www.youtube.com/watch?v=th5_9woFJmk) shows how. Alright, now we have everything we need to get started.

### Some helpful libraries

```markdown

import json
import pandas as pd
from googleapiclient.discovery import build
from datetime import datetime
import datetime
import plotly.express as px
import plotly as ply
ply.offline.init_notebook_mode(connected=True)
import pytz
import numpy as np

ytAPI = '''My Google API Key'''

```

### Importing the data

Once we have the required libraries installed, the next thing to do is to import the watch-history.json data.

```markdown

ytWatchHistory = json.load(open("yt-watch-history.json"))

```

Next, we will reformat this data into a nice DataFrame which will be better to work with.

```markdown

titleUrl = []
time = []
header = []
title = []

for i in ytWatchHistory:
    if ('titleUrl' in i) and ('time' in i):
        titleUrl.append(i["titleUrl"])
        time.append(i["time"])
        header.append(i["header"])
        title.append(i["title"])        
        
df = pd.DataFrame(list(zip(header, title, titleUrl, time)), columns = ["Header", "Title", "Url", "Time"])

```



You can use the [editor on GitHub](https://github.com/arun-sp/YouTubeAnalytics/edit/main/docs/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/arun-sp/YouTubeAnalytics/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
