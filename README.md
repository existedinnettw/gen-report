# gen-report

CLI tool to consolidate individual weekly member reports (Word / Markdown) into a single department weekly report using an LLM (via `litellm`). It can optionally leverage historical example weeks (few-shot) to steer style and structure.

## Features

* Parse member report files named like: `{member_name}工作報告-YYYYMMDD.docx|doc|md`.
* Convert `.docx` to Markdown using `mammoth`.
* Optional examples folder with both historical member reports and an existing team report (file name contains `之工作報告`). These are packaged into few-shot examples.
* Builds a structured prompt and calls a configured model (default `gemini/gemini-1.5-flash`, changeable) through `litellm`.
* Outputs a consolidated Markdown report with standardized sections.

## Environment

Get your API key from the respective provider.

Set an API key supported by `litellm` (Gemini preferred default):

```powershell
setx GOOGLE_API_KEY "your_gemini_key"  # Windows PowerShell (Gemini)
```

You can also use: `GEMINI_API_KEY`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `AZURE_OPENAI_API_KEY`, `GROQ_API_KEY`.

## Usage

```bash
gen-report --source ./this_week -e ./history1 -e ./history2 --out dept_report_20240821.md \
	--model gemini/gemini-1.5-flash
```

Dry run (print prompt only, no LLM call):

```bash
gen-report --source ./this_week -e ./history1 -e ./history2 --dry-run
gen-report --source ./this_week -e ./history1 --dry-run
```

## Folder Layout Expectations

```
this_week/
	Alice工作報告-20240821.docx
	Bob工作報告-20240821.md
history1/
	Alice工作報告-20240814.docx
	Bob工作報告-20240814.docx
	114年08月7日~ 114年08月13日之工作報告_20240814.docx
history2/
	Alice工作報告-20240814.docx
	Bob工作報告-20240814.docx
	114年04月24日~ 114年04月30日之工作報告_20240814.docx
```

## Development

Run locally without install:

```bash
python -m gen_report --source ./this_week --dry-run
```
