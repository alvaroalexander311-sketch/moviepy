from moviepy.editor import ColorClip, TextClip, CompositeVideoClip, concatenate_videoclips

clips = []
for text in ["¿Qué es la democracia hoy en México?",
             "La democracia es participación.",
             "Votar es una forma de participar.",
             "Infórmate y respeta.",
             "¡Tu voz cuenta!"]:
    bg = ColorClip(size=(720, 1280), color=(30, 60, 120), duration=3)
    
    # Agrega method='caption' para evitar problemas con ImageMagick
    txt = TextClip(text, fontsize=48, color='white', method='caption', size=(600, None))
    txt = txt.set_position('center').set_duration(3)
    
    clips.append(CompositeVideoClip([bg, txt]))

video = concatenate_videoclips(clips, method="compose")
out = "/mnt/data/video_democracia_tiktok.mp4"
video.write_videofile(out, fps=24, audio=False, verbose=False, logger=None)
print(out)
