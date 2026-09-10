To run readdicom7 p-combo

(1) Copy distributed "combo" p-code into your home "Matlab" directory
(or any other directory in your Matlab path).

(2) start Matlab and run the command as if executing regular m-function, e.g.,:
After scaninfo_combo -- cataloging
To extract specific series imageds and meta-data, execute "readdicom7_combo" 
	   (and choose series):
	>> [imdat,dim1,dim2,dim3,dim4,fov1,fov2,fov3,fov4,tr,unique_te,ppd,flip, dinf, nifti_params] = readdicom7_combo(0,1, 'fp');
INPUT pars (full list: [] = readdicom7_combo(seeit, dirchoice, fpdv, subsample, slicenum, phasenum))
	seeit	show data
	dirchoice how to browse to "series" folder: 0 = start at SimpleDicom level; 1 = start a level above last selection;
		2 = start within last selection; 3 =  start within current dir
	fpdv	output scaling: 'fp' = (default) returns scaling that is proportional to true "floating point" 
                value of true MR signal; 'dv' = returns "display value" pixel intensity same as an ROI 
		on the scanner; 'no' = means no scaling applied
	subsample average pixels to save memory: 1 = 2x2 averaging; 0 = no avreaging
	slicenum  slice number to output (gets all when missing)
	phasenum  dynamic phase to output (gets all when missing)
OUTPUT:	   
x		This structure contains the actual dynamic images.The field names stored in "x" are:
	idata	The images.  In this example, if you extract the idata field via:  
		imgs = getsafield(x,'idata');  T
	td	equal the standalone td array which is the time (in msec) 
		each image was acquired relative to the 1st slice at 1st timepoint.
	loc	Spatial location of each image (in mm) as 3x1 array.
	echotime	Echotime of each image.  Not relevant here.
	bvalue	b-value of each image.  Not relevant here.
	ppd	Pre-pulse delay.  Not relevant here.
	orient	Direction cosines of each image as 6x1 array.
	diffdir diffusion gradient direction cosines for each image 3xn-images array
dinf	DICOM header structure for the 1st image/1st slice of "idata"
nifti_params	Structure of geometric and dynamic parameter arrays (for each image in "idata")

	NOTE: you can then query the output structures and save relevant info using Matlab
 		eg, for DTI series:
	>> idat = getsafield(imdat, 'idata'); % 4D image data
	>> bvals = getsafield(imdat, 'bvalue'); % corresponding b-value array
	>> ddirs = getsafield(imdat, 'diffdir'); % diffusion direction cosines

