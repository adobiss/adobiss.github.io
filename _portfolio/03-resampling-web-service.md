---
layout: single
title: "Audio Resampling Web Service: Diving into FastAPI and Asynchronous Programming"
permalink: /projects/resampling-web-service
---

**GitHub Repository:** [Audio Resampling Web Service](https://github.com/adobiss/resample-web-service)

## Overview

Developed as a coding test for a job interview, the primary objective of this RESTful Web Service was to accept audio files in WAV or MP3 formats, resample them to a 32kHz MP3 and return the transformed file. Despite unfamiliarity with web service frameworks like Django, Flask or FastAPI, and the concept of asynchronicity, this project became a significant problem-solving and learning experience and led to a successful hiring outcome.

## The Journey

While an estimate of 4-5 hours was provided for the task, the actual project spanned ten full days due to the steep learning curve, much of which was devoted to research.

## Framework Selection ##

After thorough evaluation, FastAPI emerged as the preferred framework. Although Django is robust, it is typically more suited for expansive applications. Flask, being lightweight, lacked built-in asynchronous support at the time of building the service (as well as Django). FastAPI's simplicity, comprehensive documentation and built-in support for asynchronous operations made it the optimal choice to meet the webservice's requirements.

## Key Application Features

- **Concurrency**: Engineered to manage simultaneous client requests efficiently.
- **Optimised Resampling**: The service can identify files already in the required format, optimising the resampling process.
- **Temporary Storage & Data Privacy**: Resampled files are temporarily stored on the server and automatically deleted post-download for storage efficiency and adherence to strict data protection standards.

For setup, environment configurations and service operations, a comprehensive guide is available in the project's README. This implementation embraces a DevOps approach, designed to incorporate a core range of functionalities while providing scope for further refinement.

## Lessons Captured

1. **Strategic Framework Selection**: Choosing the right tool can significantly influence a project's trajectory.
2. **Importance of Targeted Documentation**: FastAPI's user-friendly documentation proved instrumental in implementing the web service and discerning between concurrency, which allows tasks to overlap, and parallelism, the simultaneous execution of tasks.
3. **Audio File & Metadata Management**: Gained hands-on experience in audio manipulation using Python libraries, setting a foundation for future audio-centric projects.

## Conclusion

Through targeted research, the right framework, and principles of asynchronicity, a functional solution materialised after a steep but successful learning journey. All details, including the entire codebase, can be explored on the [project's GitHub repository](https://github.com/adobiss/resample-web-service). [Feedback](/contact/) is always welcome and appreciated.
