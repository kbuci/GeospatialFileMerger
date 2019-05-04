# GeospatialFileMerger

Libraries

HDF5
https://portal.hdfgroup.org/pages/viewpage.action?pageId=50073884
http://docs.h5py.org/en/stable/

Quad tree Query approach (Danh's earlier suggestion)

>Store the bounding box points (NW corner, SW corner, etc) of all files in a tree strucutre for lookup
>The user asks for the four corners of the desired "tile" (p1,p2,p3,4)
>Create a new HDF5 file R with the size of these tile bounds, and have square chunks
>Compile a list F of all the files with bounds that intersect with these request tile

>Then do  
For File in F:  
  For elevation value in File  
    Compute the exact geospatial lat-long coordinate thing using the row#,col#, and coordinates of corner of the file  
    If that coordinate is withing the desired tile bounds:  
      Lookup the same coordinate in the R file and write to it if its emptup or has a lower/higher elevation  
>Then run preprocessing steps on R needed for PRIMo before sending it  

Building a giant file approach (Thing we drew on whiteboard)  

>Get the bounding box points (NW corner, SW corner, etc), and use it to compute the rectangle bounds the cover the whole region  
>Create a new HDF5 file R with the size of this region bounds, and have square chunks  
>Then do  
For all File  
  For elevation value in File  
    Compute the exact geospatial lat-long coordinate thing using the row#,col#, and coordinates of corner of the file  
    Lookup the same coordinate in the R file and write to it if its emptup or has a lower/higher elevation>  
>The user asks for the four corners of desired "tile" (p1,p2,p3,p4)  
>Splice that section from R directly, run preprocessing stuff before sending it  
