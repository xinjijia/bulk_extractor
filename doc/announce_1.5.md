                    Announcing bulk_extractor 1.5.
                             June 1, 2014
                                DRAFS

bulk_extractor Version 1.5 has been released for Linux, MacOS and Windows.

New functionality in Version 1.5 includes:

* scan_outlook will decrypt "Outlook Compressible Encryption" used on some PST files. 

* scan_sqlite ---- SQLite database carving (Note: only works for unfragmented databases)



Improvements
============

Improvements in existing scanners:
----------------------------------

Version 1.5 allows you to specify one of three SSN recognition modes:

    -S ssn_mode=0  SSN’s must be labeled “SSN:”. Dashes or no dashes okay.
    -S ssn_mode=1  No “SSN” required, but dashes are required.
    -S ssn_mode=2  No dashes required. Allow any 9-digit number that matches SSN allocation range.

Improvements in Python programs:
--------------------------------

* Minor improvements to regress.py


Incompatiable changes:
----------------------

Overreporting Fixes:
-------------------

We have further improved overreporting problems:

* scan_base16 is now disabled by default.

Underreporting Fixes
---------------------

Bug Fixes
---------

Usability Improvement
----------------------

Internal Improvements
--------------------- 

* introduced an atomic set and histogram to minimize the use of
  cppmutexes in the callers. 

* bulk_extractor is now distributed as both an executable and as a
  library. The library called from C or Python as a shared lib


PERFORMANCE 
============

This section tracks how performance of bulk_extractor has changed over
time.  We update it with each new release

NOTE: We recommend compiling Version 1.4 with -O3 under GCC. Please
use version GCC 4.7 or above. 

Use these configure flags to compile with a different optimization: 

  --without-opt           Drop all -O C flags
  --without-o3            Do not force O3 optimization; use default level



    Disk image: /corp/nps/drives/nps-2009-ubnist1/ubnist1.gen3.E01
                /corp/nps/drives/nps-2009-ubnist1/ubnist1.gen3.E02

                Media size:         1.9 GiB (2106589184 bytes)
                MD5:                49a775d8b109a469d9dd01dc92e0db9c
            
    Hardware:   MacBook Pro 2 Ghz Intel Core i7, 8GB 1333 Mhz DDR3
                512GB SSD (Simson's Laptop "Mucha"), 

Current and Historic Times with no tuning [1]: 

MacOS 10.8.0; LLVM build 2336.11.00; -O3

```
version 1.4:    144 seconds (14.59 MBytes/sec)  (-O3; )
version 1.3:    185 seconds (11.34 MBytes/sec)  (-O3; )
version 1.2.0:  141 seconds (14.9 MBytes/sec)   (-O3; )
version 1.1.3:  171 seconds (12.3 MBytes/sec)   (-O3; AES disabled)
version 1.0.7:  256 seconds (8.22 MBytes/sec)   (-O3; AES disabled; 

MacOS 10.7.8; LLVM build 2336.1.00; No optimization

version 1.2.0:  350 seconds (5.72 MBytes/sec)
version 1.1.3:  468 seconds (4.28 MBytes/sec)

Windows 7, same hardware ("boot camp"):

version 1.4: TBD
version 1.3:    198 seconds (10.6 MBytes/sec)  (-O3; AES enabled; 32bit)
version 1.3:    186 seconds (11.33 MBytes/sec)  (-O3; AES enabled; 64bit)
version 1.2.0:  207.4 seconds (9.69 MBytes/sec, [2])

Notes: 
1 - Times reported are the fastest of three consecutive runs
2 - bulk_extractor 1.2.0 scan_exiv was disabled under Windows
```

Current list of bulk_extractor scanners:

```
scan_accts   - Looks for phone numbers, credit card numbers, etc
scan_aes     - Detects in-memory AES keys from their key schedules
scan_ascii85 - TBD
scan_base16  - decodes hexadecimal test
scan_base64  - decodes BASE64 text
scan_bulk    - TBD     
scan_elf     - Detects and decodes ELF headers
scan_exif    - 
scan_exiv2   - Decodes EXIF headers in JPEGs using libexiv2 (for regression testing)
scan_email   - 
scan_exif    - Decodes EXIF headers in JPEGs using built-in decoder.
scan_find    - keyword searching
scan_gps     - Detects XML from Garmin GPS devices
scan_gzip    - Detects and decompresses GZIP files and gzip stream
scan_hashid
scan_hiber   - Detects and decompresses Windows hibernation fragments
scan_outlook - Decrypts Outlook Compressible Encryption
scan_json    - Detects JavaScript Object Notation files
scan_kml     - Detects KML files
scan_lightgrep
scan_net     - IP packet scanning and carving
scan_pdf     - Extracts text from some kinds of PDF files
scan_rar
scan_vcard   - Carvees VCARD files
scan_windirs - TBD
scan_winpe   -
scan_winprefetch - Extracts fields from Windows prefetch files and file fragments.
scan_wordlist - Builds word list for password cracking
scan_xor
scan_zip     - Detects and decompresses ZIP files and zlib streams
```

Current list of bulk_extractor feature files:

```
aes_keys.txt - AES encryption keys
alerts.txt   - Features found on alert list (redlist)
ccn.txt      - credit card numbers
ccn_track2.txt - Track 2 information
domain.txt   - All extracted domain names and IP addresses
email.txt    - extracted email addresses
ether.txt    - extracted ethernet addresses. Currently
               overcollecting due to a failure to consider
               local context.
exif.txt     - All exif fields from JPEGs; extracted as XML.
find.txt     - Hits on find command.
hex.txt      - Notable hexdecimal constants
gps.txt      - Extracted GPS coordinates from Garmin XML and
               GPS-enabled JPEG files
ip.txt       - Extracted IP addresses from scan_net
               cksum-bad indicates checksum test failed;
               those are less likely to actually be IP
               addresses.
json.txt     - Extracted and validated JavaScript Object
               Notation fragments.
kml.txt      - Extracted KML files
rar.txt      - 
report.xml   - The DFXML file that explains what happened.
rfc822.txt   - All extracted RFC822 headers
tcp.txt      - Summaries of all extracted UDP and TCP packets.
telephone.txt- Extracted phone numbers
url.txt      - Extracted URLs
  url_facebook-id - extracted Facebook IDs
  url_microsoft-live - extracted Microsoft Live IDs
  url_searches       - extracted search terms
  url_services       - extracted services from URLs
winprefetch.txt - Windows prefetch files and fragments,
                  recoded as XML for easy processing.
wordlist.txt - All the words 
zip.txt      - Information about all ZIP files and zip
               components.
```

Current list of carving directories:
```
unrar/
jpeg/
unzip/
```


Planned for 1.5:
================
The following are planned for 1.5 but have not been integrated yet:


* replace as many and sets maps as possible with unordered equivallent (performance improvement)

* identify_filenames should present the % of disk that has allocated files.

* Python Bridge. 

* Reporting into an sqlite database instead of or in addition to feature files

Future Plans
============

* scanner to remove all XML tags (extracts text from .docx files)

* improvements to identify_filename so it can run on a report in place.

* Find more false positives with CCN validator by scanning through XOR data

* Lnk File decoder (http://msdn.microsoft.com/en-us/library/dd871305.aspx)
  for automatically detecting and reporting Window shortcut files.

* xz, 7zip, and LZMA/LZMA2 decompression

* BZIP2 decompression

* CAB decompression

* Scanning for the start of bitlocker protected volumes.

* NTFS decompression

* Better handling of MIME encoding

* Reimplement top-n with a priority queue, rather than a sort and subset

* Process more data with -e xor and look for CCN hits. Most will be false positives

* Demonstration of bulk_extractor running on a grid (how fast can it run?)
