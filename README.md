# bot.py

import os
import random
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, ContextTypes, filters

BOT_TOKEN = os.environ.get("8488268004:AAFnyWrx9D2SHUaPkUDfKq96XEJTVIp3bNY")

anime_replies = [
    "हाय! मैं तुम्हारा Anime दोस्त हूँ 🌸",
    "ओहो! क्या बात है 😄",
    "तुम्हें कौन सा anime पसंद है?",
    "Naruto या Demon Slayer?",
    "मैं हमेशा online हूँ तुम्हारे लिए ✨",
    "Sugoi! बहुत अच्छा!",
    "Senpai, और बताओ 😅"
]

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Kon'nichiwa 🌸\nमैं एक Anime-style Hindi chatbot हूँ!\nमुझसे कुछ भी बात करो."
    )

async def chat(update: Update, context: ContextTypes.DEFAULT_TYPE):
    text = update.message.text.lower()

    if "hi" in text or "hello" in text:
        reply = "हाय हाय 🌸 कैसे हो?"
    elif "anime" in text:
        reply = "Anime तो मेरी दुनिया है ✨"
    elif "bye" in text:
        reply = "माता ने~ फिर मिलेंगे 🌙"
    else:
        reply = random.choice(anime_replies)

    await update.message.reply_text(reply)

if __name__ == "__main__":
    app = ApplicationBuilder().token(8488268004:AAFnyWrx9D2SHUaPkUDfKq96XEJTVIp3bNY).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, chat))

    print("Bot is running...")
    app.run_polling()
