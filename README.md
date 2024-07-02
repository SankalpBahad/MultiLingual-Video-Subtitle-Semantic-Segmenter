# Multilingual-Semantic-Chunking-of-Video-Subtitles

## Task Description

The task is to extract high quality and semantically meaningful segments of text from a video. Major steps are downloading the video, extracting the audio, transcribing the extracted audio and appropriate segmentation into chunks.

## Workflow

### Downloading the video from URL

Python's library Pytube was used to download the mp4 file of the video from the url provided. Pytube is easy to use and does not have compatibility issues.

### Extracting audio from the video

The library MoviePy was used for extracting the mp3 audio file from the mp4 video file. 

### Transcription of the audio

OpenAI's Whisper model, which has been observed to outperform many of the audio transcription tools was used for transcribing the audio from the audio file. The audio transcriptions were observed to be fairly accurate. The model also helped with time alignment of the transcript with audio, resulting in various segments of audio with start and end times.

The segments were not observed to be semantically segmented and hence some post processing was performed in order to chunk the text into proper semantically segmented chunks using the segments provided by the model's output.

### Chunking of text

In order to semantically chunk the data, the following logic was used. The embeddings for all the segments were first generated using the "bert-base-uncased" model. Following this, the semantic similarity score was calculated of the neighbouring segments of data, using cosine similarity on the embeddings as a metric. A threshold was set for accepting or rejecting segments into a chunk, considering the total length of the chunk to not exceed the time threshold of 15 seconds. Special focus was set on the sentences to not be split into different chunks.

This approach resulted in high quality and semantically rich chunks of the desired length.

#### This approach is a generalized approach and would work for any youtube video URL. For transcription, the tool used is OpenAI's Whisper, which is observed to have multi-language support. This should eliminate failure issues due to language choice.
