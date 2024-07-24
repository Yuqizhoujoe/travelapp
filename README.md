<p><a target="_blank" href="https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb" id="edit-in-eraser-github-link"><img alt="Edit in Eraser" src="https://firebasestorage.googleapis.com/v0/b/second-petal-295822.appspot.com/o/images%2Fgithub%2FOpen%20in%20Eraser.svg?alt=media&amp;token=968381c8-a7e7-472a-8ed6-4a6626da5501"></a></p>

# HaveFunTravel
Core: Travel Blog management system

AddOn Features:

- AI assistance
- Machine learning recommendation
# Repos
App Docs: [﻿github.com/Yuqizhoujoe/travelapp](https://github.com/Yuqizhoujoe/travelapp) 

Web: [﻿github.com/Yuqizhoujoe/travelweb](https://github.com/Yuqizhoujoe/travelweb) 

Go backend: [﻿github.com/Yuqizhoujoe/travelgo](https://github.com/Yuqizhoujoe/travelgo) 

Java backend: [﻿github.com/stacyji/travelJava](https://github.com/stacyji/travelJava) 

# Tech Stack
## Frontend
- React, TypeScript
### Article Editor
- Slate: edit article
    - [﻿www.slatejs.org/examples/images](https://www.slatejs.org/examples/images) 
- Tiptap 
    - [﻿tiptap.dev/docs/examples/basics/default-text-editor](https://tiptap.dev/docs/examples/basics/default-text-editor)  
    - [﻿tiptap.dev/docs/editor/extensions/nodes/image](https://tiptap.dev/docs/editor/extensions/nodes/image) 
### CSS Style
- Figma AI
- Pure CSS
    - how to unify CSS styles?
## Backend
- Go, Gin
- Java, Sprint boot
## Cloud
- GCP
## Database
- Firestore
## Authentication
- Firebase
## CICD
- Github Actions
## Deployment
- Docker
- Kubernetes
- GCP
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
  postThumbnail: string; // thumbnail image
  timestamp: string;
  location: string;  
}
```
```
type PostContent = {
  postId: string;
  postTitle: string;
  postLink: string;
  postThumbnail: string; // thumbnail image
  postContent: string; // use react markdown to render it
}

postContent Markdown
## Video Content
Here is a video:
<video src="https://www.youtube.com/watch?v=dQw4w9WgXcQ"></video>
Image: 
<img src={image_link_from_gcs}></img>
```
```
type PostUploadContent = {
  content: string;
  postTitle: string;
  postThumbnail: string;
}
```
### Upload Image
```
POST /travel/posts/upload
Content-Type: multipart/form-data
body: FormData {file}

response[200] OK
Content-Type: application/json
data: {
  link: string -> GCS location link 
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
  success: true,
  postId
}

success -> navigate(/posts/{postId})
```
### Get Posts
```
GET /travel/posts

response[200] OK
Content-Type: application/json
data: Post[]
```
### Get Post Content - Post View page
```
after travel.com/posts/123

GET /travel/posts/{POST_ID}

response[200] OK
Content-Type: application/json
data: PostContent
```




<!--- Eraser file: https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb --->