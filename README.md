# **Video AI Summarizer Agent** 🎥🎤🖬  

Welcome to the **Phidata Video AI Summarizer Agent**! This application leverages **Google Gemini 2.0 Flash Exp**, **DuckDuckGo Search**, and **Streamlit** to analyze video content and extract meaningful insights.  

## **Features**  
✅ Upload a video file (`.mp4`, `.mov`, `.avi`)  
✅ Ask questions about the video content  
✅ AI-powered insights with **Gemini 2.0 Flash Exp**  
✅ Web research for additional context using **DuckDuckGo**  

---

## **Installation & Setup**  

### **1️⃣ Prerequisites**  
- **Python 3.8+** installed  
- A **Google API Key** for Gemini AI  

### **2️⃣ Install Dependencies**  
Run the following command to install the required libraries:  

```bash
pip install streamlit phidata google-generativeai python-dotenv
```

### **3️⃣ Set Up API Key**  
Create a `.env` file in your project directory and add:  

```env
GOOGLE_API_KEY=your_google_api_key_here
```

This key is used to access **Gemini AI**.

---

## **How to Use**  

### **1️⃣ Start the App**  
Run the Streamlit app:  

```bash
streamlit run your_script.py
```

### **2️⃣ Upload a Video**  
- Click on the **"Upload a video file"** button  
- Select an `.mp4`, `.mov`, or `.avi` file  

### **3️⃣ Enter Your Query**  
- In the text box, type what insights you want from the video  
- Example: _"Summarize the key points in the video"_  

### **4️⃣ Analyze the Video**  
- Click **🔍 "Analyze Video"**  
- The AI agent will:  
  - Upload the video for processing  
  - Analyze its content  
  - Conduct additional web research if needed  
  - Provide a detailed response  

### **5️⃣ View the Results**  
- The summarized insights will be displayed in the app  
- If an error occurs, a message will be shown  

---

## **How the Code Works**  

### **🔹 Initializing the AI Agent**  
The agent is created using the `Agent` class from **Phidata**:  

```python
@st.cache_resource
def initialize_agent():
    return Agent(
        name="Video AI Summarizer",
        model=Gemini(id="gemini-2.0-flash-exp"),
        tools=[DuckDuckGo()],
        markdown=True,
    )

multimodal_Agent = initialize_agent()
```

### **🔹 Uploading and Processing Video**  
- The video is uploaded using `st.file_uploader()`  
- It is temporarily saved for processing  

```python
video_file = st.file_uploader("Upload a video file", type=['mp4', 'mov', 'avi'])
```

- The uploaded file is then processed with:  

```python
processed_video = upload_file(video_path)
```

### **🔹 Running the AI Analysis**  
- The user enters a query  
- The agent constructs a prompt and analyzes the video  

```python
analysis_prompt = f"""
Analyze the uploaded video for content and context.
Respond to the following query using video insights and supplementary web research:
{user_query}
"""
response = multimodal_Agent.run(analysis_prompt, videos=[processed_video])
```

### **🔹 Displaying Results**  
The AI-generated response is displayed:  

```python
st.subheader("Analysis Result")
st.markdown(response.content)
```

---

## **Troubleshooting**  

❌ **Missing API Key?**  
Ensure your `.env` file is set up correctly and restart the app.  

❌ **Video Not Processing?**  
Wait a few seconds and try again—Gemini AI takes time to process videos.  

❌ **Error Message in Analysis?**  
Check the terminal logs for debugging information.  

---

## **Future Enhancements**  
✅ Add support for **more file formats**  
✅ Improve **video processing speed**  
✅ Enhance **response accuracy**  

---

## **Contributors**  
Developed by **Shawneil Rodrigues** 🚀  
Feedback & improvements are always welcome! 🎉  

---

## **License**  
MIT License - Feel free to modify and use! 🚀
