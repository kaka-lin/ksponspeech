# KsponSpeech
#### Pre-processing KsponSpeech corpus provided by AI Hub

It's been a while since [KsponSpeech](https://www.mdpi.com/2076-3417/10/19/6936) was released, but it's hard to compare performance because there's no established preprocessing method. So we're revealing the pre-processing method we used in the [KoSpeech](https://github.com/sooftware/KoSpeech) project. This project provides processing in characters, subwords, and grapheme units.

## Intro

`KsponSpeech-preprocess` is repository for pre-processing `KsponSpeech corpus` provided by AI Hub.
**KsponSpeech corpus** is a **1000h** Korean speech data corpus provided by [AI Hub](http://www.aihub.or.kr/) in Korea.
Anyone can download this dataset just by applying. The transcription rules can see [here](http://www.aihub.or.kr/sites/default/files/2019-12/%ED%95%9C%EA%B5%AD%EC%96%B4%20%EC%9D%8C%EC%84%B1%20%EC%A0%84%EC%82%AC%EA%B7%9C%EC%B9%99%20v1.0.pdf).

You can pre-process in various output-units, such as ***character, subword, grapheme***
We will explain the details in the **Output-Unit** part below.

## Prerequisites

```bash
$ pip install -r requirements.txt
```
* Pandas: `pip install pandas` (Refer [here](https://github.com/pandas-dev/pandas) for problem installing Pandas)
* Sentencepiece: `pip install sentencepiece` (Refer [here](https://github.com/google/sentencepiece) for problem installing Sentencepiece)

## Usage

1. Copy `run.example` to `run.sh`, then configure your options in `run.sh`.

    ```bash
    DATASET_PATH="SET_YOUR_DATASET_PATH"     # path to kspon speech dataset
    VOCAB_DEST="SET_LABELS_DESTINATION"
    SAVE_PATH="SET_DATASET_DESTINATION"      # path to save preprocessed dataset
    OUTPUT_UNIT="character"                  # you can set character / subword / grapheme
    PREPROCESS_MODE="phonetic"               # phonetic : 칠 십 퍼센트,  spelling : 70%
    VOCAB_SIZE=5000                          # if you use subword output unit, set vocab size
    ```

2. Run `run.sh`

    ```shell
    $ ./run.sh
    ```

3. Leave the computer running for hours.

* Results : transcripts.txt (default: `data/transcripts.txt`)

    ```bash
    KsponSpeech_01/KsponSpeech_0001/KsponSpeech_000001.pcm  아 몬 소리야 그건 또.   8 3 731 3 174 33 27 3 5 101 3 127 4
    ...
    ...
    KsponSpeech_05/KsponSpeech_0623/KsponSpeech_622545.pcm  너 뭐 강남 자주 가?     51 3 42 3 243 197 3 47 77 3 9 15
    ```

## Preprocess

You can choose between phonetic transcription and spelling transcription to preprocess.

* Raw data

    ```bash
    b/ (70%)/(칠 십 퍼센트) 확률이라니 아/ (뭐+ 뭔)/(모+ 몬) 소리야 진짜 (100%)(백 프로)가 왜 안돼? n/
    ```

* Delete noise labels, such as b/, n/, / ..

    ```bash
    (70%)/(칠 십 퍼센트) 확률이라니 아/ (뭐+ 뭔)/(모+ 몬) 소리야 진짜 (100%)(백 프로)가 왜 안돼?
    ```

* Delete labels such as '/', '*', '+', etc. (used for interjection representation)

    ```bash
    (70%)/(칠 십 퍼센트) 확률이라니 아 (뭐 뭔)/(모 몬) 소리야 진짜 (100%)(백 프로)가 왜 안돼?
    ```

* Option1 : phonetic transcript

    ```bash
    칠 십 퍼센트 확률이라니 아 모 몬 소리야 진짜 백 프로가 왜 안돼?
    ```

* Option2 : spelling transcript

    ```bash
    70% 확률이라니 아 뭐 뭔 소리야 진짜 100%가 왜 안돼?
    ```

## Output-Unit

This project provides processing in characters, subwords, and grapheme units.

* Character-Unit

    ```bash
    아 모 몬 소리야 칠 십 퍼센트 확률이라니
    ```

* Subword-Unit

    ```bash
    ▁아 ▁모 ▁ 몬 ▁소리 야 ▁ 칠 ▁ 십 ▁퍼 센트 ▁확 률 이라 니
    ```

* Grapheme-Unit

    ```bash
    ㅇㅏ ㅁㅗ ㅁㅗㄴ ㅅㅗㄹㅣㅇㅑ ㅊㅣㄹ ㅅㅣㅂ ㅍㅓㅅㅔㄴㅌㅡ ㅎㅘㄱㄹㅠㄹㅇㅣㄹㅏㄴㅣ
    ```

## Conversion to Numeric id

* transcript

    ```bash
    아 모 몬 소리야 칠 십 퍼센트 확률이라니
    ```

* conversion

    ```bash
    7 3 106 3 730 3 173 32 26 3 319 3 120 3 490 552 157 3 315 747 5 33 22
    ```

## Troubleshoots and Contributing

If you have any questions, bug reports, and feature requests, please [open an issue](https://github.com/kaka-lin/ksponspeech/issues) on Github.

I appreciate any kind of feedback or contribution.  Feel free to proceed with small issues like bug fixes, documentation improvement.  For major contributions and new features, please discuss with the collaborators in corresponding issues.

## Reference

* [Sentencepiece](https://github.com/google/sentencepiece)

## Author
* [Soohwan Kim](https://github.com/sooftware), [Seyoung Bae](https://github.com/triplet02),  [Cheolhwang Won](https://github.com/wch18735), [Soyoung Cho](https://github.com/SoYoungCho), [Jeongwon Kwak](https://github.com/jeongwonkwak)
* Contacts: sh951011@gmail.com
