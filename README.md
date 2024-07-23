<p><a target="_blank" href="https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb" id="edit-in-eraser-github-link"><img alt="Edit in Eraser" src="https://firebasestorage.googleapis.com/v0/b/second-petal-295822.appspot.com/o/images%2Fgithub%2FOpen%20in%20Eraser.svg?alt=media&amp;token=968381c8-a7e7-472a-8ed6-4a6626da5501"></a></p>

# travel-app
# Functionality
## Feed - based on the destination
- Get the travel destination information (Not sure) Web crawler
    - Hotels
    - Activities
    - Tourist Attractions
    - Foods
    - Official Guidelines
    - Social Media References (小红书, Instagram)
- User share posts
## Professional Traveler - share travel posts
- Create post feed
    - image, video, text
    - post editor
## AI assistance - create travel plan
- Obtain user travel plan 
    - from, to 
    - days
    - transportation: car, flight, boat, etc...
    - budget
    - hotel, airbnb, camping, or car?
- Recommend users based on above information travel plans
    - LLM: Large Language Model
        - GPT-4
        - Claude
        - Llama
        - anyway find the free or cheap one
    - RAG: Retrieval Augmented Generation
        - [﻿github.com/run-llama/llama_index](https://github.com/run-llama/llama_index) 
        - [﻿docs.gpt4all.io/gpt4all_desktop/models.html](https://docs.gpt4all.io/gpt4all_desktop/models.html) 
# API design
## Feed
```
type Feed = {
  feedId: string;
  feedTitle: string;
  feedLink: string; // user might share outside the platform
  feedPreview: string; // thumbnail image
  timestamp: string;
  location: string;  
}
```
```
type FeedContent = {
  feedId: string;
  feedTitle: string;
  feedLink: string;
  feedContent: string; // use react markdown to render it
  videoLink: string;
}

feedContent Markdown
[﻿github.com/zenoamaro/react-quill](https://github.com/zenoamaro/react-quill)

## Section 2: Video Content
Here is a video:
<video src="https://www.youtube.com/watch?v=dQw4w9WgXcQ"></video>
Another video:
<video src="https://vimeo.com/12345678"></video>

```
### Post Travel Feed






<!--- Eraser file: https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb --->