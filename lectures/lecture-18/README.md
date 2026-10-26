# Lecture 18 - Web APIs and JSON

Last class you rented a machine and typed into it over SSH. This class your own laptop asks other people's servers for data. By the end you will know how a request is built, what the status code tells you, why the reply arrives as JSON, and how to find one value inside it. We do it all in the browser and the terminal, with one short taste of Python at the end. Lecture 19 does the same work in Python.

[View the slides](https://danilofreire.github.io/datasci350/lectures/lecture-18/18-web-apis.html)

## What we cover

- What an API is: a contract between two programs, and the client-server model you met on EC2
- Anatomy of a URL, and building a World Bank URL one piece at a time
- The query string, percent-encoding, and status codes
- `GET` and `POST`, and why almost everything you do this semester is a `GET`
- JSON objects and arrays, and how to write the path to one value
- The World Bank's two-element reply
- `curl` in the terminal: printing, checking the status, and saving a reply to a file
- A first look at `requests` in Python
- Three exercises, each with a worked solution in the appendix

## Data snapshots

Three JSON files live in `data/`: `openmeteo_atlanta.json`, `wb_gdp_bra.json`, and `wb_pop_ury.json`. All three were pulled on 21 August 2026. The slides show shortened copies of them, so the numbers stay put. You can make your own copies with `curl -o`, as the lecture shows.

## Rendering

```bash
quarto render 18-web-apis.qmd
```

No code executes at render time. Every output on the slides was captured from a real request and pasted in.

## Before the next class

1. Install the packages you will need: `pip install requests pandas pyarrow`.
2. Open the AWS billing console and confirm your total reads zero.
3. Read the final project instructions.
4. Form a group of four to five and email me the names by Thursday 5 November.
5. Finish Exercise 03 if you did not have time in class.

API claims last verified: 21 August 2026 (the World Bank lists 29,544 indicators).

## Using AI in this course

You may use AI for the assignments in this course. Cite the tool you used, check everything it gives you, and remember that the fluency of an answer tells you nothing about whether it is correct.

Using AI tools in a manner prohibited in this course syllabus constitutes Cheating under the Emory Honour Code and is thus a form of academic misconduct.
