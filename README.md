
**Site in construct, thanks your comprehension**
### [Consulter le site en français](README.fr.md) 

# Introduction

# __Plan :__

- [Versionning : Git & Unity](#versionning--git--unity)
  - [.gitignore](#gitignore)
  - [Smart Merge](#smart-merge)
  - [Large files (.png, .fbx, ...)](#large-files)
        
- [Tests & TDD](#tests-&-tdd)
  - [Tests : Introduction](#tests--introduction)
  - [Unit Tests](#unit-tests)
  - [TDD (Test-driven-developpement)](#tdd-test-driven-developpement)
        
- [Clean Code](#clean-code)
- [Architecture](#architecture)


# Versionning : Git & Unity

You want use *git* for your *Unity* project ? But sometimes, scenes or prefab crash ! In fact, two person modify same file in same time provoke many conflict and by default, git don't solve this problems.   
You open your scene and you see that it is empty. A solution exist for that and this is what I present below.

## .gitignore

This is important to add a **.gitignore** file to your project. This file will allow to ignore unity tempory file and IDE tempory file.  
Moreover, you can add folder to ignore, for exemple, an asset folder from the *asset store* can weight a lot and slow down your archive.

[see .gitignore Unity](https://github.com/github/gitignore/blob/master/Unity.gitignore)

## Store file in YAML

![Image of Unity Project Settings](https://s3.amazonaws.com/gamasutra/UnityVersionControlSettings.png)

Pass asset serialization mode in “Force Text”. This option convert binary file to YAML file.

## Smart Merge

Since *Unity* 5.0, a **UnityYAMLMerge tool** is include with its installation.  
For use them, Copy/Paste the following lines in  **.git/config** file.

```
[merge]
tool = unityyamlmerge
[mergetool "unityyamlmerge"]
cmd = 'C:\\Program Files\\Unity\\Editor\\Data\\Tools\\UnityYAMLMerge.exe' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
trustExitCode = false
keepTempories = true
keepBackup = false
```

Modify the "*C:\\ ...*" link to adapt with your Unity location. If you work in team, you can use the same location for easy maintenable problem.  
**Warning : don't forget to use '\\\\' and no '\\' ou '/'.**  

*[this merge tool can be used with other tools (Perforce,SVN, Mercurial, SourceTree) , see documentation](https://docs.unity3d.com/Manual/SmartMerge.html)*  

This tool is very perform and allowed to work in team without minim risk of loss scene or prefab.
  
### How it's works ?

use git as usual and when your merge crash, use the smartmerge command :  "git mergetool". 

In this following exemple, Two branch are create "Master" and "Another". Each branch modify "sceneTest" scene and commit. After, we try to merge and it crash. And now,  Our "sceneTest" is empty. Then we tap "git mergetool" and we find our scene with the twice modification.

![Schema of Smart Merge](https://raw.githubusercontent.com/jaayap/Unity_Best_Practices/master/Img/schemaSmartMergeV2.PNG?token=AHjeDi_p8D-_yEHzg1tX2cRNjKBIPpT7ks5bWHrPwA%3D%3D)

Limits of Smartmerge :  
  - Modify the same object in a scene  
  - Modify the same property of prefab  
  
In this cases, you will be able to choose the good version (your scene or colleague scene).  


## Large files

  Versionning large files (.png, .fbx, ...) can be hard. Github don't accept files that weigh more than 100 MB and git keep all versions of all your files. Versionning large files make clone and recuperation for other user longer.  
  Git imposed to each user to have as much free space as used space (For exemple, if your project is 1 GB, Git need 2 GB).  
  If your project is compatible with [Git LFS](https://git-lfs.github.com/), use it ! (GitHub / Bitbucket / Gitlab since 8.0 version)
  [Git LFS is a open source git extention](https://github.com/git-lfs/git-lfs?utm_source=gitlfs_site&utm_medium=repo_link&utm_campaign=gitlfs).  
  
  :!: **Warning**, this solution works **only** for file **less than 2 GB**.
  
### How git LFS works ?

![Image Explicative de Git LFS](https://raw.githubusercontent.com/jaayap/Unity_Best_Practices/master/Img/image9.png?token=AHjeDpsdDG7nmpaEzQkxpTVyQp2cHdTmks5bWG9nwA%3D%3D)

[Git LFS](https://git-lfs.github.com/), track chosen files with name, extensions, folder location, ...  
Chosen files will be stock in a LFS server automatically and git keep only links to their files. This system don't versionning track files but in most project, assets 3D or 2D are already versioned by Designers.  

**For install git LFS, write the command :**

```
$ git lfs install
```
Git LFS is install automatically and return this message :
```
>Updated git hooks.
>Git LFS initialized.
```
**use the follow command for track your file (here all .png file)**
```
$ git lfs track "*.extension" 
>Tracking "*.png"
```

**Add a *.gitattributes* to your project**

```
$ git add .gitattributes
```

if you use *GitHub*,the notification “stored with Git LFS” appears in your traked files.

![Image of Github Stored with Git LFS](https://raw.githubusercontent.com/jaayap/Unity_Best_Practices/master/Img/image7.png?token=AHjeDnlpMeQpTc27ikncn_j53g50GMEOks5bWG4gwA%3D%3D)


For understand [Git LFS](https://git-lfs.github.com/), you can watch the bitbucket video : 

[![video Btbucket Git LFS](http://img.youtube.com/vi/9gaTargV5BY/0.jpg)](http://www.youtube.com/watch?v=9gaTargV5BY "Git LFS explain")


Other solution for large file in git project : Git annex, Git fat , Git media , Git Bigstore, Git sizer… 
But they have few or no documentation and they don't really adapt to Unity project's needs.


# Tests & TDD
## Tests : Introduction
## Unit tests
## TDD (Test-driven-developpement)
# Clean Code
# Architecture


## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/jaayap/Unity_Best_Practices/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/jaayap/Unity_Best_Practices/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
