import os
import telebot
from google.cloud import dialogflow

# Токены (будут скрыты в Secrets)
TELEGRAM_TOKEN = os.getenv('7993921779:AAGgRBsmxqelBqcpt9217cPDPcBrOprRibI')
DIALOGFLOW_PROJECT_ID = os.getenv('newagent-hymr')

bot = telebot.TeleBot(TELEGRAM_TOKEN)

@bot.message_handler(func=lambda message: True)
def handle_message(message):
    # Отправляем сообщение в Dialogflow
    session_client = dialogflow.SessionsClient()
    session = session_client.session_path(DIALOGFLOW_PROJECT_ID, message.chat.id)
    text_input = dialogflow.TextInput(text=message.text, language_code='ru')
    query_input = dialogflow.QueryInput(text=text_input)
    
    response = session_client.detect_intent(
        request={"session": session, "query_input": query_input}
    )
    
    # Отправляем ответ пользователю
    bot.reply_to(message, response.query_result.fulfillment_text)

if __name__ == '__main__':
    bot.polling()
