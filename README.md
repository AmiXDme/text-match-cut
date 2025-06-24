# Text Match Cut Video Generator Web App

A Flask web application that generates short "match cut" style videos featuring highlighted text. The app centers a specific phrase, surrounds it with related or random text, applies optional blur effects, and allows customization of colors, dimensions, and duration. It can optionally use the Mistral AI **or Gemini AI** API to generate contextually relevant surrounding text.

![image](static/image.png)

## Features

*   **Web-Based Interface:** Easy-to-use form built with Flask and HTML.
*   **Custom Highlight Text:** Specify the exact phrase you want to highlight.
*   **Configurable Video:** Adjust video width, height, duration (seconds), and frames per second (FPS).
*   **Color Customization:** Set colors for text, background, and the highlight box using a color picker.
*   **Blur Effects:**
    *   **Gaussian Blur:** Apply a standard blur to the background text.
    *   **Radial Blur:** Keep the center sharp and increasingly blur towards the edges.
    *   **None:** No blur effect.
    *   Adjustable blur radius.
*   **Dynamic Text Generation:**
    *   **Mistral AI:** (Optional, requires API key) Generates multiple lines of text thematically related to your highlight phrase, ensuring the phrase is included naturally.
    *   **Gemini AI:** (Optional, requires API key) Uses Google Generative AI to generate contextually relevant text.
    *   **Random Text:** Falls back to generating random words if AI is disabled or unavailable.
*   **Font Handling:** Uses fonts from a local `fonts/` directory or falls back to system fonts. Randomly selects fonts for visual variety frame-by-frame.
*   **MP4 Output:** Generates a downloadable `.mp4` video file.
*   **Error Handling:** Provides feedback for font issues or generation errors.
*   **AI Provider Selection:** Choose between Mistral, Gemini, or random text in the web UI.

## Requirements

*   **Python:** 3.8+ recommended.
*   **pip:** Python package installer.
*   **FFmpeg:** Essential for video encoding/writing by Moviepy. **You MUST install FFmpeg separately** and ensure it's accessible in your system's PATH. Download from [ffmpeg.org](https://ffmpeg.org/download.html).
*   **Mistral AI API Key:** (Optional) Required *only* if you want to use the Mistral AI text generation feature. You'll need to sign up at [Mistral AI](https://mistral.ai/) to get one.
*   **Gemini AI API Key:** (Optional) Required *only* if you want to use Gemini (Google Generative AI). Get an API key from [Google AI Studio](https://aistudio.google.com/app/apikey).

## Installation & Setup

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/AmiXDme/text-match-cut.git
    cd text-match-cut
    ```

2.  **Create a Virtual Environment (Recommended):**
    ```bash
    python -m venv venv
    # On Windows:
    .\venv\Scripts\activate
    # On macOS/Linux:
    source venv/bin/activate
    ```

3.  **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set Up AI API Keys (Optional):**
    *   Create a file named `.env` in the project's root directory (`text-match-cut/`).
    *   Add your API keys to this file (add one or both as needed):
        ```ini
        # .env
        MISTRAL_API_KEY=your_actual_mistral_api_key_here
        GEMINI_API_KEY=your_actual_gemini_api_key_here
        ```
    *   The application will automatically load these keys. If both keys are missing or invalid, or if the libraries aren't installed, the AI feature will be disabled, and the app will use random text generation.

5.  **Add Fonts:**
    *   Place `.ttf` or `.otf` font files into the `fonts/` directory. The application prioritizes fonts found here.
    *   If the `fonts/` directory is empty or no valid fonts are found, it will attempt to use system-installed fonts (which might be less reliable across different environments). **Having fonts in the `fonts/` folder is highly recommended.**

6.  **Ensure Output Directory Exists:**
    *   The script automatically creates an `output/` directory where generated videos are temporarily stored. Ensure your application has write permissions for this directory.

## Usage

1.  **Run the Flask Application:**
    ```bash
    python app.py
    ```

2.  **Access the Web Interface:**
    *   Open your web browser and navigate to `http://127.0.0.1:5000/` (or the address provided in the terminal, especially if running on a different host/port).

3.  **Configure Video Parameters:**
    *   Fill out the form with your desired settings: highlighted text, duration, dimensions, colors, blur options, etc.
    *   Check/uncheck the "Use AI for Text Generation" box (it will be disabled if no API keys are set up or the libraries are missing).
    *   Select your preferred AI provider (Mistral, Gemini, or Random) from the dropdown.

4.  **Generate Video:**
    *   Click the "Generate Video" button.
    *   The process might take some time depending on video duration, resolution, and your system's performance. A loading indicator will be shown. Check the terminal running `app.py` for progress logs and potential errors.

5.  **Download:**
    *   If generation is successful, a download link for the `.mp4` file will appear on the page.
    *   If errors occur (e.g., font issues, FFmpeg problems, AI errors), an error message will be displayed on the page.

## Project Structure
```
text-match-cut/
├── app.py # Main Flask application, includes video generation logic
├── requirements.txt # Python dependencies
├── templates/
│   └── index.html # HTML template for the web UI
├── static/
│   └── style.css # Optional CSS for styling
├── fonts/ # <--- Add your .ttf/.otf font files here
│   └── (example.ttf)
├── output/ # Generated videos are saved here temporarily
├── .env # Store your MISTRAL_API_KEY and/or GEMINI_API_KEY here (Create this file!)
└── README.md # This file
```

## Technology Stack

*   **Backend:** Flask
*   **Video Processing:** Moviepy (relies on FFmpeg)
*   **Image Manipulation:** Pillow (PIL Fork)
*   **Numerical Operations:** NumPy
*   **AI Text Generation (Optional):** Mistral AI Python Client (`mistralai`), Google Generative AI (`google-generativeai`)
*   **Environment Variables:** `python-dotenv`
*   **Font Handling Fallback:** Matplotlib (`font_manager`)

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue if you find bugs or have suggestions for improvements.

## Acknowledgements

*   Inspired by kinetic typography and text-based video effects.
*   Uses the powerful Mistral AI and Gemini AI models for creative text generation.
*   Inspired by https://github.com/lrdcxdes/text-match-cut
*   My YouTube channel: [@AmiXDme](https://www.youtube.com/@AmiXDme)
