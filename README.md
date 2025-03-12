import speech_recognition as sr
import pyttsx3

class Jarvis:
    def __init__(self):
        self.recognizer = sr.Recognizer()
        self.engine = pyttsx3.init()
        self.engine.setProperty('rate', 150)  # Speed of speech
        self.engine.setProperty('volume', 1)  # Volume level (0.0 to 1.0)

    def speak(self, text):
        self.engine.say(text)
        self.engine.runAndWait()

    def listen(self):
        with sr.Microphone() as source:
            print("Listening...")
            audio = self.recognizer.listen(source)

            try:
                print("Recognizing...")
                query = self.recognizer.recognize_google(audio, language='en-US')
                print(f"User said: {query}\n")
                return query
            except Exception as e:
                print("Sorry, I did not catch that. Could you please repeat?")
                return None

    def run(self):
        self.speak("Hello, I am J.A.R.V.I.S. How can I assist you today?")
        while True:
            query = self.listen()

            if query:
                if "exit" in query.lower() or "quit" in query.lower():
                    self.speak("Goodbye!")
                    break
                elif "hello" in query.lower():
                    self.speak("Hello! How can I help you today?")
                elif "your name" in query.lower():
                    self.speak("I am J.A.R.V.I.S., your AI assistant.")
                else:
                    self.speak("I'm sorry, I don't understand that command.")

if __name__ == "__main__":
    assistant = Jarvis()
    assistant.run()
