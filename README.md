# Codesofttask2-AI
import re

class RuleBasedChatbot:
    def __init__(self):
        self.responses = {
            r"(hello|hi|hey)\b": "Hello! How can I assist you today?",
            r"how are you\b": "I'm just a chatbot, but I'm here to help!",
            r"bye\b": "Goodbye! Have a great day!",
            r"(what is|tell me about) (\w+)\b": self.topic_info,
            "default": "I'm sorry, I don't understand. Can you please rephrase?"
        }
        
    def topic_info(self, match):
        topic = match.group(2)
        if topic == "chatbots":
            return "Chatbots are computer programs designed to simulate human conversation. They use various techniques, including rule-based and machine learning approaches."
        elif topic == "ai":
            return "Artificial Intelligence (AI) refers to the simulation of human intelligence in computers. It involves tasks such as problem solving, learning, and decision making."
        else:
            return f"I'm not sure about {topic}."
        
    def get_response(self, user_input):
        user_input = user_input.lower()
        for pattern, response_func in self.responses.items():
            match = re.search(pattern, user_input)
            if match:
                if callable(response_func):
                    return response_func(match)
                else:
                    return response_func
        return self.responses["default"]

# Create an instance of the chatbot
chatbot = RuleBasedChatbot()

# Interaction loop
print("Rule-Based Chatbot: Hello! Type 'bye' to exit.")
while True:
    user_input = input("You: ")
    if user_input.lower() == "bye":
        print("Rule-Based Chatbot: Goodbye!")
        break
    response = chatbot.get_response(user_input)
    print("Rule-Based Chatbot:", response)

