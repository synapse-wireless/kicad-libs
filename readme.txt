Kicad setup to use these libraries:

1. In eeschema, add "symbols" files to Kicad's "Preferences->Component Libraries".
* Add the symbols directory path to the search path list. (use absolute, not relative path)
* Add the library files in the symbols\* directory.

2. Copy master kicad footprint libraries from Github to local directory.
   Note: This step brings all libraries local. Brings up the "PCB Library Tables" dialog,
         which configures a text file called fp-lib-table. (path at top of dialog)
   Note: This file (fp-lib-table) is cached by kicad, so after editing you'll need to completely exit all   
         kicad programs and re-launch to see the changes consistently.
* Open the "PCB Footprint Editor" and select "Preferences->Footprint Libraries Manager".
* Remove all the default 'github' plugin libraries. (fetched on demand)
* Choose "Append with Wizard" and select 'Github repository' option, saving a local copy
  to our "kicad_libs/footprints/kicad" directory.
* Select all libraries from github, and add to global library configuration. This will download
  all libraries to our local directory.
  
3. Add user footprint libraries (still in Footprint Libraries Manager)
* Choose "Append with Wizard", and select local library directories in "kicad_libs/footprints/***.pretty"

4. Add link to local 3D packages
* Each footprint file can include a path to its 3D model. This can be specified relative to KISYS3DMOD environment variable,
  but the relative path must be below that directory path. (can't use ../local/)
* Make a symlink called "local" under the default KISYS3DMOD directory, pointing to our local 3D library.
  Ex: C:\Program Files\KiCad\share\kicad\modules\packages3d>mklink /D local C:\HardwareDev\kicad_libs\packages3d



