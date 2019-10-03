---
title: Page Numbering Addon - LibreOffice/OpenOffice
date: '2018-08-29T18:51:58+03:00'
draft: false
description: Easy page numbering for LibreOffice/OpenOffice with intuitive user interface.
tags:
  - python
  - libreoffice
  - addon
  - open_source
  - gsoc2018
---
## Introduction

This is a plugin for LibreOffice/OpenOffice developed during my time as a student developer for Google Summer of Code 2018. I still casually maintain the addon, although the time I can dedicate for such projects is getting reduced day by day. The addon is already used by a great number of users worldwide, translated in many languages (that would be many more if I had the time to standardize the whole localization process but that's a whole different story to tell), and at the time of writing is the second most popular extension in [LibreOffice Extensions](https://extensions.libreoffice.org/extensions), and the first most popular Writer extension.

This project belongs to my favorite ones, mainly because it started as a personal tool and grew bigger than I ever expected.

![](https://extensions.libreoffice.org/extensions/page-numbering-addon/@@images/screenshot/large)


## Implementation

LibreOffice extension development is mainly documented for LO Basic, a language I was never proficient with. I first developed a prototype in LibreOffice Basic, mainly because it provides an abstractrion layer for LibreOffice API. For the final version, I used Python while maintaining the Basic version for older LibreOffice/OpenOffice versions that did not support Python extensions. However, I now only maintain the Python one.

## Features

* Add page numbering simplifying the previous page-break approach:
 
  Although Page Breaks are an intuitive and effective approach for document layout and styling, users migrating from Microsoft Office suites find it more than difficult to understand)

* Configure styling options such as Font, Character height, Alignment and page position (Header/Footer)

* Page offset and First page options

* Numbering type selection such as Roman, Arabic or Greek

* Multiple Page numbering setups per document

## Download

Page Numbering Addon can be found either in this repository or at the following links:

* [LibreOffice Official Extensions](https://extensions.libreoffice.org/extensions/page-numbering-addon).
* [Apache OpenOffice Extensions](https://extensions.openoffice.org/en/project/page-numbering-addon)

## Contribute

If you like to contribute in any way, please head to the following repository:

* [GitLab](https://gitlab.com/lo_extensions/lo-page-numbering)
