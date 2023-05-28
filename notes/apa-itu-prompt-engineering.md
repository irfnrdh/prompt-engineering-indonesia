# Apa itu Prompt Engineering?

Prompt engineering adalah proses mengoptimalkan dan memodifikasi prompt yang digunakan saat berinteraksi dengan model bahasa seperti ChatGPT. Dalam prompt engineering, tujuannya adalah merancang pertanyaan atau instruksi yang spesifik dan jelas agar memperoleh hasil yang diinginkan dari model.

Prompt engineering melibatkan pemahaman yang mendalam tentang cara kerja model bahasa yang digunakan dan kemampuannya. Dengan memahami perilaku model, pengguna dapat memodifikasi prompt mereka untuk menghasilkan jawaban yang lebih akurat dan relevan.

# Mulai Praktek

```py
import openai
import os

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv())

openai.api_key  = os.getenv('OPEN_AI_API')

def get_completion(prompt, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": prompt}]
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=0, # this is the degree of randomness of the model's output
    )
    return response.choices[0].message["content"]
```

## Prinsip pada Prompting
- **Prinsip 1: Tulis dengan jelas dan spesifik setiap intruksi**
- **Prinsip 2: Berikan model waktu untuk "berfikir" memahami intruksi**

### Taktik

#### Taktik 1: Use delimiters to clearly indicate distinct parts of the input

```py
text = f"""
Anda sebaiknya mengekspresikan apa yang Anda inginkan agar model melakukan dengan \
memberikan instruksi yang sejelas dan \
spesifik mungkin. \
Instruksi itu akan membimbing model menuju output yang diinginkan, \
dan mengurangi kemungkinan menerima tanggapan yang tidak relevan \
atau salah. Jangan bingung antara menulis prompt yang jelas dengan menulis prompt yang singkat. \
Dalam banyak kasus, prompt yang lebih panjang memberikan lebih banyak kejelasan \
dan konteks bagi model, yang dapat menghasilkan \
output yang lebih detail dan relevan.
"""

prompt = f"""
Summarize the text delimited by triple backticks \ 
into a single sentence.
```{text}```
"""

response = get_completion(prompt)
print(response)
```
