# Google Images Download
======================

Python Script for `searching` and `downloading` hundreds of Google images to the local hard disk!

### Summary

This is a command line python program to search keywords/key-phrases on Google Images and optionally download images to your computer. You can also invoke this script from another python file.

This is a small and ready-to-run program. No dependencies are required to be installed if you would only want to download up to 100 images per keyword. If you would want **more than 100 images** per keyword, then you would need to install `Selenium` library along with `chromedriver`. Detailed instructions in the troubleshooting section.

### Compatibility
This program is compatible with both the versions of python - `2.x` and `3.x` (recommended). It is a download-and-run program with no changes to the file. You will just have to specify parameters through the command line.

### Installation
You can use **one of the below methods** to download and use this repository.

##### Using pip

``` {.sourceCode .bash}
$ pip install google_images_download
```

##### Manually using CLI

``` {.sourceCode .bash}
$ git clone https://github.com/pourabkarchaudhuri/google-image-scraper.git
$ cd google-image-scraper && sudo python setup.py install
```

### Usage - From another python file

If you would want to use this library from another python file, you could use it as shown below:

``` {.sourceCode .python}
from google_images_download import google_images_download

response = google_images_download.googleimagesdownload()
absolute_image_paths = response.download({<Arguments...>})
```
\
**Note:** If `single_image` or `url` parameter is not present, then keywords is a mandatory parameter. No other parameters are mandatory.

### Config File Format

You can either pass the arguments directly from the command as in the examples below or you can pass it through a config file. Below is a sample of how a config file looks.

You can pass more than one record through a config file. The below sample consist of two set of records. The code will iterate through each of the record and download images based on arguments passed.

``` {.sourceCode .json}
{
    "Records": [
        {
            "keywords": "apple",
            "limit": 5,
            "color": "green",
            "print_urls": true
        },
        {
            "keywords": "universe",
            "limit": 15,
            "size": "large",
            "print_urls": true
        }
    ]
}
```

### Examples

-   If you are calling this library from another python file, below is the sample code

``` {.sourceCode .python}
from google_images_download import google_images_download   #importing the library

response = google_images_download.googleimagesdownload()   #class instantiation

arguments = {"keywords":"Polar bears,baloons,Beaches","limit":20,"print_urls":True}   #creating list of arguments
paths = response.download(arguments)   #passing the arguments to the function
print(paths)   #printing absolute paths of the downloaded images
```

-   If you are passing arguments from a config file, simply pass the config\_file argument with name of your JSON file

``` {.sourceCode .bash}
$ googleimagesdownload -cf example.json
```

-   Simple example of using keywords and limit arguments

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "Polar bears, baloons, Beaches" --limit 20
```

-   Using Suffix Keywords allows you to specify words after the main keywords. For example if the `keyword = car` and `suffix keyword = 'red,blue'` then it will first search for `car red` and then `car blue`

``` {.sourceCode .bash}
$ googleimagesdownload --k "car" -sk 'red,blue,white' -l 10
```

-   To use the short hand command

``` {.sourceCode .bash}
$ googleimagesdownload -k "Polar bears, baloons, Beaches" -l 20
```

-   To download images with specific image extension/format

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "logo" --format svg
```

-   To use color filters for the images

``` {.sourceCode .bash}
$ googleimagesdownload -k "playground" -l 20 -co red
```

-   To use non-English keywords for image search

``` {.sourceCode .bash}
$ googleimagesdownload -k "北极熊" -l 5
```

-   To download images from the google images link

``` {.sourceCode .bash}
$ googleimagesdownload -k "sample" -u <google images page URL>
```

-   To save images in specific main directory (instead of in 'downloads')

``` {.sourceCode .bash}
$ googleimagesdownload -k "boat" -o "boat_new"
```

-   To download one single image with the image URL

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "baloons" --single_image <URL of the images>
```

-   To download images with size and type constrains

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "baloons" --size medium --type animated
```

-   To download images with specific usage rights

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "universe" --usage_rights labeled-for-reuse
```

-   To download images with specific color type

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "flowers" --color_type black-and-white
```

-   To download images with specific aspect ratio

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "universe" --aspect_ratio panoramic
```

-   To download images which are similar to the image in the image URL that you provided (Reverse Image search).

``` {.sourceCode .bash}
$ googleimagesdownload -si <image url> -l 10
```

-   To download images from specific website or domain name for a given keyword

``` {.sourceCode .bash}
$ googleimagesdownload --keywords "universe" --specific_site example.com
```

===\> The images would be downloaded in their own sub-directories inside the main directory (either the one you provided or in 'downloads') in the same folder you are in.

* * * * *

Troubleshooting Errors/Issues
-----------------------------

**\#\~\~\~\# SSL Errors**

If you do see SSL errors on Mac for Python 3, please go to Finder —\> Applications —\> Python 3 —\> Click on the ‘Install Certificates.command’ and run the file.

**\#\~\~\~\# googleimagesdownload: command not found**

While using the above commands, if you get `Error: -bash: googleimagesdownload: command not found` then you have to set the correct path variable.

To get the details of the repo, run the following command:

``` {.sourceCode .bash}
$ pip show -f google_images_download 
```

you will get the result like this:

``` {.sourceCode .bash}
Location: /Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages
Files:
  ../../../bin/googleimagesdownload
```

together they make: `/Library/Frameworks/Python.framework/Versions/2.7/bin` which you need add it to the path:

``` {.sourceCode .bash}
$ export PATH="/Library/Frameworks/Python.framework/Versions/2.7/bin"
```

**\#\~\~\~\# [Errno 13] Permission denied creating directory 'downloads'**

When you run the command, it downloads the images in the current directory (the directory from where you are running the command). If you get permission denied error for creating the downloads directory, then move to a directory in which you have the write permission and then run the command again.

**\#\~\~\~\# Permission denied while installing the library**

On MAC and Linux, when you get permission denied when installing the library using pip, try doing a user install.

``` {.sourceCode .bash}
$ pip install google_images_download --user
```

You can also run pip install as a superuser with `sudo pip install google_images_download` but it is not generally a good idea because it can cause issues with your system-level packages.

**\#\~\~\~\# Installing the chromedriver (with Selenium)**

If you would want to download more than 100 images per keyword, then you will need to install 'selenium' library along with 'chromedriver' extension.

If you have pip-installed the library or had run the setup.py file, Selenium would have automatically installed on your machine. You will also need Chrome browser on your machine. For chromedriver:

[Download the correct chromedriver](https://sites.google.com/a/chromium.org/chromedriver/downloads) based on your operating system.

On **Windows** or **MAC** if for some reason the chromedriver gives you trouble, download it under the current directory and run the command.

On windows however, the path to chromedriver has to be given in the following format:

`C:\\complete\\path\\to\\chromedriver.exe`

On **Linux** if you are having issues installing google chrome browser, refer to this [CentOS or Amazon Linux Guide](https://intoli.com/blog/installing-google-chrome-on-centos/) or [Ubuntu Guide](https://askubuntu.com/questions/510056/how-to-install-google-chrome%20in%20documentation)

For **All the operating systems** you will have to use '--chromedriver' or '-cd' argument to specify the path of chromedriver that you have downloaded in your machine.

If on any rare occasion the chromedriver does not work for you, try downgrading it to a lower version.

Structure
---------

Below diagram represents the algorithm logic to download images.

![](http://www.zseries.in/flow-chart.png)


Disclaimer
----------

This program lets you download tons of images from Google. Please do not download or use any image that violates its copyright terms. Google Images is a search engine that merely indexes images and allows you to find them. It does NOT produce its own images and, as such, it doesn't own copyright on any of them. The original creators of the images own the copyrights.

Images published in the United States are automatically copyrighted by their owners, even if they do not explicitly carry a copyright warning. You may not reproduce copyright images without their owner's permission, except in "fair use" cases, or you could risk running into lawyer's warnings, cease-and-desist letters, and copyright suits. Please be very careful before its usage!
