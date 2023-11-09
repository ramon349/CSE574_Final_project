# CSE574_Final_project

# Setting up enviroment in the cluster 
1. access the cluser using this weblink : https://ood01.sol.rc.asu.edu/pun/sys/dashboard/
2.  In interactive apps select Sol Desktop.  
    - make sure to select 1 gpu 
    - I don't know if this will always be needed but at least for visualizing the demo it is needed. 
    - Model training will mostlikely be gui less 🙂
3. Open up a terminal and run the command `module load mamba`
    - This is a package manager similar to conda used by the cluster 
    - We only need this for setting up the enviroment 
    - run `mamba create -n my_vima python=3.9.18` 
    - the github repo says vima uses python3.9 so we will use the latest security update for it
    - This is probably why the below has so many issues 

4. Install the follow packages WARNING: if you don't you will have a bad time 🔫 
    - 'pip3 install setuptools==65.5.0
    - 'pip3 install wheel==0.38.4   
    - Why do we need these?  setuptools is needed for VimaBench to build properly 
    - wheel==0.38.4 is a version before a breaking change that affects openaigym 
    - Note: it is possible another configuration may fix this issue but this works 
5. Setup vima first https://github.com/vimalabs/VIMA
    - i.e run   
    ```Bash
        git clone https://github.com/ramon349/VIMA
        cd ./VIMA
        pip install -e .
    ```
6. Setup VIMABench
    ```Bash 
        git clone https://github.com/vimalabs/VimaBench && cd VimaBench
        pip install -e .
    ```
7. Do the following: THIS IS NEEDED FOR THE GUI TO WORK  source: https://asurc.atlassian.net/wiki/spaces/RC/pages/1799487521/OpenGL+WebGL+Support+on+Firefox
    ```
    module load gcc-12.1.0-gcc-11.2.0
    module load mesa-22.0.2-gcc-11.2.0
    ``` 
8. Open firefox and  type  about:config
    - Hit the blue square saying you accept the risk.  
    - Search for webgl.force  in the config search bar 
    - make sure that webgl.force-enable is set to true 
9.  within the VimaBench directory run
    ```bash
    python3 ./scripts/oracle/run.py 
    ```

# Running the model with pretrained weights 
1. Follow the instructions to download the weights from the VIMA repo 
2. Inside the vima folder there  is a bash file that will run 1 task.  
3. Modify it to point at the correct weights. 
4. run said bash file and view the outputs 
# TODOS
1. Baseline Model Implementation
    - The model was trained using behavior cloning 
    - Trajectories made by the orcale and used for training are available at: https://huggingface.co/datasets/VIMA/VIMA-Data
    - We would need to know the following 
        - The behavior cloning training loop ( Someone can  do a simple stablebaselines tutorial to understand this?) 
        - Loading and using trajectories  
        -simple baselines link: https://stable-baselines.readthedocs.io/en/master/guide/pretrain.html
2. HER Training 
    - HER training has two phases. We can observe how stablebaselines does the two phases 
    - How can we do exploration?