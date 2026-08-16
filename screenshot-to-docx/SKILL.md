---
name: screenshot-to-docx
description: Convert exam-paper screenshots into printable Word documents while preserving the original question images and diagrams. Use this skill whenever the user asks to turn a long webpage/mobile screenshot, scanned test image, or multiple exam screenshots into a DOCX, split questions from screenshots, preserve formulas/figures, or add answer pages after long questions.
compatibility: Requires Python with Pillow and python-docx. OCR is optional and used only as a segmentation aid; the original image remains the source of truth.
---

# Screenshot to DOCX

Use the bundled `scripts/assemble.py` for deterministic image splitting and Word generation. Preserve question images instead of reconstructing their text: diagrams, formulas, superscripts, coordinate grids, and circuit figures are more reliable as pixels than as OCR output.

## Workflow

1. Locate all input JPG/PNG files supplied for the task. Sort multi-image inputs by filename unless the user specifies another order.
2. Run the assembler with an output directory. For a first pass, keep the default automatic split and answer-page behavior.
3. Inspect `question_boundaries.png` and `processing_report.json`. If the report marks low-confidence boundaries, show the preview and ask for correction before claiming the document is final.
4. Deliver the generated `.docx`. Also retain the question-image directory and preview so the user can audit the result.

## Default layout contract

- A4 portrait, 18 mm margins.
- Leave the formal exam title blank unless the user provides one.
- Keep difficulty stars already present in the source image; do not infer or invent stars from question order, image height, or OCR.
- Every question must be followed by an answer area.
- Allocate each answer area dynamically between half an A4 page and one full A4 page. Shorter questions normally receive about half a page; long calculation questions receive about one page.
- If a question image spans pages, place its answer area after the final question page.
- Answer areas default to a heading plus ruled lines; use `--answer-style blank` for a blank area or `--answer-style grid` for graph-style answering.

## Review rules

- Never silently discard a question or merge two questions.
- If automatic segmentation is uncertain, report the candidate boundary rather than inventing text.
- OCR text may be used for question-number hints, but do not replace the original question image with OCR text.
- The final report must state the number of detected questions, answer areas, estimated half/full-page allocations, and any low-confidence boundaries.

## Direct command

```powershell
python scripts/assemble.py --input <screenshot-or-folder> --output <output-folder>
```

Useful overrides:

```powershell
python scripts/assemble.py --input image.jpg --output out --split-mode manual --cuts 0,820,1640
python scripts/assemble.py --input image.jpg --output out --answer-style grid
```

