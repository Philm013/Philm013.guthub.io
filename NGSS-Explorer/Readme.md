Of course. Here is the revised README with the requested technical specifications, including details about the AI context.

---

# NGSS 3D + PE Explorer: README

## 1. Overview

The **NGSS 3D + PE Explorer** is a comprehensive, client-side web application designed for educators, curriculum developers, and instructional coaches. It provides a powerful and intuitive interface to explore, analyze, and organize the Next Generation Science Standards (NGSS).

This tool operates entirely within a single HTML file, requiring no internet connection for its core features. The AI integration is an exception, as it requires communication with Google's servers. The application allows users to seamlessly navigate between Performance Expectations (PEs), the three dimensions of the standards (SEPs, DCIs, CCCs), and their grade-band progressions. Advanced features like PE bundling, a progression matrix, and AI-powered analysis help users deconstruct standards and design cohesive, three-dimensional learning experiences.

## 2. Key Features

*   **Three Powerful Views:**
    *   **PE Explorer:** A searchable and filterable database of all NGSS Performance Expectations.
    *   **3D Explorer:** A detailed view of the Science and Engineering Practices (SEPs), Disciplinary Core Ideas (DCIs), and Crosscutting Concepts (CCCs) with their K-12 grade-band progressions.
    *   **Matrix View:** A customizable matrix that visualizes the connections between 3D Elements and PEs across different grade levels.
*   **Performance Expectation (PE) Bundling:** Select multiple PEs to create custom "bundles." The tool generates a summary of all the 3D elements covered by the bundle, aiding in unit and lesson planning. Bundles can be saved, managed, and reloaded.
*   **AI-Powered Analysis (Gemini):**
    *   Integrates with the Google Gemini API to automatically analyze and color-code PE descriptions and Evidence Statements.
    *   Visually identifies phrases related to SEPs (blue), DCIs (orange), and CCCs (green).
    *   Features a flexible **interactive editor** that allows for nested formatting (e.g., adding an underline to a word within an already-highlighted phrase).
*   **Advanced Filtering and Search:**
    *   Filter PEs by Grade, Topic, or specific 3D Elements.
    *   Filter the 3D Explorer and Matrix View by Dimension, Core Idea, and Component Idea.
    *   A global search bar instantly filters the content in the current view.
*   **Interactive and User-Friendly:**
    *   Clickable links connect PEs to their constituent 3D elements and vice-versa.
    *   Right-click (or use the context menu) to easily copy the text of any standard, description, or element.
    *   The application state is saved in the URL, allowing you to bookmark or share a specific view with all your filters applied.
*   **Self-Contained and Private:** The tool runs entirely in your browser. Your data, saved bundles, and API key are stored locally and are never sent to an external server (except for API calls made directly from your browser to Google's AI services).

## 3. How to Use the Tool

### Getting Started

Simply open the `ngss-explorer.html` file in a modern web browser like Chrome, Firefox, or Edge.

### The Main Views

You can switch between the three primary views using the navigation buttons at the top of the sidebar.

#### 3.1. PE Explorer

This is the default view and serves as the main dashboard for finding and analyzing Performance Expectations.

*   **Browsing and Filtering:** Use the filters in the sidebar to narrow down the list of PEs by Bundle, Grade, Topic, or specific 3D Elements.
*   **Viewing PE Details:** Click on any PE row to expand it. The expanded view shows the full description, clarification statements, assessment boundaries, a breakdown of its three dimensions, and connections to other standards.
*   **Interacting with Details:** Within the details pane, the 3D element text is clickable. Clicking an element will take you to the **3D Explorer** and highlight that element for you.

#### 3.2. 3D Explorer

This view is designed for understanding the vertical progression of the standards across grade bands.

*   **Navigating:** The table displays all SEPs, DCIs, and CCCs, organized by dimension and showing the learning progressions for each grade band.
*   **Highlighting a PE:** When you navigate to this view from a PE, all of its associated elements are highlighted, making it easy to see the PE's three-dimensional foundation.
*   **Finding Related PEs:** Click on any specific progression item in the table. A modal window will appear listing all the PEs that are linked to that specific item.

#### 3.3. Matrix View

This view provides a high-level "map" of the standards, showing how often and where 3D elements appear across grade levels.

*   **Setting up the Matrix:** Use the **"Select/Refine Rows"** button to choose which 3D elements you want to include in the matrix.
*   **Reading the Matrix:** The table shows your selected elements as rows and the NGSS grade levels as columns. The cells are populated with the PE codes that connect them, providing a powerful visualization for curriculum planning.

## 4. Advanced Features

### 4.1. PE Bundling

This feature is essential for curriculum planning and unit design.

1.  **Select PEs:** In the **PE Explorer**, use the checkboxes to select PEs.
2.  **View Bundle Details:** Click **"View Bundle Details"** to see a summary of all 3D elements covered by your selection, followed by the details for each PE.
3.  **Save Your Bundle:** Click **"Save Bundle"** to give your selection a name for later use.
4.  **Manage and Filter:** Use the **"Manage"** button and the "Filter by Bundle" dropdown in the sidebar to load, delete, and filter by your saved bundles.

### 4.2. AI (Gemini) Integration

This feature uses generative AI to deconstruct standards visually.

1.  **Setup:**
    *   Click the **"Settings"** button in the header.
    *   Enter your **Google Gemini API Key**. (You can get a free key from Google AI Studio).
    *   Your key is saved securely in your browser's local storage and is not shared.
2.  **Analyze Content:**
    *   In a PE's detail view, click the **"Analyze with Full Context"** button to color-code its description.
    *   In the Evidence Statements modal, click **"Analyze with AI"**.
3.  **Interactive Editing (Improved):**
    *   After an analysis, you can easily refine the output.
    *   **To create a new highlight:** Select any text with your mouse. An edit menu will appear, allowing you to apply formatting.
    *   **To edit an existing highlight:** Simply click on the colored text to bring up the edit menu.
    *   **To add nested formatting:** **Select text *within* an already-highlighted span**. For example, you can select a few words inside a sentence marked as a DCI (orange) and use the menu to add an SEP underline to just those words, without affecting the original DCI highlight.

## 5. Technical Specifications

This section details the tool's architecture and how the AI integration functions.

*   **Architecture:** The application is a single-file, client-side tool built with vanilla JavaScript (ESM), HTML, and CSS. It has no server-side backend, which ensures privacy and offline functionality for core features.
*   **Data Handling:** All NGSS data is pre-compiled into local JavaScript files (`ngssK5.js`, `ngss68.js`, etc.). On launch, this data is loaded into memory, creating an instantly accessible local database.
*   **Persistence:** User-generated content is stored in the browser's `localStorage`. This includes:
    *   `ngssPeBundle`: The set of PEs currently selected for bundling.
    *   `ngssSavedBundles`: A JSON object of all user-saved bundles.
    *   `ngssAiAnalyses`: A JSON object containing the saved HTML of any AI-analyzed or manually edited text, keyed by PE ID.
    *   `geminiApiKey`: The user's Google Gemini API key.
*   **State Management:** The application's current state (active view, filters, search terms, expanded PE) is encoded into the URL's query parameters. This allows users to bookmark and share links that will restore the exact same view for others.

### AI Integration Details

The AI analysis is powered by the **Google Gemini** family of models.

*   **API & Model:** The tool uses the `gemini-1.5-flash` model via the official Google GenAI JavaScript SDK.
*   **Privacy:** The API key and all analysis requests are sent directly from the user's browser to the Google API endpoint. They are not proxied through any third-party server, ensuring the privacy of your key and data.
*   **Context Provided to the AI:** To ensure a high-quality, context-aware analysis, the tool does not just send the text to be colored. It provides the AI with a rich, structured set of reference data for the specific PE being analyzed. The context block sent to the AI includes:
    1.  **Performance Expectation:** The PE's code (e.g., 3-LS1-1) and its full description.
    2.  **Clarification Statement:** The full text, if available.
    3.  **Assessment Boundary:** The full text, if available.
    4.  **Associated 3D Elements:** A complete list of all SEPs, DCIs, and CCCs officially connected to the PE, including their codes and descriptive text.
    5.  **Evidence Statements:** The complete, raw text of the PE's evidence statements.
*   **Prompt Engineering:** The tool uses a detailed system prompt to guide the AI's response. The prompt instructs the AI to:
    *   **Assume a Role:** Act as an expert in NGSS standards and curriculum design.
    *   **Understand the Task:** Use the provided context to analyze a separate piece of "content to modify" (either the PE description or the evidence statements).
    *   **Strict Output Formatting:** Return **only** the modified HTML content. It is explicitly instructed not to include explanations, markdown code blocks (```html), or any other conversational text.
    *   **Obey HTML Rules:** A critical rule is provided: `<span>` tags must only wrap inline text content and must *not* wrap block-level elements like `<p>` or `<div>`. This ensures the returned HTML is valid and integrates cleanly.
