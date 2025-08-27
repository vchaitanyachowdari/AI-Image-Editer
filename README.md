<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

# Pixshop - AI Photo Editor

A powerful, AI-powered photo editor that allows you to retouch, apply creative filters, and make professional adjustments to your images using simple text prompts.

## ✨ Features

-   **Precise Retouching**: Click on any part of your image to select a hotspot, then describe your desired edit (e.g., "change my shirt color to blue", "remove the person in the background").
-   **Creative Filters**: Instantly transform your photos with a variety of artistic styles. Choose from presets like *Synthwave* and *Anime*, or describe your own unique filter.
-   **Professional Adjustments**: Make global enhancements to your images with ease. Apply effects like *Blur Background* for a portrait look, *Enhance Details*, or change the lighting.
-   **Standard Editing Tools**: Includes essential tools like cropping with fixed aspect ratios (1:1, 16:9) or freeform.
-   **Full History Control**:
    -   Undo and redo your edits.
    -   Press and hold to compare your current edit with the original image.
    -   Reset all changes and start over.
-   **Easy to Use**: Upload an image, choose a tool, and start editing. Download your final creation with a single click.

## 🛠️ Tech Stack

-   **Frontend**: [React](https://reactjs.org/) with [TypeScript](https://www.typescriptlang.org/)
-   **Styling**: [Tailwind CSS](https://tailwindcss.com/)
-   **AI Model**: [Google Gemini API](https://ai.google.dev/) (`gemini-2.5-flash-image-preview`) for all image generation and editing tasks.
-   **Dependencies**: `react-image-crop` for the cropping interface.

## 🚀 Getting Started

To run this project locally, you will need to set up your environment and obtain a Google AI API key.

### Prerequisites

-   A Google AI API Key. You can get one from [Google AI Studio](https://aistudio.google.com/app/apikey).
-   In this development environment, the API key is expected to be available as an environment variable (`process.env.API_KEY`).

### How It Works

1.  **Set up the API Key**: The application is configured to use an `API_KEY` from the environment. Ensure this is set up in your deployment or local environment.
2.  **Run the Application**: Simply open the `index.html` file in a browser. The application is self-contained.

### Local Development Outside This Environment

If you are running this project on your own machine:

1.  **Install dependencies:**
    ```bash
    npm install
    ```

2.  **Set up environment variables:**
    -   Create a new file named `.env` in the root of the project.
    -   Copy the contents from `.env.example` into your new `.env` file.
    -   Replace `YOUR_GOOGLE_AI_API_KEY` with your actual Google AI API key.

    Your `.env` file should look like this:
    ```
    API_KEY="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    ```

3.  **Run the application:**
    ```bash
    npm run dev
    ```

## 📝 AI Interaction Details

The application leverages the `gemini-2.5-flash-image-preview` model from the Google Gemini API.

-   **Image Upload**: The user uploads an image, which is stored in the browser's memory as a `File` object.
-   **Prompt Engineering**: When a user performs an action (e.g., retouching, applying a filter), the application constructs a detailed prompt. This prompt includes the original image, the user's text input, and specific instructions for the AI model to ensure it performs the desired edit correctly and safely. For retouching, it also includes the (x, y) coordinates of the click.
-   **API Call**: The prompt and image data (converted to a base64 string) are sent to the Gemini API via the `@google/genai` SDK.
-   **Image Response**: The API processes the request and returns a new, edited image. The application code carefully handles the response to extract the image data and manage potential errors or safety blocks.
-   **History Management**: Each new image returned from the API is added to a history stack, allowing the user to navigate back and forth between edits.
