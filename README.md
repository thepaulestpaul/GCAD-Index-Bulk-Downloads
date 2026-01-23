# GCAD-Index-Bulk-Downloads

This script is no longer functional due to the implementation
of cloudflair on guncadindex. You can thank the perpetrators of a recent
ddos attack for that.

Workaround to be published soon.

Update: automated cloudflair workaround has been added but not tested. Feel free to give it a whirl. Will test and debug this weekend as time allows. 


# !!! IMPORTANT - MUST READ !!!

 ******The scripts and other files in this repository automatically download files listed on GunCAD Index which is a search engine for DIY gun designs. It is not for children.****** By downloading or utilizing by any other means any of the content located in or linked to this repository, including but not limited to: scripts and other types of files, or by any accessing  [guncadindex.com](https://guncadindex.com/) by any other means, you acknowledge and agree that:

   - You are at least 18 years of age

   - You have read and agree to the GunCad Index site's terms and policies outlined here: https://guncadindex.com/legal
   
   - You understand that firearm-related information (including but not limited to design files) may be regulated in your jurisdiction
   
   - You are legally permitted, under all applicable laws and regulations, to access and possess information about DIY firearms
     
   - If you are a resident of a jurisdiction that restricts access to or dissemination of firearm-related technical information, you affirm that you are exempt from such restrictions or otherwise legally authorized to access it. Such jurisdictions may include, but are not limited to:
     
     -   California
     -   New Jersey
     -   New York
     
   - You are **solely responsible** for ensuring your compliance with all applicable laws
     
   - GunCAD Index does not **host, control, or distribute any linked content.** It is purely an index and search engine. You access any sites linked on [guncadindex.com](https://guncadindex.com/) directly or via or any other means at your own risk and are subject to their terms and policies

******If you do not understand and agree to the above, please **navigate away from this repository, and do not download, attempt to download, or otherwise utilize any of the content within it********


#




# GunCAD Index Downloader v6

A comprehensive Python script for downloading, organizing, and cataloging files from the GunCAD Index. Features intelligent file organization, Excel metadata tracking, and robust duplicate detection.

## 🎯 Features

### Smart Download Management
- **Incremental Downloads**: Re-run the script anytime to download only new files - already downloaded files are automatically skipped
- **Duplicate Detection**: Three-layer duplicate checking using LBRY URLs, Exel tracking, and filesystem scanning
- **Resume Capability**: Failed downloads can be retried on subsequent runs

### Intelligent File Organization
- **Intent-Based Categorization**: Files are organized by purpose, not just tags
  - Complete firearms builds (Handguns, Rifles, PCCs, Shotguns)
  - Individual parts (Frames, Uppers, Slides, Barrels, etc.)
  - Accessories (Suppressors, Magazines, Optics, Grips)
  - Tools and Jigs (Bending, Drilling, CNC fixtures)
- **Automatic Folder Structure**: Creates logical directory hierarchy based on gun model, caliber, and part type
- **README Generation**: Auto-generates README.md files in each folder with file inventories

### Comprehensive Metadata Tracking
- **Excel Master Index**: `GunCAD_Master_Index.xlsx` containing all file metadata:
  - File name, location, download date
  - LBRY and Odysee URLs
  - Release date, author, version
  - Last updated timestamp
  - Odysee engagement metrics (views, likes, dislikes)
  - Full descriptions, notes, and readme content
  - Gun model, caliber, part type classification
  - Complete tag listings
- **CSV Fallback**: Generates CSV if Excel library unavailable
- **Quick Find Guide**: `QUICK_FIND.txt` for fast navigation

### Quality of Life Features
- **Configurable Output Directory**: Choose your download location at startup
- **Adjustable Download Quantity**: Download 25 files or all 25,000+ files
- **Tag Filtering**: Exclude unwanted categories (furniture, accessories, jigs, etc.)

### File Verification
- **ZIP Validation**: Tests zip file integrity
- **Format Detection**: Recognizes CAD formats (STL, STEP, 3MF, OBJ, etc.)
- **Size Verification**: Confirms downloaded file sizes match expected values

## 📋 Requirements

### Software Dependencies
- **Python 3.7+** (tested on Python 3.8-3.11)
- **LBRY Desktop Application** (CRITICAL - see setup below)
- **Python Libraries**:
```
  requests
  openpyxl (for Excel generation)
```

### System Requirements
- **Disk Space**: 100GB+ recommended (full collection is ~500GB)
- **RAM**: 4GB minimum, 8GB+ recommended
- **Internet**: Stable broadband connection (downloads can be large)

## 🔧 Installation

### 1. Install Python Dependencies
```bash
pip install requests openpyxl
```

### 2. Install and Configure LBRY Desktop (CRITICAL)

**⚠️ The script REQUIRES LBRY Desktop to be running - it cannot download files without it!**

#### Download LBRY Desktop:
- **Windows/Mac/Linux**: [https://lbry.com/get](https://lbry.com/get)

#### Setup Steps:
1. Install LBRY Desktop application
2. Launch LBRY Desktop
3. Complete initial setup (create wallet, etc.)
4. **Keep LBRY Desktop running in the background** - the script communicates with it via API
5. Verify it's working:
   - LBRY Desktop should show "Connected" status
   - Default API endpoint: `http://localhost:5279`

#### Troubleshooting LBRY:
- **"LBRY daemon not available" error**: LBRY Desktop is not running
- **Firewall issues**: Ensure port 5279 is not blocked
- **Slow downloads**: LBRY uses P2P - speed varies based on seeders

### 3. Download the Script

Save `guncad_downloader_v6_fixed.py` to your desired location.

## 🚀 Usage

### Basic Usage
```bash
python guncad_downloader_v6_fixed.py
```

The script will guide you through:
1. **Output Directory**: Where to save files (default: `GunCAD_Downloads`)
2. **Download Quantity**: How many pages to download (25 files per page)
   - `1` = 25 files (quick test)
   - `10` = 250 files
   - `999` = Everything available (~25,000 files)
3. **Tag Filtering** (optional): Exclude categories you don't want
   - Example: `Furniture,Accessory` to skip furniture and accessories

### Interactive Prompts Explained
```
OUTPUT DIRECTORY CONFIGURATION
Default directory: GunCAD_Downloads
Press Enter to use default, or type a custom path:
> [Press Enter or type path]

DOWNLOAD QUANTITY
How many pages to download? (25 files per page)
> 10  [Downloads 250 files]

TAG FILTER (OPTIONAL)
Exclude files with specific tags (comma-separated)
> Furniture,Magazine,Jig  [Skips these categories]
```

### Re-running for New Files

Simply run the script again! It will:
- Load your existing Excel index
- Check LBRY URLs against downloaded files
- Download only new files added since last run
- Update the Excel index with new entries

## 📁 Output Structure
```
GunCAD_Downloads/
│
├── Complete_Firearms/
│   ├── Handguns/
│   │   ├── Glock_Clones/
│   │   │   ├── Glock_19/
│   │   │   │   ├── README.md
│   │   │   │   └── [files]
│   │   ├── 1911_Clones/
│   │   └── Other_Handguns/
│   ├── Rifles/
│   │   ├── AR-15_Builds/
│   │   ├── AR-22_Builds/
│   │   ├── AK_Builds/
│   │   └── Other_Rifles/
│   ├── PCCs/
│   └── Shotguns/
│
├── Parts_and_Upgrades/
│   ├── Frames_and_Receivers/
│   ├── Uppers_and_Slides/
│   ├── Fire_Control/
│   └── Barrels_and_Bolts/
│
├── Accessories/
│   ├── Suppressors/
│   ├── Magazines/
│   ├── Optics_and_Sights/
│   └── Grips_and_Stocks/
│
├── Tools_and_Jigs/
├── Furniture/
├── Miscellaneous/
│
├── GunCAD_Master_Index.xlsx  ← Main database
├── QUICK_FIND.txt             ← Navigation guide
└── download_history.json      ← Internal tracking
```

## 📊 Excel Master Index Columns

The generated Excel file contains 21 columns:

| Column | Description |
|--------|-------------|
| File Name | Original filename |
| Location | Full path to file |
| LBRY URL | Unique LBRY identifier |
| Detail URL | GunCAD Index detail page |
| Category | Organized folder path |
| Gun Model | Detected firearm model |
| Caliber | Detected caliber/gauge |
| Part Type | Component classification |
| Tags | All GunCAD tags |
| File Size (MB) | File size in megabytes |
| **Release Date** | Original release date |
| Last Updated | Most recent update |
| **Author** | Creator/uploader |
| **Version** | Version number if available |
| Date Downloaded | When you downloaded it |
| Odysee Views | View count on Odysee |
| Odysee Likes | Like count |
| Odysee Dislikes | Dislike count |
| **Description** | Full description text |
| Notes | Release notes | this needs to be removed or updated
| Readme | Readme content | this needs to be removed or updated

**Bold** = metadata fields that were recently fixed

## 🎛️ Advanced Configuration

### Custom API Endpoint
If LBRY Desktop uses a different port:
```python
# Edit line ~1200 in the script
lbry = LBRYDaemonClient(daemon_url='http://localhost:CUSTOM_PORT')
```

### Batch Update Interval
Change how often Excel updates (default: every 10 downloads):
```python
# Edit line ~1390
BATCH_UPDATE_INTERVAL = 10  # Change to desired number
```

### Download Timeout
Adjust maximum wait time per file:
```python
# Edit LBRYDaemonClient initialization
max_wait_time = 300  # Seconds (default: 5 minutes)
```

## 🔍 Troubleshooting

### "LBRY daemon not available"
- **Solution**: Launch LBRY Desktop application
- Verify it's running by visiting: `http://localhost:5279`

### Downloads are very slow
- **Cause**: LBRY uses peer-to-peer downloads - speed depends on seeders
- **Solution**: Be patient, or skip slow files and retry later

### Excel file won't open
- **Cause**: File may be open in Excel, or openpyxl not installed
- **Solution**: 
  - Close Excel
  - Install: `pip install openpyxl`
  - Use CSV fallback: `GunCAD_Master_Index.csv`

### Files downloaded to wrong location
- **Cause**: Script uses LBRY's default download folder initially
- **Note**: Files are automatically moved to organized folders after download

### "Missing metadata columns"
- This is a current bug, the next release will contain a fix

### Out of disk space
- **Solution**: 
  - Use tag filtering to exclude categories
  - Download fewer pages
  - Increase available storage

## 🤝 Contributing

Found a bug? Have a feature request?

1. Check existing issues on GitHub
2. Create detailed bug report with:
   - Error messages
   - Python version
   - LBRY Desktop version
   - Steps to reproduce

## 📜 License

This script is provided as-is for educational and archival purposes. 

**Important Legal Notes**:
- Respect all applicable laws regarding firearms and related items
- Some designs may be subject to export controls or regulations
- Users are responsible for compliance with local, state, and federal laws
- This tool is for archival and educational purposes only

## ⚠️ Disclaimer

This software is provided "AS IS" without warranty of any kind. The authors are not responsible for:
- How this software is used
- Legal compliance of downloaded content
- Any damages or legal issues arising from use

Users must ensure they comply with all applicable laws and regulations.

## 🙏 Credits

- **GunCAD Index**: [https://guncadindex.com](https://guncadindex.com)
- **LBRY Protocol**: [https://lbry.com](https://lbry.com)
- Original script concept and development: Community effort

## 📞 Support

- **GunCAD Index Issues**: Contact GunCAD Index maintainers
- **LBRY Issues**: Visit [LBRY Discord](https://discord.gg/lbry)
- **Script Issues**: GitHub Issues section

---

**Version**: 6.0 (Fixed Metadata Edition)  
**Last Updated**: January 2025  
**Status**: Active Development
