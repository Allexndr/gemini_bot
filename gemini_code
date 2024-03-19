import telebot
import google.generativeai as genai

bot = telebot.TeleBot("")

genai.configure(api_key="AIzaSyCrxXOE4h3nfOHGatKQYCxVH089hwmlDZo")

generation_config = {
    "temperature": 0.9,
    "top_p": 1,
    "top_k": 1,
    "max_output_tokens": 2048,
}

safety_settings = [
    {
        "category": "HARM_CATEGORY_HARASSMENT",
        "threshold": "BLOCK_MEDIUM_AND_ABOVE"
    },
    {
        "category": "HARM_CATEGORY_HATE_SPEECH",
        "threshold": "BLOCK_MEDIUM_AND_ABOVE"
    },
    {
        "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
        "threshold": "BLOCK_MEDIUM_AND_ABOVE"
    },
    {
        "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
        "threshold": "BLOCK_MEDIUM_AND_ABOVE"
    },
]

model = genai.GenerativeModel(model_name="gemini-1.0-pro",
                              generation_config=generation_config,
                              safety_settings=safety_settings)

convo = model.start_chat(history=[
    {
        "role": "user",
        "parts": ["Hi"]
    },
    {
        "role": "model",
        "parts": ["Hello there! How can I assist you today?"]
    },
])




@bot.message_handler(func=lambda message: True)
def echo_all(message):
    convo.send_message(message.text)
    response = convo.last.text
    print(response)
    bot.send_message(message.chat.id, response)



bot.infinity_polling()
