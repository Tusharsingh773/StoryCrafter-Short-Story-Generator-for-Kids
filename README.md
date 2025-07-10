!pip install transformers gradio torch --quiet
from transformers import pipeline, set_seed
story_generator = pipeline('text-generation', model='gpt2')
set_seed(42) 
def generate_story(theme, character, location):
    prompt = f"Once upon a time in {location}, there lived a {character} who loved {theme}. One day,"
    story = story_generator(prompt, max_length=200, num_return_sequences=1) [0]['generated_text']
    return story
    import gradio as gr

iface = gr.Interface(
    fn=generate_story,
    inputs=[
        gr.Textbox(label="Theme (e.g., adventure, kindness, magic)"),
        gr.Textbox(label="Main Character (e.g., unicorn, robot, fairy)"),
        gr.Textbox(label="Location (e.g., enchanted forest, outer space, jungle)")
    ],
    outputs=gr.Textbox(label="Generated Story"),
    title="StoryCrafter Short Story Generator for Kids",
    description="Enter a theme, character, and location to generate a magical story for children!"
)

iface.launch()
