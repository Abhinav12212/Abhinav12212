from music21 import stream, note, chord, tempo, meter, instrument

# Create a stream for the composition
score = stream.Score()

# Add tempo and meter
score.append(tempo.MetronomeMark(number=70))
score.append(meter.TimeSignature('4/4'))

# Define instruments
flute = instrument.Flute()
strings = instrument.StringQuartet()
theremin = instrument.ElectricGuitar()  # For a theremin-like sound
brass = instrument.Horn()

# Create individual parts
flute_part = stream.Part()
flute_part.append(flute)

string_part = stream.Part()
string_part.append(strings)

theremin_part = stream.Part()
theremin_part.append(theremin)

brass_part = stream.Part()
brass_part.append(brass)

# Introduction: Strings and Flute
# Strings: Tremolo D minor (D-F)
for _ in range(4):
    string_chord = chord.Chord([note.Note('D4'), note.Note('F4')], quarterLength=4)
    string_part.append(string_chord)

# Flute melody (introduction)
flute_melody = [note.Note(p, quarterLength=1) for p in ['D5', 'F5', 'G5', 'B4', 'A4', 'F#4', 'A4', 'G4', 'D4']]
flute_part.append(flute_melody)

# Main Theme: Brass and Strings (G-B-Em-C progression)
main_chords = [
    chord.Chord(['G4', 'B4', 'D5'], quarterLength=4),
    chord.Chord(['B4', 'D5', 'F#5'], quarterLength=4),
    chord.Chord(['E4', 'G4', 'B4'], quarterLength=4),
    chord.Chord(['C4', 'E4', 'G4'], quarterLength=4)
]
for ch in main_chords:
    string_part.append(ch)
    brass_part.append(ch)

# Theremin soaring melody
theremin_melody = [note.Note(p, quarterLength=2) for p in ['G5', 'B5', 'F#5', 'D5', 'A5', 'C6', 'G6']]
theremin_part.append(theremin_melody)

# Exploration: Pizzicato in Strings
pizzicato_notes = [note.Note(p, quarterLength=1) for p in ['D4', 'E4', 'G4', 'D4', 'E4', 'A4']]
string_part.append(pizzicato_notes)

# Climax: F major chords
climax_chords = [
    chord.Chord(['F4', 'A4', 'C5'], quarterLength=4),
    chord.Chord(['G4', 'B4', 'D5'], quarterLength=4)
]
for ch in climax_chords:
    string_part.append(ch)
    brass_part.append(ch)

# Outro: Tremolo on D minor (back to D and F)
for _ in range(4):
    string_chord = chord.Chord([note.Note('D4'), note.Note('F4')], quarterLength=4)
    string_part.append(string_chord)

# Combine parts into the score
score.append(flute_part)
score.append(string_part)
score.append(theremin_part)
score.append(brass_part)

# Save the score as MusicXML
score.write('musicxml', fp='planet_unseen_discovery.xml')
