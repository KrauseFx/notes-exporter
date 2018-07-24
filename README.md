# Early WIP, not ready to be used yet

# Apple Notes Exporter

GDPR defines the `Right to data portability`, but for some reason this hasn't fully reached iCloud.com yet.

I was fully aware that this is an issue, but I liked the Notes app, so I learned to live with the fact I'm locked into the Apple Notes system.

At some point I noticed how some notes are not properly synced. After further investigation, turns out, my notes haven't properly synced in months, and my iPhone and my 2 Macs are completely out of sync. 

But hey, Apple of course follows GDPR, and they offer a great way to export notes

https://support.apple.com/en-us/HT204055#note

> To copy notes, open the Notes app on your Mac or at iCloud.com. Copy the text of each note and paste it into a document on your computer, such as a Pages or TextEdit document. Save the document to your computer.

With over 2,000 notes, this seems slightly inefficient.

There is a closed-source Mac app available: [Exporter](https://itunes.apple.com/us/app/exporter/id1099120373?mt=12) that exports your Mac Notes as markdown files, but it doesn't do all the things I need it to do.

## What this tool can do

- [x] Export all your Apple Notes into Markdown files
- [x] Set the Creation and Modified data of each file
- [x] Group the exported files into folders
- [x] Store all notes into one directory to import into Bear Notes
- [ ] Automatically detect duplicate files
- [ ] Merge multiple Notes databases into one
- [x] Include the folder name as hashtag for Bear
- [x] Fully open source, customize as you want

## What it doesn't do

- Export images, you'll need to manually copy those over

## Installation

```
git clone https://github.com/KrauseFx/notes-exporter
cd notes-exporter
bundle update
```

## Usage

```
bundle exec ruby export.rb
```

## How to import into Bear

- `File` -> `Import Notes`
- Open the `all_notes`
- Check the following boxes in the `Options`
  - `Keep the original creation and modificiation date`
  - `Use first line as title`
