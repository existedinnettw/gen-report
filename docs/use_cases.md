# use cases

* This program summarizes members' weekly reports into a single department weekly report.
* User assign source folder which contains all the individual reports in `docx` or `markdown` for processing.
  * program will parse those reports and generate a summary report in markdown format.
* User should assigns additional example folder which contains all the individual reports at specific week, and relevant department report at that week.

report document naming format

member report naming, `{member_name}工作報告-{yyyyMMdd}.docx`, `{member_name}工作報告-{yyyyMMdd}.doc`, `{member_name}工作報告-{yyyyMMdd}.md`.

team report naming, file name contain `{}~ {}之工作報告_{}`.

## stage: preprocessing

* program will read example folder and convert all docx file to markdown file copy if any.
  * then program will give input members' reports and output department report (all in markdown) at that week into LLM as example context.

## stage: summarized target report

* program will convert all markdown files in src folder to plain markdown files.
* program will input all plain markdown files into LLM as input, and LLM has to generate a final department report based on the input (just as example context).


