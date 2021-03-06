# codespace-testing

How to set up GH codespace for NASA Hackathon tutorials. I will [use a predefined container](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/configuring-codespaces-for-your-project#using-a-predefined-container-configuration) based on a Jupyter Data Science container with Python, R and Julia. I wanted R, but for just running the NASA Jupyter notebooks, you could just use the default codespace container I think. Then I customize the conda environment with a `environment.yml` file (based on the NASA Openscapes [corn](https://github.com/NASA-Openscapes/corn) repo). That installs the Python packages that I need. Note, the virtual machine is on AWS but on west-2-california so the tutorials on S3 access probably won't work.

[Video of me setting up a brand new GitHub codespace from scratch](https://youtu.be/h7QLx2isrw4) Takes all of 3-4 button clicks.

[Video of me demo-ing this repo where you can run the NASA Hackathon tutorials](https://youtu.be/RIchFX_gYb0)

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


## Notes for R

You can use R within Jupyter notebooks but it doesn't have the functionality you are used with with RStudio. This R extension looks like it is working on providing better functionality for R within Visual Studio. https://github.com/REditorSupport/vscode-R

Fork this repo, that is set up for R and vscode-R already. https://github.com/jakubnowicki/r-codespaces
