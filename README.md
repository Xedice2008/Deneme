from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

# /start komandasına cavab
def start(update, context):
    update.message.reply_text("Salam! Mən musiqi botuyam. Sizə musiqi göndərə bilərəm.")

# Musiqi göndərmək üçün funksiya
def send_music(update, context):
    chat_id = update.message.chat_id
    context.bot.send_audio(chat_id=chat_id, audio=open('musiqi.mp3', 'rb'))

def main():
    TOKEN = '7890202816:AAG6M6k7gg7uFZuN39rn2PXx5JdL-T1jrKk'
    updater = Updater(TOKEN, use_context=True)

    dp = updater.dispatcher

    # /start komandasını idarə etmək üçün handler
    dp.add_handler(CommandHandler("start", start))

    # Musiqi göndərmək üçün mesaj handleri
    dp.add_handler(CommandHandler("music", send_music))

    # Botu işə salırıq
    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
