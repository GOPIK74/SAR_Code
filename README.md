## The SNAP Graph Processing Tool (GPT) 

The `gpt -h` :

```markdown
# SNAP GPT Tool Documentation

## Usage

```
Usage:
  gpt <op>|<graph-file> [options] [<source-file-1> <source-file-2> ...]

Description:
  This tool is used to execute SNAP raster data operators in batch-mode. The
  operators can be used stand-alone or combined as a directed acyclic graph
  (DAG). Processing graphs are represented using XML. More info about
  processing graphs, the operator API, and the graph XML format can be found
  in the SNAP documentation.

Arguments:
  <op>               Name of an operator. See below for the list of <op>s.
  <graph-file>       Operator graph file (XML format).
  <source-file-i>    The <i>th source product file. The actual number of source
                     file arguments is specified by <op>. May be optional for
                     operators which use the -S option.

Options:
  -h                 Displays command usage. If <op> is given, the specific
                     operator usage is displayed.
  -e                 Displays more detailed error messages. Displays a stack
                     trace, if an exception occurs.
  -t <file>          The target file. Default value is 'target.dim'.
  -f <format>        Output file format, e.g. 'GeoTIFF', 'HDF5',
                     'BEAM-DIMAP'. If not specified, format will be derived
                     from the target filename extension, if any, otherwise the
                     default format is 'BEAM-DIMAP'. Ony used, if the graph
                     in <graph-file> does not specify its own 'Write'
                     operator.
  -p <file>          A (Java Properties) file containing processing parameters
                     in the form <name>=<value> or a XML file containing a
                     parameter DOM for the operator. Entries in this file are
                     overwritten by the -P<name>=<value> command-line option
                     (see below). The following variables are substituted in
                     the parameters file:
                         ${system.<java-sys-property>}
                         ${operatorName} (given by the <op> argument)
                         ${graphFile} (given by the <graph-file> argument)
                         ${targetFile} (pull path given by the -t option)
                         ${targetDir} (derived from -t option)
                         ${targetName} (derived from -t option)
                         ${targetBaseName} (derived from -t option)
                         ${targetFormat} (given by the -f option)
  -c <cache-size>    Sets the tile cache size in bytes. Value can be suffixed
                     with 'K', 'M' and 'G'. Must be less than maximum
                     available heap space. If equal to or less than zero, tile
                     caching will be completely disabled. The default tile
                     cache size is '536,870,912M'.
  -q <parallelism>   Sets the maximum parallelism used for the computation,
                     i.e. the maximum number of parallel (native) threads.
                     The default parallelism is '20'.
  -x                 Clears the internal tile cache after writing a complete
                     row of tiles to the target product file. This option may
                     be useful if you run into memory problems.
  -S<source>=<file>  Defines a source product. <source> is specified by the
                     operator or the graph. In an XML graph, all occurrences of
                     ${<source>} will be replaced with references to a source
                     product located at <file>.
  -P<name>=<value>   Defines a processing parameter, <name> is specific for the
                     used operator or graph. In an XML graph, all occurrences
                     of ${<name>} will be replaced with <value>. Overwrites
                     parameter values specified by the '-p' option.
  -D<name>=<value>   Defines a system property for this invocation.
  -v <dir>           A directory containing any number of Velocity templates.
                     Each template generates a text output file along with the
                     target product. This feature has been added to support a
                     flexible generation of metadata files.
                     See http://velocity.apache.org/ and option -m.
  -m <file>          A (Java Properties) file containing (constant) metadata
                     in the form <name>=<value> or any XML file. Its primary
                     usage is to provide an additional context to be used
                     from within the Velocity templates. See option -v.
  --diag             Displays version and diagnostic information.
```

## Supported Operators

- **Aatsr.SST**: Computes sea surface temperature (SST) from (A)ATSR products.
- **AATSR.Ungrid**: Ungrids (A)ATSR L1B products and extracts geolocation and pixel field of view data.
- **AdaptiveThresholding**: Detect ships using Constant False Alarm Rate detector.
- **AddElevation**: Creates a DEM band
- **AddLandCover**: Creates a land cover band
- **ALOS-Deskewing**: Deskewing ALOS product
- **Apply-Orbit-File**: Apply orbit file
- **Arc.SST**: Computes sea surface temperature (SST) from (A)ATSR and SLSTR products.
- **ArviOp**: Atmospherically Resistant Vegetation Index belongs to a family of indices with built-in atmospheric corrections.
- **Azimuth-Shift-Estimation-ESD**: Estimate azimuth offset for the whole image
- **AzimuthFilter**: Azimuth Filter
- **Back-Geocoding**: Bursts co-registration using orbit and DEM
- **BandMaths**: Create a product with one or more bands using mathematical expressions.
- **BandMerge**: Allows copying raster data from any number of source products to a specified 'master' product.
- **BandPassFilter**: Creates a basebanded SLC based on a subband of 1/3 the original bandwidth
- **BandsDifferenceOp**: No description available.
- **BandSelect**: Creates a new product with only selected bands
- **BandsExtractorOp**: Creates a new product out of the source product containing only the indexes bands given
- **BatchSnaphuUnwrapOp**: Downloads and executes SNAPHU on a set of two or more interferograms.
- **Bi2Op**: The second Brightness index represents the average of the brightness of a satellite image.
- **Binning**: Performs spatial and temporal aggregation of pixel values into cells ('bins') of a planetary grid
- **BiOp**: The Brightness index represents the average of the brightness of a satellite image.
- **Biophysical10mOp**: The 'Biophysical Processor' operator retrieves LAI from atmospherically corrected Sentinel-2 products
- **BiophysicalLandsat8Op**: The 'Biophysical Processor' operator retrieves LAI from atmospherically corrected Landsat8 products
- **BiophysicalOp**: The 'Biophysical Processor' operator retrieves LAI from atmospherically corrected Sentinel-2 products
- **c2rcc.landsat8**: Performs atmospheric correction and IOP retrieval with uncertainties on Landsat-8 L1 data products.
- **c2rcc.meris**: Performs atmospheric correction and IOP retrieval with uncertainties on MERIS L1b data products.
- **c2rcc.meris4**: Performs atmospheric correction and IOP retrieval with uncertainties on MERIS L1b data products from the 4th reprocessing.
- **c2rcc.modis**: Performs atmospheric correction and IOP retrieval on MODIS L1C_LAC data products.
- **c2rcc.msi**: Performs atmospheric correction and IOP retrieval with uncertainties on Sentinel-2 MSI L1C data products.
- **c2rcc.olci**: Performs atmospheric correction and IOP retrieval with uncertainties on SENTINEL-3 OLCI L1B data products.
- **c2rcc.seawifs**: Performs atmospheric correction and IOP retrieval on SeaWifs L1C data products.
- **c2rcc.viirs**: Performs atmospheric correction and IOP retrieval on Viirs L1C data products.
- **Calibration**: Calibration of products
- **Change-Detection**: Change Detection.
- **ChangeVectorAnalysisOp**: The 'Change Vector Analysis' between two dual bands at two differents dates.
- **CiOp**: Colour Index was developed to differentiate soils in the field. It gives complementary information with the BI and the NDVI.
- **CloudProb**: Applies a clear sky conservative cloud detection algorithm.
- **Coherence**: Estimate coherence from stack of coregistered images
- **Collocate**: Collocates two products based on their geo-codings.
- **Compactpol-Radar-Vegetation-Index**: Compact-pol Radar Vegetation Indices generation
- **Compute-Slope-Aspect**: Compute Slope and Aspect from DEM
- **Convert-Datatype**: Convert product data type
- **CoregistrationOp**: Coregisters two rasters, not considering their location
- **CP-Decomposition**: Perform Compact Polarimetric decomposition of a given product
- **CP-Simulation**: Simulation of Compact Pol data from Quad Pol data
- **CP-Stokes-Parameters**: Generates compact polarimetric Stokes child parameters
- **CreateStack**: Collocates two or more products based on their geo-codings.
- **Cross-Channel-SNR-Correction**: Compute general polarimetric parameters
- **Cross-Correlation**: Automatic Selection of Ground Control Points
- **CrossResampling**: Estimate Resampling Polynomial using SAR Image Geometry, and Resample Input Images
- **DarkObjectSubtraction**: Performs dark object subtraction for spectral bands in source product.
- **DeburstWSS**: Debursts an ASAR WSS product
- **DecisionTree**: Perform decision tree classification
- **DEM-Assisted-Coregistration**: Orbit and DEM based co-registration
- **Demodulate**: Demodulation and deramping of SLC data
- **Double-Difference-Interferogram**: Compute double difference interferogram
- **DviOp**: Difference Vegetation Index retrieves the Isovegetation lines parallel to soil line
- **EAP-Phase-Correction**: EAP Phase Correction
- **Ellipsoid-Correction-GG**: GG method for orthorectification
- **Ellipsoid-Correction-RD**: Ellipsoid correction with RD method and average scene height
- **EMClusterAnalysis**: Performs an expectation-maximization (EM) cluster analysis.
- **Enhanced-Spectral-Diversity**: Estimate constant range and azimuth offsets for a stack of images
- **Faraday-Rotation-Correction**: Perform Faraday-rotation correction for quad-pol product
- **Fill-DEM-Hole**: Fill holes in given DEM product file.
- **FlhMci**: Computes fluorescence line height (FLH) or maximum chlorophyll index (MCI).
- **Flip**: flips a product horizontal/vertical
- **ForestCoverChangeOp**: Creates forest change masks out of two source products
- **FUB.Water**: MERIS FUB-CSIRO Coastal Water Processor to retrieve case II water properties and atmospheric properties
- **FuClassification**: Colour classification based on the discrete Forel-Ule scale
- **GemiOp**: This retrieves the Global Environmental Monitoring Index (GEMI).
- **Generalized-Radar-Vegetation-Index**: Generalized Radar Vegetation Indices generation
- **GenericRegionMergingOp**: The 'Generic Region Merging' operator computes the distinct regions from a product
- **GLCM**: Extract Texture Features
- **GndviOp**: Green Normalized Difference Vegetation Index
- **GoldsteinPhaseFiltering**: Phase Filtering
- **GRD-Post**: Applies GRD post-processing
- **HorizontalVerticalMotion**: Computation of Horizontal/Vertical Motion Components
- **IEM-Hybrid-Inversion**: Performs IEM inversion using Hybrid approach
- **IEM-Multi-Angle-Inversion**: Performs IEM inversion using Multi-angle approach
- **IEM-Multi-Pol-Inversion**: Performs IEM inversion using Multi-polarization approach
- **Image-Filter**: Common Image Processing Filters
- **Import-Vector**: Imports a shape file into a product
- **IntegerInterferogram**: Create integer interferogram
- **Interferogram**: Compute interferograms from stack of coregistered S-1 images
- **IonosphericCorrection**: Estimation of Ionospheric Phase Screens
- **IpviOp**: Infrared Percentage Vegetation Index retrieves the Isovegetation lines converge at origin
- **IreciOp**: Inverted red-edge chlorophyll index
- **KDTree-KNN-Classifier**: KDTree KNN classifier
- **KMeansClusterAnalysis**: Performs a K-Means cluster analysis.
- **KNN-Classifier**: K-Nearest Neighbour classifier
- **Land-Cover-Mask**: Perform a masking based on land cover classes
- **Land-Sea-Mask**: Creates a bitmask defining land vs ocean.
- **LandWaterMask**: Operator creating a target product with a single band containing a land/water-mask.
- **LinearToFromdB**: Converts bands to/from dB
- **Maximum-Likelihood-Classifier**: Maximum Likelihood classifier
- **McariOp**: Modified Chlorophyll Absorption Ratio Index, developed to be responsive to chlorophyll variation
- **Mci.s2**: Computes maximum chlorophyll index (MCI) for Sentinel-2 MSI.
- **Merge**: Allows merging of several source products by using specified 'master' as reference product.
- **Meris.Adapt.4To3**: Provides the adaptation of MERIS L1b products from 4th to 3rd reprocessing.
- **Meris.CorrectRadiometry**: Performs radiometric corrections on MERIS L1b data products.
- **Meris.N1Patcher**: Copies an existing N1 file and replaces the data for the radiance bands
- **Minimum-Distance-Classifier**: Minimum Distance classifier
- **MndwiOp**: Modified Normalized Difference Water Index, allowing for the measurement of surface water extent
- **Mosaic**: Creates a mosaic out of a set of source products.
- **MphChl**: This operator computes maximum peak height of chlorophyll (MPH/CHL).
- **Msavi2Op**: This retrieves the second Modified Soil Adjusted Vegetation Index (MSAVI2).
- **MsaviOp**: This retrieves the Modified Soil Adjusted Vegetation Index (MSAVI).
- **MtciOp**: The Meris Terrestrial Chlorophyll Index estimates the Red Edge Position (REP).
- **Multi-size Mosaic**: Creates a multi-size mosaic out of a set of source products.
- **Multi-Temporal-Speckle-Filter**: Speckle Reduction using Multitemporal Filtering
- **Multilook**: Averages the power across a number of lines in both the azimuth and range directions
- **MultiMasterInSAR**: Multi-master InSAR processing
- **MultiMasterStackGenerator**: Generates a set of master-slave pairs from a coregistered stack for use in SBAS processing
- **Multitemporal-Compositing**: Compute composite image from multi-temporal RTCs
- **Ndi45Op**: Normalized Difference Index using bands 4 and 5
- **NdpiOp**: The normalized differential pond index, combines the short-wave infrared band-I and the green band
- **NdtiOp**: Normalized difference turbidity index, allowing for the measurement of water turbidity
- **NdviOp**: The retrieves the Normalized Difference Vegetation Index (NDVI).
- **Ndwi2Op**: The Normalized Difference Water Index, allowing for the measurement of surface water extent
- **NdwiOp**: The Normalized Difference Water Index was developed for the extraction of water features
- **Object-Discrimination**: Remove false alarms from the detected objects.
- **Offset-Tracking**: Create velocity vectors from offset tracking
- **Oil-Spill-Clustering**: Remove small clusters from detected area.
- **Oil-Spill-Detection**: Detect oil spill.
- **OlciAnomalyFlagging**: Adds a flagging band indicating saturated pixels and altitude data overflows
- **OlciO2aHarmonisation**: Performs O2A band harmonisation on OLCI L1b product. Implements update v4 of R.Preusker, June 2020.
- **OlciSensorHarmonisation**: Performs sensor harmonisation on OLCI L1b product. Implements algorithm described in 'OLCI A/B Tandem Phase Analysis'
- **Orientation-Angle-Correction**: Perform polarization orientation angle correction for given coherency matrix
- **Oversample**: Oversample the datset
- **OWTClassification**: Performs an optical water type classification based on atmospherically corrected reflectances.
- **PCA**: Performs a Principal Component Analysis.
- **PduStitching**: Stitches multiple SLSTR L1B product dissemination units (PDUs) of the same orbit to a single product.
- **PhaseToDisplacement**: Phase To Displacement Conversion along LOS
- **PhaseToElevation**: DEM Generation
- **PhaseToHeight**: Phase to Height conversion
- **PixEx**: Extracts pixels from given locations and source products.
- **Polarimetric-Classification**: Perform Polarimetric classification of a given product
- **Polarimetric-Decomposition**: Perform Polarimetric decomposition of a given product
- **Polarimetric-Matrices**: Generates covariance or coherency matrix for given product
- **Polarimetric-Parameters**: Compute general polarimetric parameters
- **Polarimetric-Speckle-Filter**: Polarimetric Speckle Reduction
- **PpeFiltering**: Performs Prompt Particle Event (PPE) filtering on OLCI L1B
- **Principle-Components**: Principle Component Analysis
- **ProductSet-Reader**: Adds a list of sources
- **PssraOp**: Pigment Specific Simple Ratio, chlorophyll index
- **PviOp**: Perpendicular Vegetation Index retrieves the Isovegetation lines parallel to soil line. Soil line has an arbitrary slope and passes through origin
- **Rad2Refl**: Provides conversion from radiances to reflectances or backwards.
- **Radar-Vegetation-Index**: Dual-pol Radar Vegetation Indices generation
- **Random-Forest-Classifier**: Random Forest based classifier
- **RangeFilter**: Range Filter
- **RayleighCorrection**: Performs radiometric corrections on OLCI, MERIS L1B and S2 MSI L1C data products.
- **Read**: Reads a data product from a given file location.
- **ReflectanceToRadianceOp**: The 'Reflectance To Radiance Processor' operator retrieves the radiance from reflectance using Sentinel-2 products
- **ReipOp**: The red edge inflection point index
- **Remodulate**: Remodulation and reramping of SLC
