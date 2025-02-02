import openai
import os

def chat_with_gpt(prompt, api_key):
    openai.api_key = api_key
    
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "system", "content": "You are a helpful assistant."},
                  {"role": "user", "content": prompt}]
    )
    
    return response["choices"][0]["message"]["content"]

if __name__ == "__main__":
    api_key = os.getenv("OPENAI_API_KEY")  # Defina sua chave de API como variável de ambiente
    
    if not api_key:
        api_key = input("Digite sua chave de API da OpenAI: ")
    
    while True:
        user_input = input("Você: ")
        if user_input.lower() in ["sair", "exit", "quit"]:
            break
        response = chat_with_gpt(user_input, api_key)
        print("Chatbot:", response)
