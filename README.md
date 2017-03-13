# Larc: The Literotica Archiver

This is a small program to extract stories from Literotica that uses [FanFicFare](https://github.com/JimmXinu/FanFicFare) to extract stories into epub form. 

## Features

* You can specify only the categories you want larc to download in a file, one per line.
* Can extract all stories from each category in the category file, and supports multiple threads for category page processing.
* Supports downloading 'new' stories, and will only download ones that belong to a category you have told larc to download. This means after downloading every story in every category you want, you can progromatically keep your archive up-to-date, without processing every page in every category over and over again, redownloding and rewriting stories you already have.  Note that 'new' page parsing is single-threaded.
* Supports multiple download worker threads (which call fanficfare), so you can download many stories at once. This works whether you are downloading stories from the 'new stories' pages, or from all categories in the category file.  Please respect the Literotica servers and don't set the number of download workers very high.
* Can output all Literotica categories, commented, to a file; you can then uncomment (remove the number in front) the ones you want downloaded.
* Can optionally zip up the archive directory after downloading stories.
* Supports your tipical '--quiet' and '--verbose' options for choosing how much information gets reported to the screen.

## Installation

First, do the normal git clone or download a [zip file](https://github.com/Oliver2213/larc/archive/master.zip).
Once you have the project directory you can simlink the larc script to E.G. /home/you/bin/larc on *nix systems, or add the directory to your path on windows so you can call larc from anywhere.

## Example Usage

Larc is a program designed to get specific categories from Literotica; as such it needs to know what categories you would like for it to download. Larc can output a list of all Literotica categories for you with the '--output-categories' or '-oc' option. Run it like:
```
larc --output-categories le_categories
```
This will create a text file called le_categories in your current directory. Each line is the name of a category. All categories are commented out with a # by default; remove the comment from in front of the ones you want it to download.

Once you have a file with your categories, you can start downloading. Larc has 2 modes for this:
* '--download-categories' or '--categories': In this mode, larc will methodically go through each category you've selected, get all the stories in it and tell worker threads about them so it can download them and place them in the correct locations (larc creates category directories where their respective stories get saved). **This should only be used once**. This mode is very time consuming and puts the Literotica servers under heavy load (it requests *every* story in *every* category you've selected as well as every part and page of that story), so only use it when you first build your archive.
* '--download-new' or '--new': This mode uses Literotica's 'new stories' pages to get stories that have recently changed. Category selecctions still apply here, so after you first get stories with '--download-categories', you can keep them up-to-date with this mode. 

So a complete way to use larc looks like this:
```
larc --output-categories ./le_categories
larc --download-categories ./le_categories # Will output stories to a directory called literotica by default and take a long time...
# later...
larc --new ./le_categories # Will update stories and again output to a directory called literotica
```

For more help on larc's various options and usage, use the '--help' option.

## History

This was originally going to be a small, simple script that outsourced almost everything to `fanficfare`, a nice fanfiction / story downloader for several sites. As things progressed though, I realized that features I was considering adding in the future weren't supported by fanficfare, such as only downloding stories of a specific category, etc. I then noticed that the option in fanficfare that extracts urls from a page that might lead to stories was too broad, so I added code to parse category pages, the 'new stories' page, and then added options for those modes.