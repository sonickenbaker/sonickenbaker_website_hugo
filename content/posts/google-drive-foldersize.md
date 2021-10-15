---
title: "Google Drive Foldersize"
date: 2021-10-15T17:25:25+02:00
draft: false
---
Getting the size of a Google Drive folder is not a trivial task. Google does not provide a method from the GDrive UI to get that info. Even by using the Classes provided by Google Apps Script you don't have that info exposed.
\
\
So I made this function that calculate the size of a folder:
{{< gist sonickenbaker 0a366db19e00caae4dfc308798475873 >}}
Function gets a [Folder Class](https://developers.google.com/apps-script/reference/drive/folder?hl=en) item as input and recursively traverse it to calculate the sum of all the files contained in it.
You can use it like that:
```js
function main() {
  // select folders that are not in the Bin and contains
  // the keyword 'a_keyword' in the description field
  var folders = DriveApp.searchFolders('(trashed != true) and (fullText contains "a_keyword")');
  var folder_size = 0;
  while (folders.hasNext()) {
    var folder = folders.next();
    Logger.log("Folder: %s - Size: %s", folder.getName(), getFolderSize(folder));
  }
}
```
