# Service_Agent
from gtts import gTTS
from IPython.display import Audio, display
from pydub import AudioSegment
import os

# Define the names to convert to speech
names = ["Harika", "Mahesh", "Amulya", "Barath", "Raveena"]

# Generate audio for each name and create voice variations
for name in names:
    # Generate audio using gTTS
    text = f"Hello! Thank you for contacting HDFC Bank. This is {name}.How may I assist you today?"  # Updated text
    tts = gTTS(text=text, lang='en', tld='co.in')
    filename = f"{name}_audio.mp3"
    tts.save(filename)
    print(f"Generated speech and saved as {filename}")

    # Check if the audio file exists
    if os.path.exists(filename):
        # Load the audio file using pydub
        audio = AudioSegment.from_file(filename)

        # Define pitch/speed settings for simulating different voices
        voice_variations = {
            f'{name} - Female Voice 1': audio.speedup(playback_speed=1.1),  # Slightly higher pitch
           
            f'{name} - Male Voice 1': audio.speedup(playback_speed=1.3),    # Slightly lower pitch
          
        }

        # Save the variations and display audio
        for voice_name, modified_audio in voice_variations.items():
            modified_filename = f"{voice_name}.mp3"
            modified_audio.export(modified_filename, format="mp3")
            print(f"Generated {voice_name} and saved as {modified_filename}")
            display(Audio(modified_filename))  # Play the audio in the notebook
    else:
        print(f"Audio file {filename} does not exist.")
