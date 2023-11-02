#reading through the VIMAPolicy network we find the following 


There are several networks that make up the VIMA Policy architecture 

axattn_gpt: 
this is the GPT based model taken from the open AI library

The xaten is meant to take in the attention between the different modalities? 
you can see this when we do our forward step line 149 in  vima_policy.py 
it takes in the obs_action_tokens,prompt_tokens and a masking of the prompt 
i assume the masking is to prevent "seeing" the future? 

from the transformer perspective. 
The observation_action tokens  function as the query 
the pormpt_tokens are the key and value pairs.

it is only used in the forward step when calculating which actions to take. 
it may be of interest to note that. The model specifies 
n_layer -> number of cross attention layers. these layers will attend to the prompt and history toekns 
n_head --> number of heads in the self attention layers 
xattn_n_heads --> number of heads to learn 
xattn_n_positions --> number of positional embeddings ? 
xattn_ff_expanding --> for some reason in cross attention. We may want to expand the hidden dimension it seems internally 

THIS SHOULD BE TRAINABLE 
obj_encoder : 
- this is just the VIT model that will take the RGB view of the model and produce a vector representation 
- it uses a bounding box_mlp i assume it is to somehow parse ? 
- For our purposes we do not have to train this model  

end_effector_encoder 
- encodes the effector (motor)  observations into numerical values 

obj_fusion_layer
- fuses the encodings of the objects with the end_effector features 
action_encoder
- Since the actions are essenially a dictionary. Every action is encoded  using seperate dict of nn.linear 
- Takes the embeddigns of all the otehr possible actions and outputs them as one sincle encoding 

prompt_embedding 
- encode prompt using a wordEmbedding 
t5_prompt_encoder
- use a T5 model to encode the prompt 
t5_prompt_encoder_postlayer



OTHER interesting facts 
observations are discretized into  bins.  i,e  50 bins for x,z movement, y movement has 100 
- rotations have 50 or so unique ones 
