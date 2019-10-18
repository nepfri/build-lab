******************Before Running the Build Tool make sure the following properties are correct ********************************

Properties to check when building MMR, Berthing, EDVR and TSU: 
	File: E:\working\buildTool\build.properties
	 - jdk.location: make sure is points to the correct version of the Java Compiler for the project that is going to be built
	 - jdk.version: make sure the jdk version is the correct version of the Java Compiler for the project that is going to be built
	 - javac.target: make sure the java target is the right version of the java compiler
	 - jboss.version: make sure this is the right version of the JBoss server in which the project that is going to be built will run
					 this is only for informational purposes.
	- installer.build.mode.switch: make sure the switch is correct, possible values are Release and Debug
	- installer.compiler.exe.location: make sure this property points to the correct Visual Studio compiler for this type of project (.msi)
	- installer.visual.studio.version: make sure this property has the correct Visual Studio compiler version
	
	- edvr.svn.url, snadis.svn.url, ntdps.svn.url: To build EDVR make sure the SVN url's for these projects points to the right (tag or url) in svn
	- berthingAdmin.svn.url, berthing.svn.url, snadis.svn.url, ntdps.svn.url: To build Berthing make sure the SVN url's for these projects points to the right (tag or url) in svn
	- mmr.svn.url, snadis.svn.url, ntdps.svn.url: To build MMR make sure the SVN url's for these projects points to the right (tag or url) in svn
	- tsu.svn.url: To build TSU make sure the SVN url for the project points to the right (tag or url) in svn
	- keyport.nim.installer.svn.url: When building a release deliverable, make sure the SVN url for the project points to the right (tag or url) in svn
	
	File: E:\working\buildTool\version number properties files
		Choose the file that is named after the project that is going to be built and modify the following properties as necessary.
		These properties are read from the UI and that is what is displayed in the version number part of the UI, these properties are also used
		for updating the version number that the installer will wright to registry.
	- build.major.version
	- build.minor.version
	- build.patch.version
	- build.number: Build number gets incremented automatically, reset it everytime you create a new version
	
Properties to check when building S2DE:
	File: E:\working\buildTool\build.properties
	- msbuild.publisher.exe.location: make sure this property points to the correct Visual Studio compiler for this type of project
	- visual.studio.version: make sure this property has the correct Visual Studio compiler version
	- s2de.build.mode.switch: make sure the switch is correct, possible values are Release and Debug
	- s2de.svn.url, s2de.data.transfer.vbscripts.svn.url: To build S2DE make sure the SVN url's for these projects points to the right (tag or url) in svn

	File: E:\working\buildTool\version number properties files
		Modify the version properties in the S2DE and S2DE Data Transfer version properties files as necessary.
		These properties are read from the UI and that is what is displayed in the version number part of the UI, these properties are also used
		for updating the version number that the installer will wright to registry.
	- build.major.version
	- build.minor.version
	- build.patch.version
	- build.number: Build number gets incremented automatically, reset it everytime you create a new version
	
*********************To run the tool *****************************************************
Open an administrator command prompt
Navigate to E:\working\buildTool
Type ant and hit enter
A Keyport Build Tool pop will appear, fill out the fields and hit build. 

*********************Log In syntax***************************************************
To login use your snait user name and password.


******************War Files**********************************************************
War files can be found inside the build project in the dist folder. 
Example:
	-built project:Edvr 
	-War file location:E:\working\buildTool\buildTool\edvr\dist


********************************Deliverables****************************
If the deliverables checkbox is checked the installation package can be found in:
E:\working\Deliverables\name of deliverable