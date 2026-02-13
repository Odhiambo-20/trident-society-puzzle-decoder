# Ultimate Decoder

`ultimate_decoder.py` is a puzzle-decoding script that analyzes provided clue artifacts and outputs six target fields:

- Timer
- Location
- Phone Number
- Email
- Web Address
- Password

The project combines text extraction, signal-derived numeric decoding, and rule-based validation to produce structured final outputs.

## Project Files

- `ultimate_decoder.py` - main decoder script
- `download.mp3_converted.wav` - audio source used for numeric/phone decoding
- `TS Clues-7.pdf` - clue document used for text-derived fields
- `download.mp3.mpeg` - original audio file (pre-conversion)

## How It Works

The decoder uses multiple methods and merges the results:

1. PDF clue extraction
- Runs `pdftotext` on `TS Clues-7.pdf`
- Extracts URL-like, schedule-like, and phrase-like evidence from the text

2. Morse verification
- Uses a standard Morse map for symbol/text conversion
- Verifies the clue’s decoded Morse word via round-trip conversion

3. Audio-to-phone decoding
- Reads WAV samples from `download.mp3_converted.wav`
- Splits the signal into fixed windows and computes peak amplitude per window
- Converts peaks to digits with modulo mapping (`peak % 10`)
- Scans 10-digit windows and applies NANP validity checks
- Selects a valid US-style phone candidate deterministically

4. Field derivation
- Timer from deadline wording in clues
- Password from repeated key phrase normalization
- Email and location from textual clue context
- Web address from extracted link evidence

## Requirements

- Python 3.9+
- `pdftotext` available on system path (Poppler)

No external Python packages are required.

## Usage

From the project directory:

```bash
python3 ultimate_decoder.py
```

## Example Output (Shape)

```text
[FINAL OUTPUT]
TIMER: ...
LOCATION: ...
PHONE NUMBER: ...
EMAIL: ...
WEB ADDRESS: ...
PASSWORD: ...
```

## Notes

- Output quality depends on the exact clue files and audio content in this workspace.
- The phone number is filtered through NANP formatting/validity rules.
- The decoder is deterministic for the same inputs.

## Disclaimer

This project is designed for puzzle/CTF-style decoding workflows and should not be used as a source of verified real-world contact data.
