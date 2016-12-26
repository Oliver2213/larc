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

## History

This was originally going to be a small, simple script that outsourced almost everything to `fanficfare`, a nice fanfiction / story downloader for several sites. As things progressed though, I realized that features I was considering adding in the future weren't supported by fanficfare, such as only downloding stories of a specific category, etc. I then noticed that the option in fanficfare that extracts urls from a page that might lead to stories was too broad, so I added code to parse category pages, the 'new stories' page, and then added options for those modes.