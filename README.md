# M3M Telegram Plugin

Telegram Bot API plugin for [M3M](https://github.com/levskiy0/m3m) runtime.

## Installation

```bash
# Clone into m3m plugins directory
cd /path/to/m3m/plugins
git clone git@github.com:levskiy0/m3m-telegram.git

# Build plugin
cd m3m-telegram
go build -buildmode=plugin -o ../telegram.so
```

## Usage

```javascript
const BOT_TOKEN = $env.get("TELEGRAM_BOT_TOKEN");

$telegram.startBot(BOT_TOKEN, (bot) => {
    bot.handle("/start", (ctx) => {
        ctx.reply("Hello!");
    });

    bot.handleDefault((ctx) => {
        if (!ctx.update.message) return;
        ctx.reply(`You said: ${ctx.update.message.text}`);
    });
});
```

## API

### $telegram

- `startBot(token, callback)` - Start a new bot
- `stopBot(token)` - Stop a bot by token
- `stopAll()` - Stop all bots

### Bot Instance

**Handlers:**
- `handle(pattern, handler)` - Register command/text handler
- `handleCallback(data, handler)` - Register callback query handler
- `handleDefault(handler)` - Register default handler

**Sending:**
- `sendMessage(chatId, text, options?)` - Send text message
- `sendPhoto(chatId, photo, options?)` - Send photo
- `sendDocument(chatId, doc, options?)` - Send document
- `sendSticker(chatId, sticker)` - Send sticker
- `sendVideo(chatId, video, options?)` - Send video
- `sendAudio(chatId, audio, options?)` - Send audio
- `sendVoice(chatId, voice, options?)` - Send voice

**Editing:**
- `editMessage(chatId, messageId, text, options?)` - Edit message
- `editMessageMedia(chatId, messageId, photo, options?)` - Edit media
- `deleteMessage(chatId, messageId)` - Delete message

**Context methods:**
- `ctx.reply(text)` - Reply to message
- `ctx.replyPhoto(photo, caption?)` - Reply with photo
- `ctx.replyWithKeyboard(text, keyboard, options?)` - Reply with keyboard
- `ctx.replyWithInlineKeyboard(text, keyboard)` - Reply with inline keyboard
- `ctx.answerCallback(text?, showAlert?)` - Answer callback query
- `ctx.editMessage(text, options?)` - Edit current message
- `ctx.deleteMessage()` - Delete current message

## Build

```bash
go build -buildmode=plugin -o telegram.so
```

## License

MIT
