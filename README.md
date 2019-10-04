# South End Jupyter Lab Activity - DS 4200 F19

# Setup instructions
1. Clone the repo
2. CD to the repo directory. Create and activate a virtual environment for this project  
  * On macOS or Linux:
   ```
   python3 -m venv env
   source env/bin/activate
   which python
   ```
  * On Windows:
   ```
   py -m venv env
   .\env\Scripts\activate
   where python
   ```
3. Install necessary packages
   ```
   pip install -r requirements.txt
   ```
 
# Run instructions
   
1. Run `jupyter lab`. It should open your browser and let you select select any Jupyter Notebook .ipynb file.
2. Run individual cells with ctrl+enter. In the menu you can run all cells and restart the kernel to clear variables.

# Quit instructions
1. Make sure to save your .ipynb file and shutdown Jupyter Lab properly through the file menu. Otherwise you need to use `jupyter notebook stop`.

2. Deactivate the venv to return to your terminal using `deactivate`.

# Directions for committing

1. If you have made any changes to the required packages you should export a list of all installed packages and their versions:
   ```
   pip freeze > requirements.txt
   ```

2. **Before you commit a Jupyter Notebook .ipynb file, clear the outputs of all cells.** This decreases file size, removes unnecessary metadata, and makes diffs easier to understand. In Jupyter Lab you can use the GUI: Edit->Clear All Outputs.

## Optional git setup to automatically clear metadata using JQ (Highly Recommended)

1. Install JQ by running `sudo apt-get install jq` for more options check [here](https://stedolan.github.io/jq/download/).
2. Append the following block of code either in your local repo `.gitconfig` file or your global `.gitconfig`. I would recommend to do it in your global `.gitconfig` so you don't need to redo that for future .ipynb files.<br>
    ```
    [core]
    attributesfile = ~/.gitattributes_global

    [filter "nbstrip_full"]
    clean = "jq --indent 1 \
            '(.cells[] | select(has(\"outputs\")) | .outputs) = []  \
            | (.cells[] | select(has(\"execution_count\")) | .execution_count) = null  \
            | .metadata = {\"language_info\": {\"name\": \"python\", \"pygments_lexer\": \"ipython3\"}} \
            | .cells[].metadata = {} \
            '"
    smudge = cat
    required = true
    ```
    For more details look at this great tutorial [here](http://timstaley.co.uk/posts/making-git-and-jupyter-notebooks-play-nice/).
3. Create a global gitattributes named `.gitattributes_global` file (usually placed at the root level, so `~/.gitattributes_global`).
4.  Add the following line of code
    ```
    *.ipynb filter=nbstrip_full
    ```

# Optional features

* To get markdown section numbering use [jupyterlab-toc](https://github.com/jupyterlab/jupyterlab-toc). To install run: `jupyter labextension install @jupyterlab/toc` 
  * Then click the enumerated list button on the left strip in JupyterLab to bring up the table of contents. There you can click the itemized list button in the top to add section numbers to the markdown cells.

* For a useful [Spellchecker](https://github.com/ijmbarr/jupyterlab_spellchecker) the following extension is useful.
  *  To install run: `jupyter labextension install @ijmbarr/jupyterlab_spellchecker`

# Once we are done with the tutorial...

Start working through the [Altair data visualization curriculum](https://github.com/uwdata/visualization-curriculum).