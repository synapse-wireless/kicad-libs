[![](https://cloud.githubusercontent.com/assets/1317406/12406044/32cd9916-be0f-11e5-9b18-1547f284f878.png)](http://www.synapse-wireless.com/)

# Synapse KiCad Part Libraries

## Setup

1. In eeschema, add "symbols" files to KiCad's "Preferences->Component Libraries":

   **Note**: these settings are stored in the project (.pro) file, so this step is required for each new project.

   1. Add the local symbols directory path to the search path list. (use absolute, not relative path)
   1. Add all the library files in the symbols\* directory.


1. Copy master KiCad footprint libraries from GitHub to a local directory:

   **Note**: This step brings all libraries local. We'll use the "PCB Library Tables" dialog, which configures a global KiCad config file called fp-lib-table. (see path at top of dialog)

   **Note**: This file (fp-lib-table) is cached by KiCad, so after editing you'll need to completely exit all KiCad programs and re-launch to see the changes consistently across tools.

   1. Open the "PCB Footprint Editor" and select "Preferences->Footprint Libraries Manager".
   1. Remove all the default ('github' plugin) libraries.
   1. Choose "Append with Wizard" and select 'Github repository' option, saving a local copy to our "kicad_libs/footprints/kicad" directory.
   1. Select all libraries from GitHub, and add to global library configuration. This will download all libraries to our local directory.
  
1. Add user footprint libraries (still in Footprint Libraries Manager):

   1. Choose "Append with Wizard", and select local library directories in "kicad_libs/footprints/***.pretty"
   1. Using this dialog, add "Synapse" and "Added" libraries to global configuration

1. Add link to local 3D packages

   **Note**: Each footprint file can include a path to its 3D model. This can be specified relative to
         the KISYS3DMOD environment variable, which we'll leave at default to use the pre-installed 3D packages
         referenced by the master footprint library. Since the relative path seems to only support
         directories _below_ KISYS3DMOD, we will place our local packages under this path.

   1. Make a symlink called "local" under the default KISYS3DMOD directory, pointing to our local 3D library.
      Ex: C:\Program Files\KiCad\share\kicad\modules\packages3d>mklink /D local C:\HardwareDev\kicad_libs\packages3d

1. In eeschema, select BOM generator plugin:

   **Note**: When you generate a netlist, KiCad creates an XML file in your project directory which has all the information
         needed to create the BOM. The BOM dialog in eeschema lets you select a 'plugin' to process this XML file,
         typically into a CSV output format.

   1. Open the BOM dialog, and select "Add Plugin".
   1. Browse to local library and choose "kicad_libs/scripts/bom-in-python/bom_csv_grouped_by_value.py"
   1. In the "Command Line" input box, append .csv to the command string. Should end with  "%O".csv


