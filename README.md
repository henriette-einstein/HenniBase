# HenniBase

HenniBase is a personal knowledge management vault built in [Obsidian](https://obsidian.md). It uses a structured directory layout, typed notes with YAML frontmatter, and a Zettelkasten layer for developing original thought. This document explains how the vault is organised and where different kinds of information belong.

## Directory Structure

```
HenniBase/
├── 00 Inbox/            Unprocessed notes and quick captures
├── 10 Journal/          Daily notes (organised by year: YYYY/YYYY-MM-DD.md)
├── 20 Projects/         Active projects with dedicated folders
├── 30 Areas/            Ongoing areas of interest and responsibility
├── 40 Ressources/       Reference material and entity notes
│   ├── Cities/          City profiles (e.g. London, Brussels)
│   ├── Countries/       Country profiles (e.g. United Kingdom)
│   ├── Events/          Historical events with date ranges (e.g. Suez Crisis (1956))
│   ├── Locations/       Regions, continents, points of interest
│   ├── Notes/           General-purpose documents (FAQ, How-To, Instructions)
│   ├── Organizations/   Institutions, companies, parties (e.g. NATO)
│   ├── Persons/         Biographical notes (e.g. Anthony Eden)
│   ├── Terms/           Glossary definitions (e.g. Rentier State)
│   └── Timelines/       Chronological sequences of events
├── 50 Zettelkasten/     Permanent knowledge store
│   ├── Zettel/          Atomic notes: one idea per note, in your own words
│   ├── Essays/          Longer texts synthesised from multiple Zettel
│   └── MOCs/            Maps of Content for navigation and curation
├── 60 Sources/          Bibliography and source notes
│   ├── Articles/        Journal and web articles
│   ├── Audio/           Podcasts and audio recordings
│   ├── Books/           Book notes (filename: Author - Title.md)
│   ├── Documentations/  Technical documentation
│   └── Videos/          Video sources
├── 80 Media/            Binary attachments
│   ├── Images/          Image files
│   ├── PDFs/            PDF documents
│   └── Webarchives/     Archived web pages
└── 90 System/           Vault infrastructure (do not edit manually)
    ├── Bases/           Obsidian base files for the vault
    ├── Templates/       Note templates for each type
    └── Types/           Type definitions used in YAML frontmatter
```

## Where to Put Things

**I captured a quick thought or link.** Drop it into `00 Inbox/`. Process it later into the appropriate folder.

**I want to record facts about a real-world entity** (a person, city, country, organisation, event, or term). Create a typed note in the matching subfolder of `40 Ressources/`. Each note has YAML frontmatter that declares its type, creation date, and type-specific fields.

**I want to write down my own idea or insight.** Create a Zettel in `50 Zettelkasten/Zettel/`. Zettel are atomic (one idea per note), written in your own words, and linked to other notes. They answer the question "What do I think about this?" as opposed to Term notes, which answer "What does this word mean?"

**I want to connect several Zettel into a larger argument.** Write an Essay in `50 Zettelkasten/Essays/`. Mini-essays run 500 to 1500 words with a single argument. Normal essays run 1500 to 5000 words with multiple threads.

**I want a navigational overview of a topic.** Create a Map of Content (MOC) in `50 Zettelkasten/MOCs/`. MOCs collect and organise links to related notes across the vault. Filename convention: `MOC <Title>` for general maps, `Topic <Title>` for topic-focused ones.

**I want to take notes on a book, article, or video.** Create a source note in the matching subfolder of `60 Sources/`. Book filenames follow the pattern `Author - Title.md`.

**I have an ongoing responsibility or interest area.** Create an Area note in `30 Areas/`.

**I'm working on a bounded project with a clear goal.** Create a Project in `20 Projects/`.

## Note Types at a Glance

| Type         | Folder                       | Key YAML Fields                                |
| ------------ | ---------------------------- | ---------------------------------------------- |
| Person       | 40 Ressources/Persons/       | born, died, country, categories                |
| Event        | 40 Ressources/Events/        | **start, end** (required), where, participants |
| Organization | 40 Ressources/Organizations/ | founded, dissolved, headquarter                |
| City         | 40 Ressources/Cities/        | country, location (GPS)                        |
| Country      | 40 Ressources/Countries/     | **capital** (required), flag, location         |
| Location     | 40 Ressources/Locations/     | categories, location (GPS), country            |
| Term         | 40 Ressources/Terms/         | aliases                                        |
| Timeline     | 40 Ressources/Timelines/     | start, end                                     |
| Note         | 40 Ressources/Notes/         | tags                                           |
| Zettel       | 50 Zettelkasten/Zettel/      | tags, sources                                  |
| Essay        | 50 Zettelkasten/Essays/      | categories, status, topics                     |
| MOC          | 50 Zettelkasten/MOCs/        | categories, summary                            |
| Source       | 60 Sources/...               | authors, published, rating                     |
| Book         | 60 Sources/Books/            | authors, isbn, pages, publisher, cover         |
| Area         | 30 Areas/                    | (standard fields)                              |

Every note requires three YAML fields: `type`, `created`, and `modified`. The `type` field is always a wikilink to the type definition (e.g. `type: "[[Person]]"`).

## Writing Conventions

All notes are written in prose. Bullet points are reserved for true enumerations (member lists, data collections) and the Overview section of Country notes. The Connections section at the end of each note uses the format `- [[Link]] – Brief description`.

Event filenames include the year or period in parentheses (e.g. `Suez Crisis (1956)`, `World War I (1914-1918)`). Book filenames follow the pattern `Author - Title.md`.

## The 90 System Folder

The `90 System/` folder contains templates and type definitions that power the vault's structure. These files should not be edited manually unless you are changing the vault's schema. When creating a new note, use the matching template from `90 System/Templates/` or let the CLI tool handle it.
