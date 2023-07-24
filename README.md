# pdf-toc - add table of contents entries to a PDF file

This script provides three command-line methods to assist the process
of creating and editing true table of contents entries in PDF files.

## Background

There exist so many very excellent FOSS applications to annotate and
edit PDF files, but nothing to simply edit a PDF file's true table of
contents. See below for some FOSS projects that have what for me are
too-complicated workflows and which try to guess a file's table of
contents for you.

## Dependencies

* pdftk - https://gitlab.com/pdftk-java/pdftk  
   Probably already packaged in your distribution's repositories

* awk - http://www.gnu.org/software/gawk/  
   Probably already installed on your computer

## Usage
       pdf-toc batch PDF-FILE [dump|update] [TOC-FILE]
       pdf-toc add PDF-FILE [dump] [update] page N [level N] DESCRIPTION
       pdf-toc [dump|update] PDF-FILE [METADATA-FILE]
       pdf-toc --help-long"

1. Method / workflow #1

   Use the 'batch dump' command to output a PDF file's current table of
contents entries, if any, in an easy-to-edit format TOC-FILE. Then
edit the TOC-FILE and use the 'batch update' command to install your
changes. The TOC-FILE format (one line per entry) is: PAGE-NUMBER
LEVEL-NUMBER DESCRIPTION. The fields are space-delimited and
DESCRIPTION need not be quoted. TOC-FILE defaults to the pdf filename,
but with a '.batch' extension.

2. Method / workflow #2

   Use the 'add' command to have the script add a single TOC entry. Some
features of the 'add' command:

   * The addition is placed in its page position, after other entries
   that might exist for the same page.

   * DESCRIPTION should be quoted if it contains spaces, etc.

   * The 'level' keyword and number are optional and default to 1.

   * If the command finds a text file in the current directory with the
   same basename as PDF_FILE, it will assume that file is the metadata
   file, and will perform its edit on that file. For large PDF files,
   this will save a lot of processing time. You can force the script
   to perform a new data dump, which will overwrite the current text
   file, by specifying the optional parameter 'dump'.

   * By default, the command only edits the metadata text file, but does
   not update the PDF file. For large PDF files, this can save a lot
   of processing time if you are performing multiple additions. You
   can specify the optional 'update' parameter to have the script also
   update the PDF file after performing an individual edit.

   * The script doesn't care in what sequence you specify parameters
   'dump', 'update', 'page N', 'level N', or 'DESCRIPTION'.

3. Method / workflow #3

   Use the 'dump' command to generate a text file of the complete PDF
metadata. Then edit the file and use the 'update' command to alter the
PDF file itself. METADATA-FILE defaults to the pdf filename, but with
a '.txt' extension. The format of a table of contents entry in that
file is:
```
    BookmarkBegin
    BookmarkTitle: YOUR_TITLE
    BookmarkLevel: INTEGER
    BookmarkPageNumber: INTEGER
```
Yes, the nomenclature is confusing. Complain to the committee who
decided on it, decades ago.

## Alternatives

* Emacs package doc-tools-toc
  https://github.com/dalanicolai/doc-tools-toc

* tocPDF
  https://github.com/aminya/tocPDF

## Colophon
Copyright: © 2023, Boruch Baum <boruch_baum@gmx.com>  
License: GPLv3: Use at your own risk.
