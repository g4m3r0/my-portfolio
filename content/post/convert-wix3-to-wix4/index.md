---
title: Converting WiX Toolkit v3 XML Code to WiX Toolkit v4
subtitle: WiX Toolkit has undergone significant changes between v3 and v4, with improvements in the delivery model, MSBuild project support, and command-line tools.

# Summary for listings and search engines
summary: WiX Toolkit has undergone significant changes between v3 and v4, with improvements in the delivery model, MSBuild project support, and command-line tools.

# Link this post with a project
projects: []

# Date published
date: '2023-04-27T12:00:00Z'

# Date updated
lastmod: '2023-04-27T12:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Wix
  - Wix4

categories:
  - Wix4
---

WiX Toolkit has undergone significant changes between v3 and v4, with improvements in the delivery model, MSBuild project support, and command-line tools. To transition from WiX v3 to WiX v4, you'll need to convert your existing WiX v3 authoring to the new WiX v4 language. This short guide will walk you through the process of converting your WiX v3 XML code to WiX v4 using the `wix convert` command. [firegiant.com](https://www.firegiant.com/wix/tutorial/upgrading-to-wix-v4/)

## **Prerequisites**

Before you begin, ensure you have the following installed:

1. WiX v4 .NET tool: Install the WiX v4 .NET tool by following the instructions in the [WiX v4 documentation](https://wixtoolset.org/documentation/manual/v4/getting_started/).
2. Version control: Make sure your WiX v3 source code is in a version control system, so you can easily revert any changes made by `wix convert` if necessary.

## **Converting WiX v3 to WiX v4**

Once you have the WiX v4 .NET tool installed, you can use the `wix convert` command to convert your WiX v3 authoring to WiX v4. [firegiant.com](https://www.firegiant.com/wix/tutorial/upgrading-to-wix-v4/)

### **Converting Individual WiX Source Files**

To convert a single WiX v3 source file to WiX v4, run the following command:

```bash
wix convert path\to\file.wxs
```

Replace `path\to\file.wxs` with the path to your WiX v3 source file. [firegiant.com](https://www.firegiant.com/wix/tutorial/upgrading-to-wix-v4/)

### **Converting All WiX Source Files in a Directory**

To convert all WiX v3 source files in a specified directory, run the following command:

```bash
wix convert --recurse path\to\directory
```

Replace `path\to\directory` with the path to the directory containing your WiX v3 source files. [firegiant.com](https://www.firegiant.com/wix/tutorial/upgrading-to-wix-v4/)

### **Performing a Dry Run**

By default, `wix convert` overwrites the original files with the converted versions. If you want to see the changes `wix convert` would make without actually modifying the files, use the `--dry-run` switch:

```bash
wix convert --dry-run path\to\file.wxs
```

Replace `path\to\file.wxs` with the path to your WiX v3 source file. [firegiant.com](https://www.firegiant.com/wix/tutorial/upgrading-to-wix-v4/)

## **Conclusion**

Converting your WiX v3 XML code to WiX v4 using `wix convert` is a straightforward process. With the WiX v4 .NET tool installed and your source code in version control, you can easily convert individual files or entire directories. Remember to use the `--dry-run` switch if you want to preview the changes before overwriting your original files. Happy converting!
