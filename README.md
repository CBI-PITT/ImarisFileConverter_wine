# ImarisFileConverter_wine

This repository contains ImarisFileConverter(s) that are verified to work with [wine](https://www.winehq.org/) on linux.

Only verified on: Ubuntu 22.04 server

## Installation Notes:

This is designed to work with [wine](https://www.winehq.org/) for linux (no sudo required): 

```bash
git clone https://github.com/wine-mirror/wine.git #or specific commit
cd to/cloned/directory

./configure --enable-win64 --without-x --without-freetype

# On Ubuntu 22.04 server you may need to: "apt-get install flex bison"

make -j22 #(j = # of threads that you want to use to build wine)
```

Now that wine is compiled, you need to show wine where to find data in linux so that ImarisFileConverter can be used to convert files located on linux mount points. This is done adding a soft link to the editing the dosdevices directory located in the "users_home_directory/.wine/dosdevices"

```bash
cd ~/.wine/dosdevices
```

We will add the following linux mount points to windows:

| Linux Mount Point | Windows Drive Letter | Command                 |
| ----------------- | -------------------- | ----------------------- |
| /CBI_FastStore    | f:\                  | ln -s /CBI_FastStore f: |
| /h20              | h:\                  | ln -s /h20 h:           |



### Install of specific versions of ImarisFileConverter:

#### v10.2.0:

Specific commit of wine verified to work with with version

https://github.com/wine-mirror/wine/tree/2bca8cb236b7d4d5f4e0e35d6fcad6a1d8a2c5e3)



## Command examples

**NOTE:** 

Calling the converter can be done with linux paths

```bash
/h20/home/lab/src/wine/wine64 /h20/home/lab/src/ImarisFileConverter_wine/10.2.0/ImarisConvert.exe
```

Files referenced by the ImarisConvert.exe must be expressed in windows drive letter locations. Use "" because of the "\\"

```bash
"h:\file\location\my_image.tif"
```



### Help:

```bash
/h20/home/lab/src/wine/wine64 /h20/home/lab/src/ImarisFileConverter_wine/10.2.0/ImarisConvert.exe --help

# Wine will throw warnings and errors but this does not effect functionality

#EXAMPLE OUTPUT FOR --help:
0158:fixme:nls:RtlGetThreadPreferredUILanguages 00000038, 00007FFFFE1FF254, 00007FFFFE1FF270 00007FFFFE1FF250
0158:fixme:nls:get_dummy_preferred_ui_language (0x38 0x409 00007FFFFE1FF254 00007FFFFE1FF270 00007FFFFE1FF250) returning a dummy value (current locale)
0158:fixme:file:NtLockFile I/O completion on lock not implemented yet
016c:fixme:file:NtLockFile I/O completion on lock not implemented yet
016c:fixme:process:SetProcessShutdownParameters (00000100, 00000001): partial stub.
0170:err:winediag:nodrv_CreateWindow Application tried to create a window, but no driver could be loaded.
0170:err:winediag:nodrv_CreateWindow L"The graphics driver is missing. Check your build!"

Imaris Convert 10.2.0  [Jun 18 2024] Build 67164 for x64
Usage: ImarisConvert.exe -i "retina.ome" -o "retina.ims"

  Argument Name:                   Argument Description:             Argument Value:
  -h   |--help                     This help screen                  -
  -v   |--version                  Print Version                     -
  -i   |--input                    Input File Name                   (required: filename)
  -mi  |--inputlist                Input File Contains List of Files (default: no)
  -if  |--inputformat              Input File Format                 (default: autodetect)
  -ii  |--inputindex               Input File Image Index            (files with multiple images, default: 0)
  -ic  |--inputcrop                Crop Input File Image             (default: do not crop - MinX,MaxX,MinY,MaxY,MinZ,MaxZ,MinC,MaxC,MinT,MaxT

                                                                     0 defaults to min or max, resp.)
  -il  |--inputlayout              Apply layout to file series       (default: no layout - filename
  -vs  |--voxelsize                Set Voxel Size                    (default: empty - read from file)
  -vx  |--voxelsizex               Set Voxel Size in X dimension     (default: empty - read from file)
  -vy  |--voxelsizey               Set Voxel Size in Y dimension     (default: empty - read from file)
  -vz  |--voxelsizez               Set Voxel Size in Z dimension     (default: empty - read from file)
  -o   |--output                   Output File Name                  (default: empty - do not generate)
  -t   |--thumbnail                Thumbnail File Name               (TIFF image, use thumbnail arguments multiple times for multiple thumbnai
ls)
  -tb  |--tbackground              Thumbnail Background Color        (#RRGGBBAA, default: system window color)
  -tm  |--tmode                    Thumbnail Mode                    (default: Automatic - Slice|MiddleSlice|MaxIntensity|MinIntensity|Automat
ic)
  -ts  |--tsize                    Thumbnail Image Size X and Y      (default: size of input image)
  -tl  |--tlimit                   Thumbnail Image Size Max X,Y      (default: 1024, or input image size if smaller)
  -th  |--ttimepoint               Thumbnail Image Time point        (default: 0)
  -tz  |--tSliceIndexZ             Thumbnail Image z slice           (default: 0)
  -tf  |--tformat                  Thumbnail Image output format     (default: png - tiff|jpeg (75:1 quality) )
  -to  |--timeout                  Timeout in seconds                (default: no timeout)
  -ti  |--tointerval               Throughput output interval in ms  (default: 0 - no throughput output)
  -a   |--allfiles                 Show Attached Files               (default: empty - do not generate. -a [filename])
  -m   |--metadata                 Show Image Meta Data              (default: empty - do not generate. -m [filename])
  -x   |--voxelhash                Show Voxel Hash Code              (default: empty - do not generate. -x [filename])
  -d   |--descriptors              Show Image Descriptors            (default: empty - do not generate. -d [filename])
  -xs  |--vblocksort               Block reading sequence            (n|t - default is t, n=no, t=time)
  -l   |--log                      Log into file                     (default: to stdout - filename|"none")
  -lp  |--logprogress              Log R/W progress to stdout        (default: do not log progress)
  -nt  |--nthreads                 Set number of compression threads (default: 8)
  -f   |--formats                  Get supported file formats        -
  -ff  |--fileformats              Show supported file formats       -
  -c   |--compression              Compression level                 (default: 2)
  -ch  |--colorhint                Color hint                        (default: ColorLUTHint - ColorLUTHint|ColorEmissionHint|ColorDefaultHint)

  -frp |--filereaderplugins        File Reader Plugins Path          (default: empty - no plugins)
  -dcl |--defaultcolorlist         Default color list                (4 #RRGGBB colors that apply to first, second, third and other channels)
  -fsdx|--fileseriesdelimitersx    File series delimiters X          (X delimiters to apply to configurable file formats, colon separated)
  -fsdy|--fileseriesdelimitersy    File series delimiters Y          (Y delimiters to apply to configurable file formats, colon separated)
  -fsdz|--fileseriesdelimitersz    File series delimiters Z          (Z delimiters to apply to configurable file formats, colon separated)
  -fsdc|--fileseriesdelimitersc    File series delimiters C          (C delimiters to apply to configurable file formats, colon separated)
  -fsdt|--fileseriesdelimiterst    File series delimiters T          (T delimiters to apply to configurable file formats, colon separated)
  -fsdf|--fileseriesdelimitersf    File series delimiters F          (F delimiters to apply to configurable file formats, colon separated)

Input File Formats are:

  ImarisSceneFile Bitplane: Imaris Scene File - (IMX;IMS)
  Imaris3         Bitplane: Imaris 3.0 - (IMS)
  Imaris          Bitplane: Imaris 2.7 - (IMS)
  AndorIQ         Andor: iQ ImageDisk - (KINETIC)
  Andor           Andor: Multi-TIFF (Series) - (TIF;TIFF)
  DeltaVision     Applied Precision: DeltaVision - (R3D;DV)
  Biorad          Biorad: MRC (series) - (PIC)
  Aztec           Oxford instruments: Aztec - (H5OINA)
  Witec           Oxford instruments: Witec - (H5OIWT)
  IPLab           BioVision: IPLab IPL (series) - (IPL)
  IPLabMac        BioVision: IPLab IPM - (IPM)
  Gatan           Gatan: DigitalMicrograph (series) - (DM3)
  CXD             Hamamatsu Compix: SimplePCI - (CXD)
  SlideBook       Intelligent Imaging Innovations: SlideBook - (SLD;SLDY;SLDYZ)
  MRC             IMOD: MRC - (MRC;ST;REC)
  LeicaLif        Leica: Image File Format LIF - (LIF)
  LeicaLof        Leica: Image File Format LOF - (LOF)
  LeicaXlef       Leica: Experiments Structure in Multiple Files XLEF - (XLEF)
  LeicaSingle     Leica: TCS-NT - (TIF;TIFF)
  LeicaSeries     Leica: Series - (TIF;TIFF;INF;INFO)
  LeicaVista      Leica: Vista LCS - (TIF;TIFF;LEI;RAW)
  MicroManager    Micro-Manager: Image5D - (TIF;TIFF;TXT)
  MetamorphSTK    Molecular Devices: MetaMorph STK (series) - (STK)
  MetamorphND     Molecular Devices: MetaMorph ND - (ND)
  ICS             Nikon: Image Cytometry Standard ICS - (ICS;IDS)
  NikonND2        Nikon: ND2 - (ND2)
  OlympusCellR    Olympus: cellR - (TIF;TIFF)
  OlympusOIB      Olympus: FluoView OIB - (OIB)
  OlympusOIF      Olympus: FluoView OIF - (OIF)
  OlympusOIR      Olympus: FluoView OIR - (OIR)
  Olympus         Olympus: FluoView TIFF - (TIF;TIFF)
  OlympusVSI      Olympus: VSI - (VSI;TIF)
  Prairie         Prairie Technologies: Prairie View - (XML;CFG;TIF;TIFF)
  GEInCell6000    GE: InCell 6000 - (TIF;TIFF;XDCE)
  PhaseView       Phase View - (TIF;TIFF)
  AuroxOmeTiff    Aurox Open Microscopy Environment: TIFF - (OME)
  OmeTiff         Open Microscopy Environment: TIFF - (TIF;TIFF;TF8)
  ImageJTiff      TIFF ImageJ (adjustable file series) - (TIF;TIFF)
  OmeXml          Open Microscopy Environment: XML - (OME)
  OpenlabLiff     PerkinElmer: Improvision Openlab LIFF (series) - (LIFF)
  OpenlabRaw      PerkinElmer: Improvision Openlab RAW - (RAW)
  PerkinElmer2    PerkinElmer: UltraView - (TIM;ZPO)
  Till            TILL Photonics: TILLvisION - (RBINF)
  AxioVision      Zeiss: AxioVision / ZVI - (ZVI)
  Lsm510          Zeiss: LSM710, LSM510 - (LSM)
  Lsm410          Zeiss: LSM410, LSM310 - (TIF;TIFF)
  BmpSeries       BMP (adjustable file series) - (BMP)
  TiffSeries      TIFF (adjustable file series) - (TIF;TIFF)
  ZeissCZI        Zeiss: CZI (series) - (CZI)
  AbberiorOBF     Abberior Instruments: OBF/MSR - (OBF;MSR)
  AperioSVS       Aperio (SVS, TIF): single-file pyramidal tiled TIFF - (SVS;TIF)
  DICOMSeries     DICOM file format (series) - (;DCM)
  HamamatsuNDPI   Hamamatsu NDPI - (NDPI)
  Imaris5         Bitplane: Imaris 5.5 - (IMS)
  BigDataViewer   Big Data Viewer - (XML;H5)

Output File Formats are:

  Imaris5 Bitplane: Imaris 5.5 - (ims)

Exit Codes:

  0 - Success (no error)
  2 - Invalid Arguments
  3 - Unknown File Type
  99 - Timeout
  4 - Abnormal Termination

Examples:

> ImarisConvert.exe -i "Leica_serie2.lif" -ii 1 -o "Leica_serie2_conv_1.ims"

Reads "Leica_serie2.lif" as "lif" file.
If "Leica_serie2.lif" contains more than one image the option "-ii" specifies the
index of the source image (index counting starts with 0).

> ImarisConvert.exe -i "retina.ims" -m "retina.imi"

Extracts all image meta data of the file. The resulting "retina.imi" contains
file name(s), image names, desctiptions, image size, channel information etc.
The data in the output file is structured by XML tags.

> ImarisConvert.exe -i "retina.ims" -x "retina.x"

Reads all voxel data of the file, and calculates a hash-code. The resulting
"retina.x" contains the voxel-hash-code as XML

> ImarisConvert.exe -i "retina.lif" -ii 2 -t "retina.tif" -ts 128

If "retina.lif" contains more than one image the option "-ii" specifies the
index of the source image (index counting starts with 0). The output is a
compressed tiff-image image with 128 x 128 pixels. If the option "-ts" is not
specified, the output image has the same size as the original image.

0158:fixme:msvcrt:__clean_type_info_names_internal (00006FFFFF5C75C8) stub
0158:fixme:msvcrt:__clean_type_info_names_internal (00007FFFFE6A16E8) stub
0158:fixme:msvcrt:__clean_type_info_names_internal (00007FFFFE6CC8A8) stub
0158:fixme:msvcrt:__clean_type_info_names_internal (000000001223B088) stub
0158:fixme:msvcrt:__clean_type_info_names_internal (00006FFFFF2573F8) stub
0158:fixme:msvcrt:__clean_type_info_names_internal (00007FFFFE455618) stub
```



### Examples of file conversions:

```bash
/h20/home/lab/src/wine/wine64 /h20/home/lab/src/ImarisFileConverter_wine/10.2.0/ImarisConvert.exe --voxelsizex 1 --voxelsizey 1 --voxelsizez 1 -i "h:\file\location\my_image.tif" -o "h:\file\out\location\my_image.ims" --logprogress --nthreads 24 --compression 6

# Outputs will show scrolling progress
```

Single file conversions can require special considerations if they are a part of a larger series of files stored in the same directory. It may require that a layout file be produced. For the example above, make the following .xml file:

```xml
#h:\file\location\layout_file.xml

<FileSeriesLayout>
    <ImageIndex name="h:\file\location\my_image.tif" x="0" y="0" z="0" c="0" t="0"/></FileSeriesLayout>
```

Then run the command:

```bash
/h20/home/lab/src/wine/wine64 /h20/home/lab/src/ImarisFileConverter_wine/10.2.0/ImarisConvert.exe --voxelsizex 1 --voxelsizey 1 --voxelsizez 1 -i "h:\file\location\my_image.tif" -o "h:\file\out\location\my_image.ims" --logprogress --nthreads 24 --compression 6 -il "h:\file\location\layout_file.xml"
```

Multi-file conversions will require a layout file. Here is an example:

```xml
#h:\img\layout_file.xml

<FileSeriesLayout>
<ImageIndex name="f:\img\composite_z000_c405.tif" x="0" y="0" z="0" c="0" t="0"/>
<ImageIndex name="f:\img\composite_z000_c561.tif" x="0" y="0" z="0" c="1" t="0"/>
<ImageIndex name="f:\img\composite_z001_c405.tif" x="0" y="0" z="1" c="0" t="0"/>
<ImageIndex name="f:\img\composite_z001_c561.tif" x="0" y="0" z="1" c="1" t="0"/>
<ImageIndex name="f:\img\composite_z002_c405.tif" x="0" y="0" z="2" c="0" t="0"/>
<ImageIndex name="f:\img\composite_z002_c561.tif" x="0" y="0" z="2" c="1" t="0"/>
<ImageIndex name="f:\img\composite_z003_c405.tif" x="0" y="0" z="3" c="0" t="0"/>
<ImageIndex name="f:\img\composite_z003_c561.tif" x="0" y="0" z="3" c="1" t="0"/>
<ImageIndex name="f:\img\composite_z004_c405.tif" x="0" y="0" z="4" c="0" t="0"/>
<ImageIndex name="f:\img\composite_z004_c561.tif" x="0" y="0" z="4" c="1" t="0"/></FileSeriesLayout>
```

Then run the command:

```bash
/h20/home/lab/src/wine/wine64 /h20/home/lab/src/ImarisFileConverter_wine/10.2.0/ImarisConvert.exe --voxelsizex 1 --voxelsizey 1 --voxelsizez 1 -i "f:\img\composite_z000_c405.tif" -o "f:\img\converted_volume.ims" --logprogress --nthreads 24 --compression 6 -il "h:\img\layout_file.xml"
```



## Installing other versions of ImarisFileConverter not included in this repo:

If you are trying to install a new version of ImarisFileConverter that is not in this repository, install the application on windows first. Then copy the entire install directory to the linux system that has wine installed. Verify that it is working on windows first. Now try running "ImarisConvert.exe --help". It may complain that it can not find some .dll files (often found here for win11: C:\Windows\SysWOW64  or  C:\Windows\System32).  Example: "mfc140.dll". Copy the .dll(s) to the ImarisFileConverter folder and try again.

