# Issue repro repository

## Foreword

The present repository contains the repro for an issue with Adaptive Cards regex validation in Bot Framework.

## Steps to get a repro

### Requirements

* [.NET 6](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)
* [Bot Framework emulator](https://github.com/Microsoft/BotFramework-Emulator/releases/tag/v4.14.1) _to run the tests_

### Setup

* Clone or download this Github folder
* Using your favourite IDE (Visual Studio or IntelliJ) or with the dotnet CLI `dotnet run` run the project from the SimpleBot folder
* Open the Bot Framework emulator and set `http://localhost:3978/api/messages` as the Bot URL.

## Tests

### Context

We are looking to send an adaptive card with a Regex validation for a phone number.

Regex:
```
^\\(?([0-9]{3})\\)?[-. ]?([0-9]{3})[-. ]?([0-9 ]{4})\\ ?\\.?$
```

* The Regex is valid (you can verify on https://regex101.com/) and accepts input such as `1234567890`, `123 456 8790`
* The adaptive card is valid (you can verify on https://adaptivecards.io/designer/ by setting the target version to 1.3, and then testing inputs in Preview mode),

### Issue

When receiving the greetings from the bot it triggers an error:
```
SimpleBot.en-us.lg:Bad JSON escape sequence: \(. Path 'body[1].regex', line 17, position 19. [SendActivity_Greeting]  Error occurred when evaluating expression. [__temp__2e107cdbb4794f199d2deef102998b02]  Error occurred when evaluating expression.,
SimpleBot.en-us.lg:Bad JSON escape sequence: \(. Path 'body[1].regex', line 17, position 19. [SendActivity_Greeting]  Error occurred when evaluating expression. [__temp__8834b940e025474386f4dc596bbaa782]  Error occurred when evaluating expression.
```

The expectation was to get an adaptive card that has an input validation.
