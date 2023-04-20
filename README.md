# poe-openai-proxy

A wrapper that lets you use the reverse-engineered Python library `poe-api` library as if it was the OpenAI API for ChatGPT. You can connect your favorite OpenAI API based apps to this proxy and enjoy the ChatGPT API for free!

[简体中文](README_zh.md)

## Installation

1. Clone this repository to your local machine:

```bash
git clone https://github.com/juzeon/poe-openai-proxy.git
cd poe-openai-proxy/
```

2. Install the python requirements for the `poe-api` library:

```bash
pip install -r requirements.txt
```

3. Edit the configuration file according to the instructions in the comments:

```bash
vim config.toml
```

config.toml:

```toml
# The port number for the proxy service. The proxied OpenAI API endpoint will be: http://localhost:3700/v1/chat/completions
port = 3700

# A list of poe tokens. You can get them from the cookies on poe.com, they look like this: p-b=fdasac5a1dfa6%3D%3D
tokens = ["fdasac5a1dfa6%3D%3D","d84ef53ad5f132sa%3D%3D"]

# The gateway url for the Python backend of poe-api. Don't change this unless you modify external/api.py
gateway = "http://127.0.0.1:5000"

```

4. Install dependencies from requirements.txt and start the Python backend for `poe-api`:

```bash
pip install -r requirements.txt
python external/api.py # Running on port 5000
```

5. Build and start the Go backend:

```bash
go build
chmod +x poe-openai-proxy
./poe-openai-proxy
```

## Usage

See [OpenAI Document](https://platform.openai.com/docs/api-reference/chat/create) for more details on how to use the ChatGPT API.

Just replace `https://api.openai.com/v1/chat/completions` in your code with `http://localhost:3700/v1/chat/completions` and you're good to go.

Supported parameters:

| Parameter | Note                                                         |
| --------- | ------------------------------------------------------------ |
| model     | It doesn't matter what you pass here, poe will always use `gpt-3.5-turbo`. |
| messages  | You can use this as in the official API, except for `name`.            |
| stream    | You can use this as in the official API.                               |

Other parameters will be ignored.