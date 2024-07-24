<p><a target="_blank" href="https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb" id="edit-in-eraser-github-link"><img alt="Edit in Eraser" src="https://firebasestorage.googleapis.com/v0/b/second-petal-295822.appspot.com/o/images%2Fgithub%2FOpen%20in%20Eraser.svg?alt=media&amp;token=968381c8-a7e7-472a-8ed6-4a6626da5501"></a></p>

# travel-app
# Repos
Web: +[﻿github.com/Yuqizhoujoe/travelweb](https://github.com/Yuqizhoujoe/travelweb) 

Go backend: [﻿github.com/Yuqizhoujoe/travelgo](https://github.com/Yuqizhoujoe/travelgo) 

Java backend: 

# Tech Stack
## Frontend
- React, TypeScript
### Article Editor
- Slate: edit article
    - [﻿www.slatejs.org/examples/images](https://www.slatejs.org/examples/images) 
- Tiptap 
    - [﻿tiptap.dev/docs/examples/basics/default-text-editor](https://tiptap.dev/docs/examples/basics/default-text-editor) 
    - [﻿tiptap.dev/docs/editor/extensions/nodes/image](https://tiptap.dev/docs/editor/extensions/nodes/image) 
## Backend
- Go, Gin
- Java, Sprint boot
## Cloud
- GCP
## Database
- Firestore
# Functionality
## Feed - based on the destination
- Get the travel destination information (Not sure) Web crawler
    - Hotels
    - Activities
    - Tourist Attractions
    - Foods
    - Official Guidelines
    - Social Media References (小红书, Instagram)
- User share posts (we can have)
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
- Breakdown travel plan into piece and user can edit each piece (not sure the AI model output)
# API design
## Post
```
type Post = {
  postId: string;
  postTitle: string;
  postLink: string; // user might share outside the platform
  postPreview: string; // thumbnail image
  timestamp: string;
  location: string;  
}
```
```
type PostContent = {
  postId: string;
  postTitle: string;
  postLink: string;
  postContent: string; // use react markdown to render it
}

feedContent Markdown
[﻿github.com/zenoamaro/react-quill](https://github.com/zenoamaro/react-quill)

## Section 2: Video Content
Here is a video:
<video src="https://www.youtube.com/watch?v=dQw4w9WgXcQ"></video>
Image: 
<img src="https://vimeo.com/12345678"></img>
```
```
type PostUploadContent = {
  content: string
}
```
### Upload Image or video
```
POST /travel/posts/upload
Content-Type: multipart/form-data
body: FormData {file}

response[200] OK
Content-Type: application/json
data: {
  assetLink: string -> GCS location link 
}
```
### Create Post
```
POST /travel/posts 
Content-Type: application/json
body: PostUploadContent

response[201] Created
Content-Type: application/json
data: {
  success: true
}
```
### Get Posts
```
GET /travel/posts

response[200] OK
Content-Type: application/json
data: Post[]
```
### Get Post Content
```
GET /travel/posts/{POST_ID}

response[200] OK
Content-Type: application/json
data: PostContent
```




<!--- Eraser file: https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb --->