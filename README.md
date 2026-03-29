# edge-tts

`edge-tts` 是一个 Python 模块，允许你在 Python 代码或通过提供的 `edge-tts` / `edge-playback` 命令行工具中使用 Microsoft Edge 的在线文本转语音服务。无需安装 Microsoft Edge、Windows 或 API 密钥。

## 安装

使用以下命令安装：

    $ pip install edge-tts

如果你只需要使用 `edge-tts` 和 `edge-playback` 命令行工具，建议使用 `pipx`：

    $ pipx install edge-tts

## 用法

### 基本用法

使用 `edge-tts` 命令，只需运行以下命令：

    $ edge-tts --text "Hello, world!" --write-media hello.mp3 --write-subtitles hello.srt

如果你想立即播放语音并显示字幕，可以使用 `edge-playback` 命令：

    $ edge-playback --text "Hello, world!"

注意：除 Windows 系统外，`edge-playback` 需要安装 [`mpv` 命令行播放器](https://mpv.io/)。

所有 `edge-tts` 的命令选项都可以用于 `edge-playback`，但 `--write-media`、`--write-subtitles` 和 `--list-voices` 选项除外。

### 更改语音

你可以使用 `--voice` 选项来更改文本转语音服务所使用的语音。`--list-voices` 选项可以列出所有可用的语音。

    $ edge-tts --list-voices
    Name                               Gender    ContentCategories      VoicePersonalities
    ---------------------------------  --------  ---------------------  --------------------------------------
    af-ZA-AdriNeural                   Female    General                Friendly, Positive
    af-ZA-WillemNeural                 Male      General                Friendly, Positive
    am-ET-AmehaNeural                  Male      General                Friendly, Positive
    am-ET-MekdesNeural                 Female    General                Friendly, Positive
    ar-AE-FatimaNeural                 Female    General                Friendly, Positive
    ar-AE-HamdanNeural                 Male      General                Friendly, Positive
    ar-BH-AliNeural                    Male      General                Friendly, Positive
    ar-BH-LailaNeural                  Female    General                Friendly, Positive
    ar-DZ-AminaNeural                  Female    General                Friendly, Positive
    ar-DZ-IsmaelNeural                 Male      General                Friendly, Positive
    ar-EG-SalmaNeural                  Female    General                Friendly, Positive
    ...

    $ edge-tts --voice ar-EG-SalmaNeural --text "مرحبا كيف حالك؟" --write-media hello_in_arabic.mp3 --write-subtitles hello_in_arabic.srt

### 自定义 SSML

自定义 SSML 支持已被移除，因为 Microsoft 会阻止使用任何非 Microsoft Edge 自身生成的 SSML。这意味着所有需要自定义 SSML 的场景都无法支持，因为该服务仅允许一个 `<voice>` 标签内包含一个 `<prosody>` 标签。`<prosody>` 标签中可用的自定义选项已全部在本库或命令行中提供。

### 调整语速、音量和音高

你可以使用 `--rate`、`--volume` 和 `--pitch` 选项来调整生成语音的语速、音量和音高。使用负值时，需要写成 `--[选项]=-50%` 而非 `--[选项] -50%`，以避免该值被误认为命令行选项。

    $ edge-tts --rate=-50% --text "Hello, world!" --write-media hello_with_rate_lowered.mp3 --write-subtitles hello_with_rate_lowered.srt
    $ edge-tts --volume=-50% --text "Hello, world!" --write-media hello_with_volume_lowered.mp3 --write-subtitles hello_with_volume_lowered.srt
    $ edge-tts --pitch=-50Hz --text "Hello, world!" --write-media hello_with_pitch_lowered.mp3 --write-subtitles hello_with_pitch_lowered.srt

## Python 模块

你可以直接在 Python 代码中使用 `edge-tts` 模块。项目自带的示例包括：

* [示例代码](https://github.com/rany2/edge-tts/tree/main/examples)
* [工具模块](https://github.com/rany2/edge-tts/blob/main/src/edge_tts/util.py)

其他使用了 `edge-tts` 模块的项目包括：

* [hass-edge-tts](https://github.com/hasscc/hass-edge-tts/blob/main/custom_components/edge_tts/tts.py)
* [Podcastfy](https://github.com/souzatharsis/podcastfy/blob/main/podcastfy/tts/providers/edge.py)
* [tts-samples](https://github.com/yaph/tts-samples/blob/main/bin/create_sound_samples.py) - 一组 [mp3 语音样本](https://github.com/yaph/tts-samples/tree/main/mp3)合集，方便你为项目挑选合适的语音。
