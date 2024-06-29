# Mass Messages Script

# SendScript in WhatsApp Web

This JavaScript script is designed to automate sending multiple messages via WhatsApp Web. It can be useful for sending warning messages or repetitive notifications to a specific contact.

## Description

The script divides the text into lines, writes each line in the WhatsApp text box, and sends each message with a small delay between each one to avoid being detected as a bot.

## Use

### 1. Open WhatsApp Web
Go to [WhatsApp Web](https://web.whatsapp.com/) and log in by scanning the QR code with your WhatsApp application on your mobile.

### 2. Select a Conversation
Open the conversation to which you want to send messages.

### 3. Open the Browser Console
In your browser (Chrome, Firefox, etc.), open the developer console. This is usually done with `Ctrl+Shift+I` (or `Cmd+Option+I` on Mac) and then selecting the "Console" tab.

### 4. Paste and Run the Script
Copy the script below and paste it into the browser console, then press `Enter`.

> ⚠️ **Important Notice:**  
> Our recent update in Google Chrome is preventing any script from sneaking into the console.  
> To fix this issue, the developer console expects to receive a confirmation via a text message typed into the console: "allow-scripts".  
> After this, it will be allowed to cast and continue with the execution of the script.

```javascript
async function enviarScript(scriptText){
    const lines = scriptText.split(/[\n\t]+/).map(line => line.trim()).filter(line => line);
    main = document.querySelector("#main"),
    textarea = main.querySelector(`div[contenteditable ="true"]`)

    if(!textarea) throw new Error("No hay una conversacion abierta")

    for(const line of lines){
        console.log(line)
    
        textarea.focus();
        document.execCommand('insertText', false, line);
        textarea.dispatchEvent(new Event('change', {bubbles: true}));

        setTimeout(() =>{
            (main.querySelector(`[data-testid="send"]`) || main.querySelector(`[data-icon="send"]`)).click();
        }, 100);
        if(lines.indexOf(line) !== lines.length - 1) await new Promise(resolve => setTimeout(resolve, 250));
    }

    return lines.length

}

enviarScript(`
*mensaje a enviar*
`).then(e => console.log(`Código finalizado, ${e} mensagens enviadas`)).catch(console.error)
```

---

This markdown provides a clear and organized way to present the instructions for using the script.