# outline2dita
Python script to generate a DITA project from a text outline

Creating a DITA project structure for oXygen XML Editor, starting from a simple content outline.  
This initial solution is using a python script. The second version (see https://github.com/mgcalo/model2dita) is using an oXygen framework and adds more features, such as keymaps, submaps and sub-folders. 

## Prerequirements

For outline2dita v1.0 you need:
* oXygen Editor (tested with v16.1, v17.1)
* python 3

## Initial setup

Your repository structure (for example *C:/DITA/outline2dita/*) should contain the following sub-folders and files:

- *_outlines*  
    - *convert-outline2ditamap.bat*  
    - *outline2ditamap.py*
    - *test-project.txt*
    - *testprojekt.txt*  
      *test-project.txt* and *testprojekt.txt* are sample outlines.  
- *projects*  
	- *_topic-templates*  
    		- *de*  
    		- *en*  
    		- *stub-py-Project.xpr*  
    - *test-project*  
    - *test-projekt*  
    	  *test-project* and *testprojekt* are folders with sample results.  

## Writing the content outline

Based on your information model for a new project, write the outline in a .txt file and save it in the *_outlines* folder.  
Until further development, the outline files must start by specifying the three parameters for language, repository and folder name:   
```
language=en  
projects repository=C:/DITA/outline2dita/projects/  
project folder name=test-project
```

Make sure your DITA-OT contains the corresponding language strings. Otherwise it will report a series of errors. 

Starting with the 4th line, each line in the outline text file must contain a topic title and topic type.  
Use **tabs** before the topic title, to give the proper nesting level.  
To specify the topic type, insert a space followed by double hash and the type prefix for concept ##c, task ##t, reference ##r. Eventually, add *_ov* for overview topics.  

Example:  
```
language=en
projects repository=C:/DITA/outline2dita/projects/
project folder name=test-project
Introduction ##c_ov
	About this manual ##c_ov
		Scope ##c
		Qualifications ##r
		Liability ##c
	Product overview ##c_ov
		System requirements ##r
		Support ##r
Installing the product ##t_ov
	Installing the server ##t
	Installing the client ##t
Imprint ##c
```

## Creating the DITA project

1. Double-click *convert-outline2ditamap.bat* to start the script.
2. Click **Choose File** and select the outline file. For example *test-project.txt*.
3. Click **Open** and close the script window.  
  The script creates the stub project structure in the location you specified as `project repository` and opens the File Explorer when ready:  
  - en  
  - test-project.xpr  
  The topic files are created under *en/source/*. The file name and the `title` element are assigned as given in the outline.  
  The ditamap is created under *en* and already contains `conref` elements to the topic files.  
4. Open the .xpr project in oXygen and check if the new *test-project.ditamap* is valid.
5. Try publishing the two associated scenarios for PDF and WebHelp.

## Known issues

1. The map should end with a topic on the first level (such as *Imprint*).
  This issue will be fixed asap.
2. Right-click the other language folder, if you don't need it (*de* or *en*), and click **Remove from project**.
 
