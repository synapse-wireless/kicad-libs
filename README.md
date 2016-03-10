----- Local Libraries for Kicad -----


** Kicad setup to use these libraries:

1. In eeschema, add "symbols" files to Kicad's "Preferences->Component Libraries":

   NOTE: these settings are stored in the project (.pro) file, so this step is required for each new project.

a) Add the local symbols directory path to the search path list. (use absolute, not relative path)
b) Add all the library files in the symbols\* directory.


2. Copy master kicad footprint libraries from Github to a local directory:

   Note: This step brings all libraries local. We'll use the "PCB Library Tables" dialog,
         which configures a global Kicad config file called fp-lib-table. (see path at top of dialog)

   Note: This file (fp-lib-table) is cached by kicad, so after editing you'll need to completely exit all   
         kicad programs and re-launch to see the changes consistently across tools.

a) Open the "PCB Footprint Editor" and select "Preferences->Footprint Libraries Manager".
b) Remove all the default ('github' plugin) libraries.
c) Choose "Append with Wizard" and select 'Github repository' option, saving a local copy
   to our "kicad_libs/footprints/kicad" directory.
d) Select all libraries from github, and add to global library configuration. This will download
   all libraries to our local directory.
  

3. Add user footprint libraries (still in Footprint Libraries Manager):

a) Choose "Append with Wizard", and select local library directories in "kicad_libs/footprints/***.pretty"
b) Using this dialog, add "Synapse" and "Added" libraries to global configuration


4. Add link to local 3D packages

   NOTE: Each footprint file can include a path to its 3D model. This can be specified relative to
         the KISYS3DMOD environment variable, which we'll leave at default to use the pre-installed 3D packages
         referenced by the master footprint library. Since the relative path seems to only support
         directories _below_ KISYS3DMOD, we will place our local packages under this path.

a) Make a symlink called "local" under the default KISYS3DMOD directory, pointing to our local 3D library.
   Ex: C:\Program Files\KiCad\share\kicad\modules\packages3d>mklink /D local C:\HardwareDev\kicad_libs\packages3d



5. In eeschema, select BOM generator plugin:

   NOTE: When you generate a netlist, Kicad creates an XML file in your project directory which has all the information
         needed to create the BOM. The BOM dialog in eeschema lets you select a 'plugin' to process this XML file,
         typically into a CSV output format.

a) Open the BOM dialog, and select "Add Plugin".
b) Browse to local library and choose "kicad_libs/scripts/bom-in-python/bom_csv_grouped_by_value.py"
c) In the "Command Line" input box, append .csv to the command string. Should end with  "%O".csv


