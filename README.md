python-telegram-bot
flask
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters

import os

# קבלת הטוקן מהסביבה (שמור אותו ב-Railway תחת Environment Variables)
TOKEN = os.getenv("BOT_TOKEN")

# יצירת אובייקט הבוט
app = Application.builder().token(TOKEN).build()

# פקודה /start
async def start(update: Update, context):
    await update.message.reply_text("שלום! אני בוט חנות החטיפים 🍫 איך אפשר לעזור לך?")

# תגובה לכל הודעה שנשלחת לבוט
async def handle_message(update: Update, context):
    text = update.message.text
    response = f"הודעה שקיבלתי: {text}"
    await update.message.reply_text(response)

# חיבור הפקודות לבוט
app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

# הרצת הבוט
if __name__ == "__main__":
    print("הבוט פועל...")
    app.run_polling()
