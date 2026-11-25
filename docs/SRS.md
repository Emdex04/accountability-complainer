# AccountabilityComplainer — Software Requirements Specification (open-source edition)

**Version:** 2.0-oss · **Date:** 25 November 2026 · **Owner:** Muokwe Matai

> This is the public, general-market edition. The private edition also has an LSU (Learning Support) mode for schools, which is not part of this repository.

## 1. Purpose
A single-page web tool for writing text (requirements, observations, complaints, incident or maintenance reports) and attaching photos, video and audio to it automatically. Each file goes either at the exact point the writer marks in the text or into an Attachments section at the end. The finished report exports as Word, PDF, HTML, or a full package (.zip) that includes all of these plus the media files.

## 2. Users
Facility managers, landlords and tenants, contractors, QA inspectors, school and office administrators, project owners writing requirements, and anyone who needs a clear report with evidence attached in the right place.

## 3. Media format decision

| Format | Photos | Video | Audio | Best for |
|--------|--------|-------|-------|----------|
| HTML | Inline | Plays inline | Plays inline | Reading on screen; sharing by email or chat apps |
| Word (.docx) | Inline | Still frame + caption + link | Caption + link | Editing and official records |
| PDF | Inline | Still frame + caption + link | Caption + link | Printing and filing |
| Full package (.zip) | All of the above | `media/` folder | `media/` folder | Recommended whenever video or audio is present |

Why: Word and PDF cannot reliably play embedded media across devices, so in those formats each video becomes a still frame plus a link, and the media files travel alongside the report.

## 4. Functional requirements

| ID | Requirement |
|----|-------------|
| FR-01 | Enter a document title, author and free text |
| FR-02 | A line starting with `# ` becomes a heading |
| FR-03 | Upload several photos, videos or audio files by button or drag-and-drop |
| FR-04 | Separate editable maximum sizes: images 2 MB, video 50 MB, audio 15 MB |
| FR-05 | Oversized images are shrunk (resized and recompressed to JPEG) or rejected, by user choice. Oversized video or audio is rejected with advice |
| FR-06 | Markers `[[img-N]]`, `[[vid-N]]`, `[[aud-N]]`. "Insert here" places a marker at the cursor |
| FR-07 | Dragging or pasting a file into the text uploads it and places its marker at the cursor |
| FR-08 | A marked file is placed right after the sentence or paragraph containing its marker |
| FR-09 | Unmarked files go into "Attachments" at the end (can be turned off) |
| FR-10 | Separate numbering for each type (Figure, Video, Audio), with durations and editable captions |
| FR-11 | A still frame is grabbed from each video. A placeholder still is used if the browser can't decode the video |
| FR-12 | Files can be reordered (changes their order in Attachments) and removed. Removing a file also removes its markers |
| FR-13 | Live preview with inline playback |
| FR-14 | Word (.docx) export with embedded images, video stills and clickable media links |
| FR-15 | PDF export (A4) with images, video stills and media links |
| FR-16 | HTML export with all media embedded. Warns when media exceeds 80 MB |
| FR-17 | Full package (.zip): .docx, .pdf, an .html that points to the media files, the `media/` folder, and READ-ME.txt |
| FR-18 | Templates: Requirements, Observation report, Complaint/incident, Facility check |
| FR-19 | Text draft kept in the browser (localStorage) between visits |
| FR-20 | Optional voice dictation and saving when running inside a Claude artifact (feature-detected; hidden elsewhere) |

## 5. Non-functional requirements
- Single static `index.html`. No backend and no build step. Hostable on GitHub Pages.
- All processing happens on the device. Nothing is uploaded.
- Responsive layout that stacks below 900px. Light and dark themes. 44px touch targets and visible focus.
- External dependencies: JSZip 3.10.1 and jsPDF 2.5.1 from cdnjs.

## 6. Testing
On 25 Nov 2026, in headless Chrome (Playwright) with a PNG, an MP4 and a WAV: adding files, placing markers inline, sending unplaced files to Attachments, and all four exports. The .docx opened in python-docx with 2 inline images. The PDF text was extracted and checked, and the zip contents were verified.

## 7. Known limits
- No video compression in the browser.
- Some iPhone HEVC `.mov` files won't preview in Chrome on Windows.
- Media isn't kept after a reload.
- The PDF uses Helvetica, which only covers Latin-1 characters.
- Word and PDF links to media only work while the files sit in the unzipped package folder.

## 8. Roadmap
- Save and reopen projects with media (IndexedDB)
- Logo, letterhead and reference numbers
- Bold, italics and bullet lists
- Photo timestamps for evidence-grade reports
- PWA install for offline use on phones

## 9. Change log
| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-11-25 | Text editor, image placement, size limit and auto-shrink, captions, DOCX/PDF/HTML export |
| 2.0-oss | 2026-11-25 | Video and audio, per-type limits, video stills, inline playback, media-aware exports, full package (.zip); first public release |
