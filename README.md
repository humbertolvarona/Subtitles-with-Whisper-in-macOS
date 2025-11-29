# Manual for Extracting Subtitles with Whisper on macOS

## 1. Environment Preparation

To generate SRT subtitles from a video or audio file, Whisper can be used from the macOS command line. This manual describes the entire process step by step.

## 2. Verify or Install Python 3

Make sure you have Python 3 installed. Check it in Terminal:

```bash
python3 --version
```

If it is not installed or you want the latest version, download it from:
[https://www.python.org/downloads/macos/](https://www.python.org/downloads/macos/)

## 3. Install Whisper

Install Whisper using pip:

```bash
pip install -U openai-whisper
```

## 4. Install or Repair Python SSL Certificates (macOS)

On macOS, Python installed from python.org includes a script to fix SSL certificates.

1. Open Finder.
2. Navigate to:

   ```
   /Applications/Python 3.10
   ```
3. Run:

   ```
   Install Certificates.command
   ```

This reconfigures the system certificates to allow secure HTTPS downloads.

## 5. Extract Audio from Video (Optional)

If you want to process an MP4 video, you may extract the audio:

```bash
ffmpeg -i video.mp4 -vn -acodec pcm_s16le -ar 16000 -ac 1 audio.wav
```

You can also transcribe the MP4 directly without extracting audio.

## 6. Generate SRT Subtitles with Whisper

Run the following command:

```bash
whisper audio.wav --language es --task transcribe --model medium --output_format srt
```

Whisper will download the selected model (such as "medium") and generate an `.srt` file.

## 7. Location of the Generated SRT File

Whisper will create a file similar to:

```
audio.srt
```

This file will appear in the same folder where you executed the command.

## 8. Additional Useful Options

* List all available models:

  ```bash
  whisper --help
  ```
* Use a smaller model if you have limited memory:

  ```bash
  --model small
  ```
* Increase accuracy by using a larger model:

  ```bash
  --model large
  ```

## 9. Troubleshooting

### SSL Error: CERTIFICATE_VERIFY_FAILED

If you encounter:

```
ssl.SSLCertVerificationError
```

Recommended actions:

1. Run `Install Certificates.command`.
2. Alternatively, use `certifi`:

   ```bash
   pip install certifi
   export SSL_CERT_FILE=$(python3 -c "import certifi; print(certifi.where())")
   ```

### "no such file or directory" Error When Accessing Python 3.10

Verify that the folder exists:

```bash
ls /Applications
```

The folder should be named:

```
Python 3.10
```

with the exact spacing and version.

## 10. Editing and Reviewing the SRT File

Once the subtitle file is generated:

* Edit it with your preferred text editor (VS Code, Sublime, Notepad++).
* Verify numbering, timestamps, and blank lines.

