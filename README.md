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

Design: [﻿builder.io/content](https://builder.io/content) 

# Tech Stack
## Frontend
- React, TypeScript
### Post Editor
- [﻿Editor.js](https://editorjs.io/) : Amazing, Bravo!! Have very detailed docs 
- [﻿BlockNote](https://github.com/TypeCellOS/BlockNote) : Looks like Notion block
- [﻿Yoopta-Editor](https://github.com/Darginec05/Yoopta-Editor) 
- LiveBlock:  real-time collaboration
    - [﻿liveblocks.io/](https://liveblocks.io/) 
- Tiptap 
    - [﻿tiptap.dev/docs/examples/basics/default-text-editor](https://tiptap.dev/docs/examples/basics/default-text-editor)  
    - [﻿tiptap.dev/docs/editor/extensions/nodes/image](https://tiptap.dev/docs/editor/extensions/nodes/image) 
### CSS Style
- Figma AI
- Tailwind
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
  postID: string;
  postTitle: string; 
  postThumbnail: File; // default: travel.jpeg 
  postPreviewLink: string;
  block: Block; // editor.js input format
  travelPlan: Plan; 
}
```
```
type PostUploadContent = {
  postTitle: string;
  postThumbnail: file;
  blockData: Block;
  travelPlan: Plan; 
}
```
```
type BlockData = {
  time: timestamp;
  id: string; 
  blocks: Block[] 
}

type Block = {
  blockId: string;
  blocks: [
    
  ]
}
```
```
type Plan = {
  
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
# Frontend Story: AI & Block Editor
## AI Candidates
- OpenAI
- Claude
- Llama
## Editor Candidates
- Editor.js
## Data
### Travel Plan Data
```
{
  "travel_plan": [
    {
      "day": 1,
      "departure": "Austin, TX",
      "destination": "San Antonio, TX",
      "activities": [
        {"time": "morning", "activity": "Depart from Austin to San Antonio (1.5-hour drive)"},
        {"time": "afternoon", "activity": "Visit the Alamo and River Walk"},
        {"time": "evening", "activity": "Enjoy dinner in the Pearl District"}
      ],
      "overnight": "San Antonio, TX"
    },
    {
      "day": 2,
      "departure": "San Antonio, TX",
      "destination": "El Paso, TX",
      "activities": [
        {"time": "morning", "activity": "Drive to El Paso (8-hour drive)"},
        {"time": "afternoon", "activity": "Explore the El Paso Museum of Art"},
        {"time": "evening", "activity": "Enjoy local cuisine at L&J Cafe"}
      ],
      "overnight": "El Paso, TX"
    },
    {
      "day": 3,
      "departure": "El Paso, TX",
      "destination": "Tucson, AZ",
      "activities": [
        {"time": "morning", "activity": "Depart for Tucson (4.5-hour drive)"},
        {"time": "afternoon", "activity": "Visit Saguaro National Park"},
        {"time": "evening", "activity": "Dinner at El Charro Café"}
      ],
      "overnight": "Tucson, AZ"
    },
    {
      "day": 4,
      "departure": "Tucson, AZ",
      "destination": "Phoenix, AZ",
      "activities": [
        {"time": "morning", "activity": "Drive to Phoenix (2-hour drive)"},
        {"time": "afternoon", "activity": "Explore Desert Botanical Garden"},
        {"time": "evening", "activity": "Dinner in downtown Phoenix"}
      ],
      "overnight": "Phoenix, AZ"
    },
    {
      "day": 5,
      "departure": "Phoenix, AZ",
      "destination": "Los Angeles, CA",
      "activities": [
        {"time": "morning", "activity": "Drive to Los Angeles (6-hour drive)"},
        {"time": "afternoon", "activity": "Visit Griffith Observatory or Santa Monica Pier"},
        {"time": "evening", "activity": "Dinner in West Hollywood"}
      ],
      "overnight": "Los Angeles, CA"
    },
    {
      "day": 6,
      "departure": "Los Angeles, CA",
      "destination": "Santa Barbara, CA",
      "activities": [
        {"time": "morning", "activity": "Depart for Santa Barbara (2-hour drive)"},
        {"time": "afternoon", "activity": "Explore Stearns Wharf and State Street"},
        {"time": "evening", "activity": "Dinner at a beachside restaurant"}
      ],
      "overnight": "Santa Barbara, CA"
    },
    {
      "day": 7,
      "departure": "Santa Barbara, CA",
      "destination": "San Francisco, CA",
      "activities": [
        {"time": "morning", "activity": "Drive to San Francisco (5-hour drive)"},
        {"time": "afternoon", "activity": "Visit Golden Gate Bridge and Fisherman's Wharf"},
        {"time": "evening", "activity": "Dinner in Chinatown"}
      ],
      "overnight": "San Francisco, CA"
    }
  ]
}
```
### Block Editor Data 
```
{
  "time": 1633345270320,
  "blocks": [
    {
      "type": "header",
      "data": {
        "text": "Editor.js Example",
        "level": 2
      }
    },
    {
      "type": "paragraph",
      "data": {
        "text": "This is an example of content for Editor.js."
      }
    },
    {
      "type": "image",
      "data": {
        "file": {
          "url": "https://example.com/image.jpg"
        },
        "caption": "Example Image",
        "withBorder": false,
        "stretched": false,
        "withBackground": false
      }
    },
    {
      "type": "list",
      "data": {
        "style": "unordered",
        "items": [
          "First item",
          "Second item",
          "Third item"
        ]
      }
    }
  ],
  "version": "2.22.2"
}
```
## How AI works with Editor
1. At AI assistance page, user chat with AI assistance and confirm the travel plan
2. then request AI to generate travel plan and block editor json data
    1. travel plan data 
        1. maybe later used to compare with block editor data
        2. generate travel report
        3. machine learning
    2. block editor data -> editor.js input format
3. both data will be saved in the Post 
4. after data saved success, navigate to Post page
```
PostContent = {
  postID: "post123"
  postTitle: "AI generated travel plan",
  postThumbnail: travel.jpeg File
  postPreviewLink: ""
  block: Block; // editor.js input format
  travelPlan: Plan; 
}
```
# Maybe Useful
[﻿www.langchain.com/](https://www.langchain.com/) 

[﻿www.pinecone.io/](https://www.pinecone.io/) 




<!-- eraser-additional-content -->
## Diagrams
<!-- eraser-additional-files -->
<a href="/README-FlowChart-1.eraserdiagram" data-element-id="t8XJn4yzZsfzSLFqMhi_l"><img src="/.eraser/msyd9SQo08JUWQItKwPb___U806QwDlsSPtLlAvlCOgMCkeE3W2___---diagram----14acf7252718882ca76278458be2983b-FlowChart.png" alt="" data-element-id="t8XJn4yzZsfzSLFqMhi_l" /></a>
<!-- end-eraser-additional-files -->
<!-- end-eraser-additional-content -->
<!--- Eraser file: https://app.eraser.io/workspace/msyd9SQo08JUWQItKwPb --->