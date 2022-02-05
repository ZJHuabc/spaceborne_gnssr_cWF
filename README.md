# Spaceborne_GNSSR_CWF_Processing

# Spaceborne_cWF_Product

A processing tool for the spaceborne GNSS-R complex waveform products available at IEEC's GOLD-RTR server.
 The project provides an example for accessing, searching and analyzing the compelx waveform product derived from the GNSS-R raw IF data collected by different spaceborne missions (e.g. TDS-1, CYGNSS, BuFeng-1, SPIRE).

## Functions:

### Downloa_cWF_File_List:
The lists of the product tracks are also available at the GOLD-RTR server. This function is to download the up-to-date lists of the complex waveform products, which include the basic information of the raw IF tracks, such as the raw IF data ID, the data collection time, the PRN of the GNSS transmitter, the SNR of the direct and reflected signals, and the geolocation of the specular point. 

###Find_RawIF_Track:
With the basic information of all available tracks, this function is to search complex waveform tracks by time and geographic location, which returns a text file including a list of the complex waveform files with the specular point crossing the target area, i.e. a rectangle area defined by the maximum/minimum latitudes and longitudes.

###Download_cWF_File:
This function is to download a local copy of a complex waveform file from the GOLD-RTR server. With the text file returned by the \textit{Find\_RawIF\_Track} function, all the complex waveform files can be downloaded sequentially.

###Read_CW_File:
Given the filename of the complex waveform file, this function can return two labeled multi-dimensional arrays including all the variables in the "cWF" group and the "MetaData" group, respectively.

###ShiftCW and CounterRotateCW:
As the OL tracking model is computed without considering the variation of the surface elevation along the track, it is necessary to realign the complex waveform by recomputing the bistatic delay of the reflected signal following a refined surface elevation model. With the precise estimation of the delay evolution along the track, `ShiftCW` function is to align the complex waveforms by shifting each of them along the delay axis, and `CounterRotateCW` function is to counter rotate the phase of the complex waveform by means of a product with a phasor rotated with the corresponding delay difference. It is noted that some other delay correction terms, such as the ionosphere delay and the troposphere delay can be also included in the bistatic delay computation and applied in the complex waveform realignment.

###Integration:
In the raw IF processing stage, the direct and reflected signals are integrated coherently for a fixed period of 1 ms. To decrease the impact of thermal and speckle noise, coherent integration (complex sum) and incoherent average (averaging of the squared amplitudes) are applied to the 1-ms complex waveforms of the direct and reflected signals.

###GNSSR_Obs:
Different GNSS-R observables can be derived from the complex or power waveforms. Currently, the main observables provided with the example function include the SNRs of the direct and reflected signals, the carrier phase of the reflected signal and the coherence factor of the reflected signal. In addition, the geographic locations, i.e. the latitude and longitude, corresponding to these variables are also interpolated at each observation epoch.

###Visualization:
With the value and geographic location of each observable, this function is to generate a KML file \cite{kml} using the Python package `simplekml`. By importing the generated KML file into an Earth browser such as Google Earth, the values of the observable can be indicated with color scales along the track of the specular points, which can be used to characterize the GNSS-R observable over different surface types.
