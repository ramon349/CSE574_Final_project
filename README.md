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
        pip install git+https://github.com/ramon349/VIMA`
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

# Training the model 
 - To be continuned 

#TODOS 
1. Download weights
2. Run the baseline demo
