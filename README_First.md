# nanoporeseq

Collection of scripts for processing Oxford Nanopore Data + README files describing environment setup, what to do with outputs, etc.
Workspace Setup, General coding outline, and troubleshooting found below.

----------------------------------------------------------------------------------------------------------------------------------------




****Workspace Setup****
----------------------------------------------------------------------------------------------------------------------------------------
	Step 1:
		
		Download your RAW fastq files from the website you ran them from. The Raw fastq files should be the larger of the .fq files available to you.

	Step 2: 

		Create a folder on your Desktop with a unique name that DOES NOT have any spaces.
			ex: seqdata060923
   			ex: mattvirus051223

	Step 4:

		Using Finder, move the RAW fastq files into the folder you made. 

	Step 5:

		You will need to download a few files from the internet, particularly those relating to the Viral Reference genome 
		you want to use. The following links will lead you to either the KOS or Strain 17 data.

  		https://www.ncbi.nlm.nih.gov/nuccore/NC_001806   (Strain 17 ~Aug. 2018)
    		https://www.ncbi.nlm.nih.gov/nuccore/KT899744.1  (KOS ~Nov. 2015)
      		https://www.ncbi.nlm.nih.gov/nuccore/            (Search this database with the terms "{your parent strain} HSV1 complete")

	Step 6:

		Download a .fasta file and .gff3 from the site (click "send to"). Move the .fasta file into the same folder you created in Step 2.

	Step 7:
		
		This is now arguably the most important step to make sure the script doesn't break. You need to add a ".fq" to every RAW file in the folder, and a ".fasta" to the one fasta file in the folder.

			ex: Loftus_M9A_3_AH_US11-GFP_Huge_152 -->  Loftus_M9A_3_AH_US11-GFP_Huge_152.fq
			ex: sequence.fa -->  sequence.fasta

		These extensions HAVE to read with either a .fq or .fasta VERBATIM or the code will return an error. 



****Coding****
----------------------------------------------------------------------------------------------------------------------------------------

	Step 7:

		Open iTerm2 and cd (change directory) into your Desktop, then into the new folder you created. The following
		line of code will do that for you when copy and pasted into iTerm2:

			cd Desktop/XXXXX # replace XXXXX with the name of your folder

	Step 8:

		Check to be sure all your files are there in the folder (directory) by typing the following line:

			ls

	Step 9:

		Activate the conda environment "seqtools" by copy/pasting the next indented line, set up in the README text file. This will load in the proper packages "igvtools", "minimap2", and "samtools".

			conda activate seqtools

	Step 10:

		Into the command line, type the following two characters:

			sh

		Then, find the Nanopore_Step1.sh script in Finder and drag it into the command prompt. This will load the script, showing you the direct file path, and the "sh" will tell your computer through the terminal to run it. Press the Enter button.

**At this point, you will have the sorted bam files with IGV index files (.bam.bai) in the bam_aligned_sorted folder**


****Working with IGV Viewer****
----------------------------------------------------------------------------------------------------------------------------------------

	Step 11: 
 
 		Open IGV Viewer and navigate to the "Genome" bar on the top menu. Load in your reference .fasta in your named folder.

   	Step 12:

      		Navigate to "load file" in the sequences tab and load in the .gff3 file (This step is a work-in-progress. I am adding a line of code that will index the .gff3 file automatically to make it loadable.)


 	Step 13:

  		First, load in using the "load file" tab the .bai file for the alignment you want to view, then load the .bam file for the same alignment. This will visualize the entire alignment file for you!
    
    	Here are some useful resources for working with IGV: 
      	https://igv.org/workshops/March2017/SlidesHandouts/IGV_SlideDeck.pdf
		https://notebook.community/ssjunnebo/pathogen-informatics-training/Notebooks/RNA-Seq/transcriptome-visualisation
  		https://evomics.org/wp-content/uploads/2011/09/IGVworkshop_CSH_2013.pdf




****Troubleshooting****
----------------------------------------------------------------------------------------------------------------------------------------

_The coding file is running and I see the output from the "echo" lines, but no files are being generated in any of the folders. It will say a file doesn't exist._

  Solution: Make sure you are both in the correct directory (you can see your .FQ files and .fasta using the "ls" command") and that the proper conda environment is loaded.

_One part of the script is failing (i.e. I'm not seeing a .bai file being created that I need to view the sequences). What is going on?_

  Solution: The first step is to be sure you have all the proper software loaded in your conda environment and that it is active. See the "README_Environment_Setup" file for details on how to do that. The second step is to attempt to manually run each line of code and verify everything is working when it is outside the script. See the "MANUAL_Data_Entry" file for how to run individual files and troubleshoot. 
