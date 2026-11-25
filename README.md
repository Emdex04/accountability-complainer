# AccountabilityComplainer

**Write the report first. Drop in the evidence. It lands exactly where you point.**

AccountabilityComplainer is a single-file web app for evidence-backed reports: requirements, site observations, complaints, incident logs and maintenance checks. Type your text, add photos, video and audio, and each file is placed right after the sentence it belongs to, or collected in an Attachments section at the end. Export the finished report as Word, PDF, HTML or a full package.

No sign-up, no server, no build step. Files never leave your device.

## Features

- **Place files inline or at the end.** Put the cursor where a file should go and click *Insert here*, or drag or paste the file straight into the text. Markers look like `[[img-1]]`, `[[vid-2]]`, `[[aud-3]]`. Anything you don't place goes into *Attachments*.
- **Photos, video and audio**, each with its own size limit (defaults: 2 MB / 50 MB / 15 MB).
- **Automatic image shrinking.** Oversized photos are resized and recompressed until they fit, or rejected if you prefer.
- **Separate numbering for each type** (Figure 1, Video 1, Audio 1), with editable captions, video durations and a still frame grabbed from each video.
- **Live preview** that plays video and audio.
- **Exports**
  | Format | Video and audio |
  |---|---|
  | HTML | Play inline, all files embedded |
  | Word (.docx) | Still frame + caption + clickable link to the file |
  | PDF | Still frame + caption + link to the file |
  | **Full package (.zip)** | Word, PDF and HTML in one folder, with the media files in `media/`. Recommended whenever there's video or audio |
- **Templates:** requirements list, observation report, complaint/incident report, facility check.
- Headings with `# `, a draft that survives a reload, light and dark themes, and a layout that works on phones.

## Run it

Download `index.html` and open it in any modern browser. That's it.

To host it free on **GitHub Pages**: *Settings → Pages → Deploy from branch → `main` / root*. The app will be live at `https://<your-username>.github.io/accountability-complainer/`.

## How it works

Everything runs in the browser:
- Images are read with `FileReader`, and PNG/JPEG conversion and shrinking happen on a `<canvas>`.
- Video stills and durations come from a hidden `<video>` element.
- `.docx` files are built by hand (WordprocessingML + DrawingML, zipped with [JSZip](https://stuk.github.io/jszip/)).
- PDFs use [jsPDF](https://github.com/parallax/jsPDF).
- The full package is a JSZip archive.

Both libraries load from cdnjs, so the first export needs an internet connection.

## Documentation

See [`docs/SRS.md`](docs/SRS.md) for the software requirements specification, known limits and roadmap.

## Known limits

- Video can't be compressed in the browser. Trim long phone clips before uploading.
- Some iPhone HEVC `.mov` files won't preview in Chrome on Windows. They still attach and export.
- Images aren't kept after a page reload. The text is.
- The PDF uses Helvetica, so characters outside Latin-1 may not render. Word and HTML are unaffected.

## License

MIT. See [LICENSE](LICENSE).

---

Built by [Muokwe Matai](https://github.com/Emdex04).
