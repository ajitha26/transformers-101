llm basics

1)Install transformers and accelerate
2)Load model and Tokenizer
3)Create a pipeline
4)Prompt 
5)Generte output

AutomodelForCasualLM -GPT like models (Use case:chatbots,completion,creative writing)
AutoModelForCausalLM, AutoModelForSeq2SeqLM, and AutoModelForMaskedLM—they serve different tasks (generation, translation, fill-in-the-blank).
LOAD MODEL
model = AutoModelForCausalLM.from_pretrained(
    "microsoft/Phi-3-mini-4k-instruct",
    device_map="cuda",
    torch_dtype="auto",
    trust_remote_code=False,
)
instruct indicates that it has been fine tuned to respond tp prompts with helpful completions.It follows natural language prompts.(Useful for RAG,Chatbots,Agents,Coding assistants)
1)While choosing a model go thru model Training data,Intended use,Limitations,License from Model card in Hugging face.
2)device_map="cuda":Maps the model to gpu
we can also choose auto(based on availability splitting) or cpu
3)torch_dtype="auto" (selects the apppropriate tensor precision)
This can be set as float32,float16,bfloat16
torch_dtype affects Performance,Model loading errors,Accuracy
4)trust_remote_code=False(disables execution of custom code from model repo)
tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3-mini-4k-instruct")
Autotokeniser converts text to tokens to numerical inputs for models
Autotokeniser auto selects the right tokeniser for your model.It ensures that it matches the model family(eg GPT style,T5 style)


PIPELINE GENERATION(IN DETAIL)
Here pipeline is a function and model=model and tokeniser=tokeniser indicates that we r supplying model and tokeniser
1)return_full_text=False(Only generates the answer given by llm and not the qn)
2)max_new_tokens=500(limits the number of tokens generated after prompt)
3)do_sample=False(disables randomness)
