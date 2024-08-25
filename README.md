const qrcode = require('qrcode-terminal');
const { Client, LocalAuth } = require('whatsapp-web.js');

// إنشاء عميل بوت واتساب
const client = new Client({
    authStrategy: new LocalAuth()
});

// إظهار QR code للمصادقة
client.on('qr', (qr) => {
    qrcode.generate(qr, { small: true });
});

// رسالة عند جاهزية البوت
client.on('ready', () => {
    console.log('بوت واتساب جاهز!');
});

// التعامل مع الرسائل
client.on('message', message => {
    if(message.body.toLowerCase() === 'مرحبا') {
        message.reply('مرحبًا! كيف يمكنني مساعدتك اليوم؟ 😊');
    } else if (message.body.toLowerCase().includes('كيف حالك؟')) {
        message.reply('أنا بخير، شكراً لسؤالك! وأنت؟');
    } else {
        message.reply('أنا هنا لأساعدك! كيف يمكنني مساعدتك اليوم؟');
    }
});

// بدء العميل
client.initialize();