## Install and Setup UV package manager
- https://docs.astral.sh/uv/getting-started/installation/
---
## Set UV environment

- Go to your project folder(Notebooks) and use this command to initialise uv environment:
	- `uv venv`
-  To view environment is created or not using this `ls -al` command, which will show `.venv` folder is created to handle uv environment.
- Now activate the environment using this command `source .venv/bin/activate`
>[!Warning] 
>Note Everytime you need to activate this project environment to run the notebooks.

---
###  Set Jupyter Kernel
- To manage jupyter kernel in this create environment we first need to install the `ipykernel` package using uv.
	-  `uv pip install ipykernel`
-  Now to create a new kernel use this commands
	- `python -m ipykernel install --user --name=myenv --display-name "Python(myenv)"`
	- Here `--name` is name for your kernel and `--display-name` is the displayed name for your kernel.
- To check our kernel is created or not use this kernel list command: `jupyter kernelspec list`
- And to delete a existing kernel use this command:`jupyter kernelspec list `
- And to delete a existing kernel use this command: `jupyter kernelspec uninstall myenv`
	-  Here instead of `myenv` give your kernel name.
	
---
###  Installing PyTorch
- First you need to install PyTorch in the newly created environment : `uv pip install jupyter lab.`
-  After installation run the jupyter lab using this command: `jupyter lab`
>[!Warning]
> Use the `jupyter lab .` command in the current working project directory.
---

