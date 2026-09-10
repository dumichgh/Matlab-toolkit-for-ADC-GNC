FUNCTIONALITY
"scaninfo_combo" catalogues the DICOM series within selected exam folder.

PREREQUISITES
This function expects that individual input series are pre-arranged as a 
single-frame DICOM in separate folders or all series/images are in a single 
folder. It also requires "readdicom7_combo.p" to be placed in Matlab path.

INPUT
(1) optional: browse = 0 (start form current directory), 
		     = 1 (start from the last directory)
(2) User is prompted to select DICOM "exam folder" to catalogue

OUTPUT
"image_order.mat" in each series folder and "ExamDemongraphics.mat" and 
"scaninfo.txt" catalogues for the exam stored inside exam-folder. 
(1) "image_order.mat" is an index file with aux info for each series
(2)"ExamDemographics" contains "ExamSeries" structure with key geomtery and 
acquisition parameters for the series. Its also contains "SiteScanDemographics" 
structure with the system information, and path-string for the original 
exam-folder.
(3) "scaninfo.txt" is an ASCII catalogue of the exam with the brief list of
system "demographics" and series acquisition parameters. 

USAGE
>> scaninfo_combo(0/1); % browse to and select exam folder 
			% containing DICOM series folders

NOTE1: The function will NOT OVER-WRITE existing structures and catalogue.
	If re-catalogueing is desired, purge the exam/series folders from
	all existing "mat" and "txt" before re-run.
NOTE2: Each output mat-structure can be loaded into workspace for perusal: 
	use field-names for guidance.

Authors: Thomas Chenevert (tlchenev@umich.edu) and Dariya Malyarenko (dariya@umich.edu)


