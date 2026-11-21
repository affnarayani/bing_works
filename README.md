# bing_works

`bing_works` is an unofficial async API wrapper for Bing Image & Video Creator. Generate AI-powered images and videos from Bing's creation tools programmatically, with support for multiple models and aspect ratios.

> **Warning:** The `_U` auth cookie should be refreshed every 2-4 weeks for reliable functionality.

## Features

- Fully asynchronous — built on `curl_cffi` and `asyncio`
- Generate images using DALL-E, GPT-4O, and MAI1 models
- Generate videos from text prompts
- Custom aspect ratios: Square (1:1), Landscape (7:4), Portrait (4:7)
- Get up to 4 image URLs per request
- Flexible authentication via `_U` cookie or auto-fetch from browsers
- Enhanced prompts with AI-improved versions
- Async context manager support (`async with`)
- Custom exceptions for error handling

## Installation

```bash
pip install bing_works
```

## Quick Start

```python
import asyncio
from bing_works import BingArt

async def main():
    async with BingArt(auth_cookie_U='your_cookie_value') as bing:
        result = await bing.generate('sunset over mountains')
        print(result)

asyncio.run(main())
```

## Auto Cookie Detection

Let `bing_works` fetch the `_U` cookie automatically from your installed browsers:

```python
from bing_works import BingArt

bing = BingArt(auto=True)
```

Supported browsers: Chrome, Edge, Firefox, Brave, Opera, Vivaldi, Chromium.

## Models and Aspect Ratios

```python
import asyncio
from bing_works import BingArt, Model, Aspect

async def main():
    async with BingArt(auth_cookie_U='your_cookie_value') as bing:
        result = await bing.generate(
            'a futuristic cityscape',
            model=Model.GPT4O,
            aspect=Aspect.PORTRAIT
        )
        print(result)

asyncio.run(main())
```

**Models:** `Model.DALLE`, `Model.GPT4O`, `Model.MAI1`

**Aspects:** `Aspect.SQUARE`, `Aspect.LANDSCAPE`, `Aspect.PORTRAIT`

## Video Generation

```python
import asyncio
from bing_works import BingArt

async def main():
    async with BingArt(auth_cookie_U='your_cookie_value') as bing:
        result = await bing.generate(
            'a dancing robot in a futuristic city',
            content_type='video'
        )
        print(result)

asyncio.run(main())
```

## Exceptions

```python
from bing_works import BingArt, AuthCookieError, PromptRejectedError

try:
    result = await bing.generate('your prompt')
except AuthCookieError:
    print("Invalid or expired auth cookie")
except PromptRejectedError:
    print("Prompt rejected by content policy")
```

## Getting Your `_U` Cookie

1. Open [Bing Image Creator](https://www.bing.com/images/create) and sign in.
2. Press F12 to open Developer Tools.
3. Go to Application/Storage → Cookies → `https://www.bing.com`.
4. Copy the value of the `_U` cookie.

## Requirements

- Python >= 3.6
- `curl_cffi`
- `rookiepy`

## License

MIT License — see the LICENSE file for details.

## Disclaimer

This is an unofficial wrapper and is not affiliated with Microsoft or Bing. Use responsibly and in accordance with Bing's terms of service.
