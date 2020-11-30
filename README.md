# codemonkey-hebrew-translations
Hebrew audio translation for codemonkey words.

Used for the chrome extension at https://github.com/noamraph/codemonkey-hebrew-translate.

Notes for me for recording:

I recorded using Audacity. Exported to FLAC (which is lossless). Uploaded to Auphonic. Settings: -16 dB LUFS, mono, enable noise reduction: auto. Downloaded FLAC.

In Audacity, I added a label for each word (select, and press ctrl-B and type the word). Then File->Export->Labels to `labels.txt`. Then, in python:

```
pip install pydub
```

```python
labels_s = open('labels.txt').read()
words = [(float(start_s), float(stop_s), word) for line in labels_s.split('\n') if line and line[0] != '\\' for start_s, stop_s, word in [line.split()]]
for start, stop, word in words:
    rec[start*1000:stop*1000].export('{}.mp3'.format(word))
```
