- 👋 Hi, I’m @Barankral1
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Barankral1/Barankral1 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import openai
from moviepy.editor import TextClip, concatenate_videoclips

# GPT API ile script oluşturma
def generate_script(prompt, api_key):
    openai.api_key = api_key
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    return response['choices'][0]['message']['content']

# Basit bir video oluşturma
def create_video(script, output_file):
    clips = []
    for i, line in enumerate(script.split('. ')):
        text_clip = TextClip(line, fontsize=24, color='white', size=(1280, 720), bg_color='black', duration=5)
        clips.append(text_clip)
    final_video = concatenate_videoclips(clips)
    final_video.write_videofile(output_file, fps=24)

# Kullanıcıdan prompt alma ve script oluşturma
api_key = "API_KEYİNİZ"
prompt = input("Video promptunu girin: ")
script = generate_script(prompt, api_key)

# Script'i kullanarak video oluşturma
output_file = "output.mp4"
create_video(script, output_file)
print(f"{output_file} dosyası oluşturuldu!")
