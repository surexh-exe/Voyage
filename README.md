# 🌍 **Voyage: Your Personal Travel Itinerary Chatbot**

Welcome to **Voyage** — your ultimate AI travel guide designed to help adventurous travelers plan their perfect itineraries with ease. Built with cutting-edge AI technologies, Voyage allows you to craft detailed, personalized travel plans directly through chat-based interactions, all while enhancing your travel experience with real-time suggestions!

Explore the world, discover hidden gems, and create unforgettable journeys — all through a seamless and interactive chatbot interface!

## 🚀 **Live Demo & Colab Notebook**
You can try out **Voyage** directly by running the chatbot in Google Colab.  
[Run in Google Colab](https://colab.research.google.com/drive/1j_AW1VxTyoCLRFNQjm9v9M8SliXvOIZI?usp=sharing)

## 🛠️ **Technologies Used**
**Voyage** leverages the following advanced technologies to deliver an exceptional user experience:

### 1. **Hugging Face Hub**:
   Hugging Face is a leading platform for natural language processing models, offering pre-trained models that make it easy to build AI applications. We're utilizing Hugging Face's model serving capabilities to power Voyage's natural language understanding.
   
   - **Why Hugging Face?**  
   Hugging Face allows us to tap into cutting-edge language models, enabling Voyage to understand travel-related queries and provide human-like responses.

### 2. **LangChain**:
   LangChain is a framework for developing applications powered by language models. It enables better control over conversational agents, perfect for designing an interactive and smart travel itinerary chatbot.
   
   - **Why LangChain?**  
   LangChain enhances the conversational flow of Voyage, helping the chatbot ask meaningful questions and refine its suggestions based on your responses.

### 3. **OpenAI**:
   OpenAI provides the underlying language model that powers Voyage’s intelligence, allowing the chatbot to engage in natural and insightful conversations with travelers.
   
   - **Why OpenAI?**  
   The sophisticated natural language processing models from OpenAI enable Voyage to give personalized and accurate responses, catering to unique travel needs.

### 4. **Gradio**:
   Gradio is an easy-to-use Python library that allows you to quickly create customizable UIs for machine learning models. With Gradio, users can interact with Voyage directly through a web-based interface.
   
   - **Why Gradio?**  
   Gradio offers an elegant and intuitive interface for interacting with Voyage, providing a seamless way for users to communicate with the chatbot and receive personalized travel recommendations.

---

## 🔧 **How to Use Voyage in Your Web Pages**
Want to integrate **Voyage** into your website or application? It's simple! Here’s how you can get started:

### Step 1: Clone the Repository
```bash
git clone https://huggingface.co/spaces/surexh-exe/Voyage-chatBot
```

### Step 2: Install Dependencies
Ensure you have the required libraries installed:

```bash
pip install gradio huggingface_hub langchain openai
```

### Step 3: Launch the Chatbot
You can launch the Voyage chatbot using Gradio’s interface:

```python

import gradio as gr
from huggingface_hub import InferenceClient
#Initialize the Hugging Face Inference Client
client = InferenceClient("Your hugging face model")

# Define the system message
system_message = ("""You are Voyage, the Personal Travel Itinerary Chatbot, designed to help users plan thrilling and well-organized trips by collecting detailed information and offering customized recommendations.

Introduction: Begin with a brief and engaging introduction to capture the user’s attention.
Question Flow to Collect User Data one by one, Dont collect Multiple data at once atleast perform 7 iterations:
    1) Ask for the user's current location.
    2) Request the travel destination.
    3) Inquire about the number of days for the itinerary.
    4) Gather the budget for the trip.
    5) Find out if the user has any specific preferences.
Confirmation and Next Steps: Express gratitude for the information provided, confirm receipt of all details, and let the user know that you will now suggest exciting places to visit and create a personalized itinerary based on their input.
Itinerary Recommendations: After receiving all the necessary details, present a detailed itinerary in a tabular format. This should include hotel names, restaurant names, resort names, and a daily schedule for each day of the trip, tailored to the user’s destination and itinerary duration.""")

def respond(message, history):
    # Set parameters
    max_tokens = 1800
    temperature = 0.7
    top_p = 0.95

    # Prepare messages for the model
    messages = [{"role": "system", "content": system_message}]

    for val in history:
        if val[0]:
            messages.append({"role": "user", "content": val[0]})
        if val[1]:
            messages.append({"role": "assistant", "content": val[1]})

    messages.append({"role": "user", "content": message})

    response = ""

    try:
        for message in client.chat_completion(
            messages,
            max_tokens=max_tokens,
            stream=True,
            temperature=temperature,
            top_p=top_p,
        ):
            token = message.choices[0].delta.content
            response += token
            yield response
    except Exception as e:
        yield f"An error occurred: {str(e)}"

# Create the Gradio chat interface
demo = gr.ChatInterface(
    fn=respond,
    theme="default"
)

if __name__ == "__main__":
    demo.launch()
```

### Step 4: Customizing the Chatbot for Your Needs
Feel free to modify the codebase to tailor the chatbot to your own travel requirements. You can easily integrate the chatbot within any website by embedding the Gradio interface.

---

## 🎯 **Features**
- **Personalized Itineraries**: Based on your travel preferences, location, and budget.
- **Real-Time Suggestions**: Get instant recommendations for hotels, restaurants, and attractions.
- **Engaging Conversations**: A friendly, interactive bot that helps refine your trip through meaningful Q&A.
- **Seamless Integration**: Easily plug into your website or project with minimal setup.

---

## 🌐 **License**
This project is licensed under the MIT License — feel free to explore, modify, and deploy as you wish!

---

Ready to start planning your next adventure? Try **Voyage** today and explore the world like never before! 🌍✈️

