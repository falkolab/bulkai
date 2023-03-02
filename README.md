# bulkai

**bulkai** is a tool to generate AI images in bulk

## Features

**bulkai** works with the following AI image generators:

 - Midjourney
 - Bluewillow

**bulkai** automates the following tasks:

 - Send prompts to the AI
 - Upscale the generated images
 - Or crop the preview images if upscale is disabled
 - Optionally, generate variations of the generated images
 - Download the generated images
 - Create thumbnails
 - Generate a HTML album page with the generated images

## Installation

You can use the golang binary to install **bulkai**:

To install the cli:

```bash
go install github.com/igolaizola/bulkai/cmd/bulkai@latest
```

To install the GUI:

> The GUI is a work in progress and it may not work properly.

```bash
go install github.com/igolaizola/bulkai/cmd/bulkaigui@latest
```

Or you can download the binary from the [releases](https://github.com/igolaizola/bulkai/releases)

## Usage: command-line interface 

The binary you need to use is `bulkai`.

### 1. Create session (only for the first time)

You first need to create a session file with the discord credentials and other information retrieved from your browser.
**bulkai** needs this to:

 - Be able to login to Discord
 - Mimic the browser and avoid being detected as a bot

Use the `bulkai create-session` command to create the session file.
It will open a chrome window and you will need to login to Discord.

```bash
bulkai create-session
```

### 2. Configure settings

You can configure different settings.
See the parameters section to see all available options: [Parameters](#parameters)

Using a configuration file in YAML format:

```bash
bulkai generate --config bulkai.yaml
```

bulkai.yaml
```yaml
bot: midjourney
album: cute-animals
download: true
upscale: true
variation: false
thumbnail: true
suffix: " --ar 3:2"
prompt:
  - cute-animals-1.txt
  - cute-animals-2.txt
  - cute monkey dancing on a tree
```

### 2. Launch

Use the `bulkai generate` command to launch the generation.
Images will be downloaded to the album name in the output directory specified in the configuration file.
You will be able to see the progress in the console.
This task can take a long time depending on the number of images to generate.

```bash
bulkai generate
```

You can press `Ctrl+C` to stop the generation.
If you want to resume the generation, just press launch the command again using the same settings and album name.
Prompt field will be ignored and the prompts will be loaded from the album.

## Usage: graphical user interface

> The GUI is a work in progress and it may not work properly.

The binary you need to use is `bulkaigui`.

### 1. Create session (only for the first time)

You first need to create a session file with the discord credentials and other information retrieved from your browser.
**bulkai** needs this to:

 - Be able to login to Discord
 - Mimic the browser and avoid being detected as a bot

Go to the `Settings` tab and click on the `Create session` button.

### 2. Configure settings

On the `Settings` tab you can configure different settings.
This options will be saved in the configuration file.
See the parameters section to see all available options: [Parameters](#parameters)

On the `Main` tab you can set the name of the album and the prompts to use.
Each line will be processed as a different prompt.
You can also set the path to a prompt file instead.

### 3. Launch

Press the `Start` button to launch the generation.
Images will be downloaded to the album name in the output directory specified in the configuration file.
You will be able to see the progress in the window.
This task can take a long time depending on the number of images to generate.

You can use the `Stop` button to stop the generation.
If you want to resume the generation, just press the `Start` button again using the same settings and album name.
Prompt field will be ignored and the prompts will be loaded from the album.

## Parameters

Here is a list of all the parameters available to run the image generation.

 - `bot` (string): Name of the bot to use.
Available options are: `midjourney` and `bluewillow`. (required)
 - `download` (bool): Download the generated images. (default: `true`)
 - `upscale` (bool): Upscale the generated images. (default: `true`)
If you disable this the generation will be much faster.
It will directly use the preview images generated by the AI.
In midjourney for example, the preview images are 256x256.
 - `variation` (bool): Generate variations of the generated images. (default: `false`)
This will generate 4 extra variations of each prompt.
The generation will be much slower.
 - `thumbnail` (bool): Generate thumbnails of the generated images. (default: `true`)
This operation is done locally, it will improve the performance of the HTML page.
 - `suffix` (string): Suffix to add to all prompts. (optional)
 - `prefix` (string): Prefix to add to all prompts. (optional)
 - `prompt` (list): List of prompts to use. (required)
If you want include prompts from a file, just write the path to the file.
 - `album` (string): Name of the album. (optional, but recommended)
If unset a time based name will be used.
 - `output` (string): Path to the output directory. (default: `./output`)
 - `session` (string): Path to the session file. (default: `./session.json`)
 - `channel` (string): Name of the channel to use in the form `guild/channel`. (optional)
If unset the DM chat with the bot will be used.
 - `proxy` (string): Proxy to use in HTTP calls. (optional)
 - `concurrency` (int): How many prompts can be running at the same time. (optional)
If unset the maximum for the bot will be used.
 - `wait` (int): Time to wait between prompts. (optional)
There is already a rate limit implemented to avoid sending too many requests to discord.
 - `debug` (bool): Enable debug mode. (default: `false`)

## FAQ

### Do I need to generate a new session every time I want to use use **bulkai**?

No, you only need to generate a new session if you want to use a different account.

### Do I need to enable relaxed mode?

It is up to you to use relaxed or fast mode.
Just keep in mind that if you use fast mode with a lot of prompts, you may consume your quota very quickly.

### Can I use suffix settings of midjourney?

You must disable any suffix configurations in discord, such as `High quality` or `Style High`, or any suffixes configured with `/prefer`.
If you don't disable them, **bulkai** won't be able to retrieve generated images.

However, you can use the `suffix` parameter of **bulkai** to add a suffixes to all prompts.
For example, if you want to use the `High quality` setting, you can use `suffix: " --q 2"`.

## Disclaimer

The automation of User Discord accounts also known as self-bots is a violation of Discord Terms of Service & Community guidelines and will result in your account(s) being terminated.

The automation of Midjourney and Bluewillow accounts is also a violation of their Terms of Service and will result in your account(s) being terminated.

Read about Discord, Midjourney and Bluewillow Terms of Service and Community Guidelines

**bulkai** was written as a proof of concept and the code has been released for educational purposes only.
The authors are released of any liabilities which your usage may entail.

## Support

If you have found my code helpful, please give the repository a star ⭐

Additionally, if you would like to support my late-night coding efforts and the coffee that keeps me going, I would greatly appreciate a donation.

You can invite me for a coffee:

<a href="https://www.buymeacoffee.com/igolaizola">
    <img src="https://user-images.githubusercontent.com/11333576/221318625-736e63fe-489e-434e-b239-5c891cf5026a.png"/>
</a>

Donate to my PayPal:

[paypal.me/igolaizola](https://www.paypal.me/igolaizola)

Sponsor me on GitHub:

[github.com/sponsors/igolaizola](https://github.com/sponsors/igolaizola)

Or donate to any of my crypto addresses:

 - BTC `bc1qvuyrqwhml65adlu0j6l59mpfeez8ahdmm6t3ge`
 - ETH `0x960a7a9cdba245c106F729170693C0BaE8b2fdeD`
 - USDT (TRC20) `TD35PTZhsvWmR5gB12cVLtJwZtTv1nroDU`
 - USDC (BEP20) / BUSD (BEP20) `0x960a7a9cdba245c106F729170693C0BaE8b2fdeD`
 - Monero `41yc4R9d9iZMePe47VbfameDWASYrVcjoZJhJHFaK7DM3F2F41HmcygCrnLptS4hkiJARCwQcWbkW9k1z1xQtGSCAu3A7V4`

Thanks for your support!

## Resources

Some of the resources I used to create this project:

 - [jkvatne/gio-v](https://github.com/jkvatne/gio-v) to be able to implement the GUI in a quick and easy way.
 - [bwmarrin/discordgo](https://github.com/bwmarrin/discordgo) to retrieve events from Discord.
 - [Danny-Dasilva/CycleTLS](https://github.com/Danny-Dasilva/CycleTLS) to mimic the browser and avoid being detected as a bot.
