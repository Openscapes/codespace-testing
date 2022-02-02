# codespace-testing

How to set up GH codespace for NASA Hackathon tutorials. I will [use a predefined container](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/configuring-codespaces-for-your-project#using-a-predefined-container-configuration) based on a Jupyter Data Science container with Python, R and Julia. I wanted R, but for just running the NASA Jupyter notebooks, you could just use the default codespace container I think. Then I customize the conda environment with a `environment.yml` file. That installs the Python packages that I need.

1. Click on green code button and then the codespace tab
2. Select a 4-core, 8Gig RAM codespace
3. Once you are in the codespace, use Shift+Command+P to get to the  VS Code Command Palette. Then start typing "dev container". Select Codespaces: Add Development Container Configuration Files....
4. In the dropdown, select 'show all' or something like that, and then pick the Jupyter data-science container. That will get you Jupyter notebook. There is probably a lighter container that you could select.
5. Click Rebuild Now. Takes awhile for it to build the first time.

Now you add the environment file to get the Python packages needed for the NASA Hackathon. You can do this in the codespace or in the repo. Putz around in the codespace and you'll stumble on the links to get back to the repo or to add files directly in the codespace. Look for the branch icon to commit changes back to the repo.

7. As the base level of the repo, add a file [`environment.yml`](https://github.com/Openscapes/codespace-testing/blob/main/environment.yml)
8. Open `.devcontainer/devcontainer.json`. Scroll towards the botton and add this line.
```
"postCreateCommand": "sudo -E mamba env update -f environment.yml",
```

9. Rebuild your codespace. Be patient the first time. It takes awhile to load the environment. You want to get the terminal showing at the bottom and then you can watch the progress.
10. The next time you open the codespace it'll go faster.
