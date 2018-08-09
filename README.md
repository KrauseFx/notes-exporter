# Apple Notes Exporter

GDPR defines the `Right to data portability`, but for some reason this hasn't fully reached iCloud.com yet.

I was fully aware that this is an issue, but I liked the Notes app, so I learned to live with the fact I'm locked into the Apple Notes system.

At some point I noticed how some notes are not properly synced. After further investigation, turns out, my notes haven't properly synced in months, and my iPhone and my 2 Macs are completely out of sync. 

But hey, Apple of course follows GDPR, and they offer a great way to export notes

https://support.apple.com/en-us/HT204055#note

> To copy notes, open the Notes app on your Mac or at iCloud.com. Copy the text of each note and paste it into a document on your computer, such as a Pages or TextEdit document. Save the document to your computer.

With over 2,000 notes, this seems slightly inefficient.

There is a closed-source Mac app available: [Exporter](https://itunes.apple.com/us/app/exporter/id1099120373?mt=12) that exports your Mac Notes as markdown files, but it doesn't do all the things I need it to do.

I took 2 approaches for this, the one at the bottom doesn't work with the new iCloud format.

## Keyboard Maestro based exporter

I was able to implement a complete migration for all my notes using [Keyboard Maestro](https://www.keyboardmaestro.com/main/). It uses copy and paste directly into Bear Notes, resulting in all images to be copied over also. It takes a long time to run (I left it running over night), but the result was good and the script was stable. The trickiest piece of the script was to update the Modified Date of each note to the original one, which could only be done directly through the sqlite database of Bear Notes. 

While Bear Notes also uses iCloudKit, at least you can easily export all your notes into any format (e.g. Markdown, HTML)

[Open Notes2Bear.kmmacros](https://raw.githubusercontent.com/KrauseFx/notes-exporter/master/Notes2Bear.kmmacros), download it by hitting `CMD` + `S` and opening it up with [Keyboard Maestro](https://www.keyboardmaestro.com/main/).

1. Open the Notes app and click on the `Edit date` until it shows the modified date
1. Open Bear to view all the Notes (not a folder)
1. Open "All iCloud" in the Notes app.
1. Make sure to add one line of the last note in the list to this workflow (bottom of workflow) so the script knows when to stop
1. Make sure to have your Notes app unlocked in case you have any encrypted notes, as otherwise the script will be interrupted

## [Deprecated] Database exporter

At first, I built a Ruby script that exports all the notes by accessing the SQLite database directly. The database contained all your notes as HTML text, so it was easy to convert them from HTML to markdown. However as it turns out, Apple migrated to a new format, and just left the old database file on your machine. When I looked into the new database format, it seems like the data is stored encrypted, and I couldn't figure out how to access it (yeah data lock-in, this is great), even if your notes aren't encrypted using the password protection UI.

### What this tool can do

- [x] Export all your Apple Notes into Markdown files
- [x] Set the Creation and Modified data of each file
- [x] Group the exported files into folders
- [x] Store all notes into one directory to import into Bear Notes
- [ ] Automatically detect duplicate files
- [ ] Merge multiple Notes databases into one
- [x] Include the folder name as hashtag for Bear
- [x] Fully open source, customize as you want

### What it doesn't do

- Export images, you'll need to manually copy those over

### Installation

```
git clone https://github.com/KrauseFx/notes-exporter
cd notes-exporter
bundle update
```

### Usage

```
bundle exec ruby export.rb
```

### How to import into Bear

- `File` -> `Import Notes`
- Open the `all_notes`
- Check the following boxes in the `Options`
  - `Keep the original creation and modificiation date`
  - `Use first line as title`
