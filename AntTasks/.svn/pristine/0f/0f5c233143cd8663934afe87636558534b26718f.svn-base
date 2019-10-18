package build.antTasks.classes;

import java.awt.*;
import java.awt.event.*;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Properties;

import org.apache.tools.ant.Task;
import org.apache.tools.ant.BuildException;

public class BuildChoice extends Task {
	
	// used to store the parameters passed by the build.xml to the task 
	private File propetiesFileLocation;
	private String projectProperty;
	private File versionFilesLocation;
	//private String versionPropertiesFileLocation;
	
	// used to store temp values before setting the project properties
	private String projecValue;
	private String value;
	private String pass;
	private String versionNum;
	private String deliverable_name;
	private String newRoot;
	private String edvrVersionNum;
	private String berthingVersionNum;
	private String mmrVersionNum;

	
	private boolean cancelled;

	//project constants
	public final String edvrProject = "EDVR";
	public final String berthingProject = "Berthing";
	public final String mmrProject = "MMR";
	public final String s2deProject = "S2DE";
	public final String allProjects = "All NTDPS Integration Deliverables";
	public final String defaultValue ="--------------------------------------------";
	
	// setters that are being used to set the the variables that came from the build.xml file
	public void setPropetiesFileLocation(File location){
		this.propetiesFileLocation=location;
	}
	
	public void setVersionFilesLocation(File versionFileLocation){
		this.versionFilesLocation=versionFileLocation;
	}
	
	public void setProjectProperty(String property){
		this.projectProperty=property;
	}
		
	/**
	 * Method that runs the task
	 */
	public void execute() throws BuildException {
		// might need it
		final Properties properties = loadProperties(propetiesFileLocation);
		
		cancelled = false;

		Frame hiddenFrame = new Frame("NTDPS frame");
		
		final Dialog dialog = new Dialog(hiddenFrame, "NTDPS Build Tool", true);
		dialog.setLocation(100,100);
		
		dialog.setLayout(new GridLayout(7,1));
		dialog.addWindowListener(new WindowAdapter() {
			public void windowClosing(WindowEvent windowEvent) {
				cancelled = true;
				dialog.dispose();
			} 
		});
		
		// login information************************************************
		Panel cvsPanel= new Panel();
		Label cvsRootLabel = new Label("CVS Username");
		
		final TextField cvsRootInput = new TextField(16);

		
		cvsPanel.add(cvsRootLabel);
		cvsPanel.add(cvsRootInput);
		
		Panel passPanel= new Panel();
		Label passLabel = new Label("CVS Password");
		
		final TextField passInput = new TextField(16);
		passInput.setEchoChar('*');

		passPanel.add(passLabel);
		passPanel.add(passInput);
		//login information*********************************************
		
		// drop down box panel************************************************
		Panel choicePanel= new Panel();
		Label choiceLabel = new Label("Select project to build");
		
		final Choice projectChoice = new Choice();

		projectChoice.add(defaultValue);
		projectChoice.add(edvrProject);
		projectChoice.add(berthingProject);
		projectChoice.add(mmrProject);
		projectChoice.add(s2deProject);
		projectChoice.add(allProjects);
		
		choicePanel.add(choiceLabel);
		choicePanel.add(projectChoice);
		//drop down box panel*****************************************************
		
		//check box panel *****************************
		Panel checkBoxPannel= new Panel();
		final Checkbox executableCheckBox= new Checkbox("Create executables?");
		checkBoxPannel.add(executableCheckBox);
		// check box panel******************************
		
		//deliverable info panels******************************************************
		
		final Panel deliverableInfo = new Panel();
		Label deliverableNameLabel = new Label("Please provide the name of deliverable:");
		final TextField deliverableName = new TextField(16);

		
		deliverableInfo.add(deliverableNameLabel);
		deliverableInfo.add(deliverableName);
		deliverableInfo.setVisible(false);
		
		final Panel versionInfo = new Panel();
		final Panel singleVersion= new Panel();
		final Label versionNumberLabel= new Label("Project version number:");
	
		
		final TextField versionNumber= new TextField(16);
		versionNumber.setEnabled(false);
		singleVersion.add(versionNumberLabel);
		singleVersion.add(versionNumber);
		
		final Panel multipleVersions= new Panel();
		final Label edvrVersionLabel= new Label("EDVR version:");
		final TextField edvrVersion= new TextField(6);
		edvrVersion.setEnabled(false);
		final Label berthingVersionLabel= new Label("Berthing version:");
		final TextField berthingVersion= new TextField(6);
		berthingVersion.setEnabled(false);
		final Label mmrVersionLabel = new Label("MMR version:");
		final TextField mmrVersion = new TextField(6);
		mmrVersion.setEnabled(false);
		
		multipleVersions.add(edvrVersionLabel);
		multipleVersions.add(edvrVersion);
		multipleVersions.add(berthingVersionLabel);
		multipleVersions.add(berthingVersion);
		multipleVersions.add(mmrVersionLabel);
		multipleVersions.add(mmrVersion);
		
		versionInfo.setVisible(false);
		// deliverable info panels***************************************************
		
		// buttons panel**************************************************
		Panel buttonPanel = new Panel();
		Button okButton = new Button("Build");
		Button cancelButton = new Button("Cancel");
		buttonPanel.add(okButton);
		buttonPanel.add(cancelButton);
		//buttons panel*******************************************
		
		// action listeners*************************************
		// ok button action listener****************************
		okButton.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent actionEvent) {
				value = cvsRootInput.getText();
				pass=passInput.getText();
				String cvsLocation = properties.getProperty("cvs.ip");
				newRoot=createCVSRoot(value,pass, cvsLocation);
				projecValue=projectChoice.getSelectedItem();
				if(executableCheckBox.getState()){
					deliverable_name = deliverableName.getText();
					versionNum = versionNumber.getText();
					if(projectChoice.getSelectedItem().equals(allProjects)){
						edvrVersionNum=edvrVersion.getText();
						berthingVersionNum=berthingVersion.getText();
						mmrVersionNum=mmrVersion.getText();
					}
					else{
						versionNum=versionNumber.getText();
					}
				}
				dialog.dispose();
			}
		});
		// ok button action listener****************************
		// cancel button action listener************************
		cancelButton.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent actionEvent) {
				cancelled = true;
				dialog.dispose();
			}
		});
		// cancel button action listener************************
		
		//drop down action listener****************************
		projectChoice.addItemListener(new ItemListener(){			
			public void itemStateChanged(ItemEvent e) {
				versionInfo.setVisible(false);
				executableCheckBox.setVisible(true);
				deliverableInfo.setVisible(false);
				versionNumber.setText("");
				executableCheckBox.setState(false);
				
				File versionPropertiesFile;
				if(e.getItem().equals(edvrProject)){ 
					versionPropertiesFile= new File(versionFilesLocation + "/" + "edvr.version.properties");
					versionNumber.setText(createVersionNum(loadProperties(versionPropertiesFile)));
				}
				else if(e.getItem().equals(berthingProject)){
					versionPropertiesFile= new File(versionFilesLocation + "/" + "berthing.version.properties");
					versionNumber.setText(createVersionNum(loadProperties(versionPropertiesFile)));
					
				}
				else if(e.getItem().equals(mmrProject)){
					versionPropertiesFile= new File(versionFilesLocation + "/" + "mmr.version.properties");
					versionNumber.setText(createVersionNum(loadProperties(versionPropertiesFile)));
				}
				else if(e.getItem().equals(s2deProject)){
					versionPropertiesFile= new File(versionFilesLocation + "/" + "s2de.version.properties");
					versionNumber.setText(createVersionNum(loadProperties(versionPropertiesFile)));
					executableCheckBox.setVisible(false);
					dialog.validate();
					versionInfo.setVisible(true);
				}
				else if(e.getItem().equals(defaultValue)){
					
					executableCheckBox.setState(false);
					deliverableInfo.setVisible(false);
					versionInfo.setVisible(false);
				}
				if(e.getItem().equals(allProjects)){
					
					versionPropertiesFile= new File(versionFilesLocation + "/" + "edvr.version.properties");
					edvrVersion.setText(createVersionNum(loadProperties(versionPropertiesFile)));
					versionPropertiesFile= new File(versionFilesLocation + "/" + "berthing.version.properties");
					berthingVersion.setText(createVersionNum(loadProperties(versionPropertiesFile)));
					versionPropertiesFile= new File(versionFilesLocation + "/" + "mmr.version.properties");
					mmrVersion.setText(createVersionNum(loadProperties(versionPropertiesFile)));
					
					
					versionInfo.remove(singleVersion);
					versionInfo.add(multipleVersions);
					versionInfo.validate();
					dialog.validate();
				}
				else{
					
					versionInfo.remove(multipleVersions);
					versionInfo.add(singleVersion);
					versionInfo.validate();
					dialog.validate();
				}
			}}
		);
		
		//drop down listener****************************************
		
		//checkbox action listener*************************************
		executableCheckBox.addItemListener(new ItemListener(){
			public void itemStateChanged(ItemEvent e) {
				if(e.getStateChange()==ItemEvent.SELECTED && !projectChoice.getSelectedItem().equals(defaultValue)){
					deliverableInfo.setVisible(true);
					versionInfo.setVisible(true);
					deliverableInfo.requestFocus();
				}
				else{
					deliverableInfo.setVisible(false);
					versionInfo.setVisible(false);
				}	
			}
		});
		// checkbox action listener***************************************
		// textboxes key listener*****************************************
		KeyAdapter ka= new KeyAdapter(){
			public void keyPressed(KeyEvent e){
				if(e.getKeyCode() == KeyEvent.VK_ENTER){
					if(e.getSource()==cvsRootInput){
						passInput.requestFocus();
					}
					else if(e.getSource()==deliverableName){
						versionNumber.requestFocus();
					}
				}
			}
		};
		
		//textboxes key listener******************************************
		cvsRootInput.addKeyListener(ka);
		deliverableName.addKeyListener(ka);
		versionNumber.addKeyListener(ka);
		//action listeners***************************************************
		
		dialog.add(cvsPanel);
		dialog.add(passPanel);
		dialog.add(choicePanel);
		dialog.add(checkBoxPannel);
		dialog.add(deliverableInfo);
		dialog.add(versionInfo);
		dialog.add(buttonPanel);
		
		dialog.pack();
		dialog.setSize(550, dialog.getSize().height);
		dialog.setVisible(true);
		hiddenFrame.dispose();

		if (cancelled) {
			throw new BuildException("Cancelled by user.");
		}
	
		//error checking
		if((value.trim().length()== 0 || value.trim().equals("")) || (pass.trim().length()== 0 || pass.trim().equals(""))){
			throw new BuildException("Login information is required");
		}
		else if(projecValue.equals(defaultValue)){
			throw new BuildException("Project is required");
		}
		else if(executableCheckBox.getState() && (deliverable_name.trim().length()==0 || deliverable_name.trim().equals(""))){
			throw new BuildException("Deliverable name is required");
		}
		//end of error checking
		
		//setting project properties
		if (value != null && pass!=null && !projecValue.equals(defaultValue)){
			getProject().setProperty(projectProperty, projecValue);
			getProject().setProperty("cvsroot", newRoot);
			if(executableCheckBox.getState()){
				getProject().setProperty("create_Executables", "true");
				getProject().setProperty("deliverable_Name", deliverable_name);
				if(projectChoice.getSelectedItem().equals(allProjects)){
					getProject().setProperty("edvr_version", edvrVersionNum);
					getProject().setProperty("berthing_version", berthingVersionNum);
					getProject().setProperty("mmr_version", mmrVersionNum);
					
				}
				else{
					getProject().setProperty("version_Number", versionNum);
				}
			}
		}
		//setting project properties
	}
	
    /**
     * Method to load the properties from a properties file, the location of the file is load when the task is called
     * @return the loaded properties from the properties file
     * @throws BuildException
     */
	public Properties loadProperties(File fileLocation) throws BuildException{
		
		FileInputStream input=null;
		try{
			Properties p= new Properties();
			input = new FileInputStream(fileLocation);
			p.load(input);
			return p;
		}
		catch(final FileNotFoundException e){
			throw new BuildException("Could not find " + fileLocation + " properties file");
		}
		catch(final IOException e){
			throw new BuildException("malformated properties file");
		}
		finally{
			if(null !=input){
				try{
					input.close();
				}
				catch(final IOException e){
					throw new BuildException("error closing input stream");
				}
			}
		}	
	}
	
	/**
	 * Create a version number with a v in front of the version number
	 * @param version: the version number of the project provided by the user
	 * @return version: the version number formated with a v in front of the version number (v1-2-3)
	 */
	public String createVersionNum(Properties p){
		//check what happens if the property is empty
		String version="";
		int minor=Integer.parseInt(p.getProperty("build.minor.version")), patch=Integer.parseInt(p.getProperty("build.patch.version"));
		int buildNumber=Integer.parseInt(p.getProperty("build.number"))+1;

		if(p.getProperty("minor.version").equals("true")){
			minor+=1;
		}
		if(p.getProperty("patch.version").equals("true")){
			patch+=1;
		}
		
		//version="v" + p.getProperty("build.major.version") + "-" + minor + "-" + patch + "-" + buildNumber;
		version="v" + p.getProperty("build.major.version") + "-" + minor + "-" + patch;
		
		if(p.getProperty("beta.version").equals("true")){
			version+= "-beta";
			
		}
		return version;
	}
	/**
	 * Method used to construct the string that will be used to login to cvs
	 * @param userName: the user name provided by the user
	 * @param userPassword: password provided by the user
	 * @return cvsroot: the string that will be used to login to cvs
	 */
	public String createCVSRoot(String userName, String userPassword, String cvsLocation){
		String cvsRoot=":pserver:" + userName + ":" + userPassword + "@192.168.1.116:/CVSROOT";
		if(cvsLocation != null || cvsLocation != ""){
			cvsRoot=":pserver:" + userName + ":" + userPassword + "@" + cvsLocation + ":/CVSROOT";	
		}
		return cvsRoot;
		
	}
	
}