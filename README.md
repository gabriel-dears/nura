# Nura - YouTube Video Processing and Analysis System

Nura is an advanced video processing system that automatically processes YouTube videos to generate clips, transcribe and summarize content, categorize themes, and create metadata for better accessibility. It utilizes a microservice architecture, integrating different technologies like video processing, machine learning, and third-party APIs to generate and manage video content effectively.

## Project Overview

The Nura system automates the process of extracting, analyzing, and categorizing video content from YouTube. It uses a combination of speech recognition, summarization, and categorization models, alongside video generation and machine learning to produce relevant video clips and metadata.

### Key Features:
- **Audio Chunking**: Download and split videos into 30-second chunks.
- **Transcription**: Convert speech from audio chunks into text using speech-to-text models.
- **Summarization**: Summarize transcriptions into short and meaningful summaries.
- **Categorization**: Categorize video content based on the summarized text.
- **Clip Generation**: Automatically generate clips based on the most relevant topics discussed in the video.
- **Trend Analysis**: Use social media trends to influence video categorization and clip generation.
- **YouTube Upload**: Automatically upload the generated clips to YouTube with optimized metadata.

## Architecture Overview

Nura uses a **microservices architecture** with the following main components:

1. **Video Downloader Service**: Responsible for downloading videos from YouTube using the provided channel ID. It handles fetching videos (excluding shorts) and splitting them into 30-second chunks.
   
2. **Transcription Service**: This service processes the audio chunks from videos and transcribes them into text using speech recognition technologies.

3. **Summarization Service**: Once transcriptions are complete, this service takes the text and generates a summary of the most relevant information.

4. **Categorization Service**: Based on the summary and text analysis, this service categorizes the video content into predefined topics or themes.

5. **Clip Generation Service**: Using the categorized data and identified trends, this service generates video clips and prepares them for upload to YouTube.

6. **Trend Analysis Service**: This service fetches the latest trends from social media platforms like Twitter and categorizes them, influencing the categorization and summarization of video content.

7. **YouTube API Service**: Responsible for uploading the generated clips to YouTube and managing metadata, including titles and descriptions based on the video content and social media trends.

8. **Database Service**: Stores video metadata, trends, transcriptions, and categorization results. It ensures no video is processed twice by keeping track of previously processed videos.

9. **Messaging Queue Service**: Used for communication between services. RabbitMQ is the message broker used for service communication (e.g., sending transcriptions for summarization, summaries for categorization, etc.).

10. **API Gateway**: Exposes endpoints for triggering the system's workflows. It can be used to initiate video processing, get clip details, or interact with other services in the ecosystem.

---

## Microservices Breakdown

### 1. **Video Downloader Service**
- **Language/Technology**: Java, Spring Boot
- **Responsibilities**: Downloads videos from YouTube, excluding shorts, using the provided channel ID and fetches metadata.
- **Input**: Channel IDs from the YouTube API.
- **Output**: 30-second audio chunks stored in cloud storage.

### 2. **Transcription Service**
- **Language/Technology**: Python, FastAPI
- **Responsibilities**: Transcribes the audio chunks into text using SpeechRecognition or a similar service.
- **Input**: Audio chunks in WAV format.
- **Output**: Transcribed text for each audio chunk.

### 3. **Summarization Service**
- **Language/Technology**: Python, FastAPI
- **Responsibilities**: Summarizes transcriptions using an AI-based summarization model like T5.
- **Input**: Transcribed text.
- **Output**: Summarized text that provides a concise version of the original transcription.

### 4. **Categorization Service**
- **Language/Technology**: Python, FastAPI
- **Responsibilities**: Categorizes summarized text into predefined topics or categories (e.g., sports, politics).
- **Input**: Summarized text.
- **Output**: Categorized data for each video.

### 5. **Clip Generation Service**
- **Language/Technology**: Python, FFmpeg
- **Responsibilities**: Generates video clips based on categorized data, ensuring that clips are relevant to the identified themes.
- **Input**: Video chunks and categorized themes.
- **Output**: Video clips stored in cloud storage.

### 6. **Trend Analysis Service**
- **Language/Technology**: Python
- **Responsibilities**: Analyzes social media trends (e.g., Twitter) and categorizes relevant topics. These trends influence the categorization of video content.
- **Input**: Social media API data (e.g., Twitter trends).
- **Output**: Categorized trend topics stored in the database.

### 7. **YouTube API Service**
- **Language/Technology**: Java, Spring Boot
- **Responsibilities**: Manages YouTube API interactions, uploading generated clips to YouTube with appropriate metadata (titles, descriptions, tags).
- **Input**: Video clips and metadata.
- **Output**: Uploaded video clips on YouTube.

### 8. **Database Service**
- **Language/Technology**: Java, Spring Boot (PostgreSQL)
- **Responsibilities**: Stores video metadata, transcription data, trend information, and categorized results.
- **Input**: Transcriptions, video metadata, trends, and categories.
- **Output**: Persistent storage of all processed data.

### 9. **Messaging Queue Service (RabbitMQ)**
- **Language/Technology**: RabbitMQ
- **Responsibilities**: Ensures asynchronous communication between services, enabling each service to process tasks independently.
- **Input**: Messages from various services (e.g., transcription completed, summarization requested).
- **Output**: Triggered services based on messages in the queue.

### 10. **API Gateway**
- **Language/Technology**: Java, Spring Boot
- **Responsibilities**: Exposes REST APIs to trigger the various workflows (e.g., initiate video processing, get clip details, upload clips).
- **Input**: External API requests.
- **Output**: Responses triggering processes across microservices.

---

## Resources

### Cloud Infrastructure
- **Compute**: AWS EC2, Google Cloud Compute Engine, or Azure VMs.
- **Storage**: AWS S3, Google Cloud Storage, or Azure Blob Storage.
- **Database**: PostgreSQL on AWS RDS, Google Cloud SQL, or Azure SQL Database.
- **Messaging**: RabbitMQ for inter-service communication.
- **Machine Learning**: TensorFlow or PyTorch for summarization models; use GPU-based instances if needed.
- **API Gateway**: AWS API Gateway or similar services.

### Third-Party APIs
- **YouTube API**: For video retrieval, metadata, and uploads.
- **Twitter API**: For retrieving social media trends.

---

## Running the System

1. **Set up the database**: Create PostgreSQL databases for storing video metadata, transcriptions, and trends.
2. **Configure the API Gateway**: Expose endpoints for triggering video processing and retrieving results.
3. **Deploy each service**: Set up the individual services (downloader, transcription, summarization, categorization, etc.) and deploy them in a containerized or serverless environment.
4. **Start the pipeline**: Trigger the system with a channel ID or manually initiate the workflow using the API Gateway.

---

## Future Enhancements
- **Scaling**: Implement auto-scaling for high-demand workloads.
- **AI/ML Optimization**: Continuously train models to improve summarization and categorization accuracy.
- **Social Media Trend Integration**: Enhance the trend analysis service to include more platforms beyond Twitter.
- **Video Generation Improvements**: Implement more advanced techniques for video clip creation, including automated thumbnail generation.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

