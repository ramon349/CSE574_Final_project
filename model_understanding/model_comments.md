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

end_effector_encoder 
obj_fusion_layer
action_encoder
prompt_embedding
t5_prompt_encoder
t5_prompt_encoder_postlayer
