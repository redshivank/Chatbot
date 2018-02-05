# Chatbot
const Readline = require('readline');
const Chalk = require('chalk');
const RiveScript = require('rivescript');

const bot = new RiveScript()
const rl = Readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

//load our training data
bot.loadFile('./training_data.rive', function() {
   // console.log("read sucess")
   bot.sortReplies();
   ask();
}, function(error){
    console.log("Error reading file: " + error);
})


function ask () {
    rl.question('You: ', (message) => {
        if(message == 'bye')process.exit();
        var reply = bot.reply('local-user', message);
        console.log(Chalk.red('Bot: ' + reply));
        ask();
    });
}
