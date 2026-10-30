# Data notes for the train/test release (October 2026)

This file documents how the Mathematics, English, Physics, Chemistry and Biology
train/test sets were prepared from the authors' working files, and every place where
the data was changed by hand. Existing History, Geography and Civic Education sets
and the `eval` sets are unchanged.

## Splits

| Subject | test | train |
| :--- | :--- | :--- |
| Mathematics | `MET_Math_OE_2019..2023_101` (official exams, 5) | `Math_*` (29) + `MET_Math_OE_2019..2022_102..104` (12) |
| English | `MET_Eng_OE_2020..2022_401` (3) | `Eng_*` (7) + `MET_Eng_OE_2020..2022_402` (3) |
| Physics | `Phy_41` .. `Phy_45` | `Phy_1` .. `Phy_40` |
| Chemistry | `Che_41` .. `Che_45` | `Che_1` .. `Che_40` |
| Biology | `Bio_41` .. `Bio_45` | `Bio_1` .. `Bio_40` |

For Physics, Chemistry and Biology the working folder held 45 practice exams in a single
folder; the last five (41–45) were set aside as the test set.

## Format

Every exam is stored twice, with identical content:

* `Word format/<split>/<Subject>/<exam>.docx` – one table with the columns
  `ID | Image_Question | Question | Choice | Image_Answer | Explanation`
* `JSON format/<split>/<Subject>/<exam>.json` – a list of objects with the same six keys.

Images live in a folder named after the exam next to the file, and are referenced as
`<exam>/<file>`; several images are separated by `, `. Formulas are kept as LaTeX text.

Processing applied to all new files:

* Physics and English were converted from the 3-column working format
  (question | explanation | answer) to the 6-column format; rows that Word had split in
  two were merged back.
* Biology images that were embedded in the Word table were extracted to
  `Bio_X/Bio_X_<question>[ _a].<ext>` (`_a` = image in the explanation).
* Image references were normalised (e.g. `image0010.png` → `image010.png`, wrong
  `.png`/`.jpg` extension, missing folder prefix). All references point to an existing file.
* Answers are always one of `A`–`D`. Where the answer cell was empty or garbled, the
  answer stated in the explanation ("Chọn X", "Đáp án X") was used.

## Removed items

* `MET_Math_OE_2022_103 (1).docx` – duplicate of `MET_Math_OE_2022_103.docx` (the newer file was kept).
* `MET_Math_OE_2022_101` item 51 – empty row.
* `Che_1` item 29 – open-ended (non multiple-choice) question.
* `Che_5` question 32 – the question text is missing in the source; only its answer remained.
  IDs in `Che_5` keep the original question numbers (… 31, 33 … 40).

Some practice exams are shorter than 40/50 questions in the source: `Bio_1` (30), `Che_1` (28), `Che_5` (39).

## Realigned files

The source tables of these exams were shifted by one row; questions, answers and
explanations were realigned by hand and checked against the worked solutions:

* `Bio_19` – answers/explanations of Q7–Q15; Q15 was split out of the Q14 cell.
* `Che_5` – question texts of Q33–Q40.
* `MET_Eng_OE_2021_401` – answers/explanations of Q23–Q50; Q49 answer set to C
  ("intelligent" → "intelligible").

## Answers filled in by hand

These items had no answer anywhere in the source. The answer was taken from the worked
solution when one existed, otherwise solved by hand; a short justification was appended
to `Explanation`.

| Exam | Question | Answer |
| :--- | ---: | :---: |
| Bio_11 | 4 | A |
| Bio_11 | 17 | A |
| Bio_11 | 22 | B |
| Bio_11 | 23 | D |
| Bio_13 | 6 | B |
| Bio_13 | 16 | C |
| Bio_13 | 25 | C |
| Bio_15 | 39 | C |
| Bio_20 | 12 | A |
| Bio_22 | 5 | A |
| Bio_24 | 21 | B |
| Bio_26 | 12 | D |
| Bio_27 | 18 | B |
| Bio_30 | 4 | C |
| Bio_30 | 16 | D |
| Bio_31 | 10 | C |
| Bio_31 | 13 | C |
| Bio_31 | 30 | C |
| Bio_35 | 22 | A |
| Bio_35 | 27 | D |
| Bio_41 | 37 | C |
| Bio_45 | 30 | B |
| Bio_45 | 38 | B |
| MET_Math_OE_2019_102 | 47 | A |
| MET_Math_OE_2020_102 | 27 | C |
| MET_Math_OE_2020_102 | 30 | A |
| MET_Math_OE_2021_101 | 12 | A |
| MET_Math_OE_2021_101 | 31 | C |
| Math_3 | 27 | B |
| Math_32 | 5 | A |
| Math_4 | 22 | D |
| Math_5 | 6 | C |
| Math_6 | 10 | A |
| Phy_44 | 29 | C |

## Answers corrected

The `Choice` cell contradicted the worked solution in the same row; the solution was
re-checked and its answer kept.

| Exam | Question | Was | Now |
| :--- | ---: | :---: | :---: |
| Bio_35 | 14 | C | D |
| Che_32 | 2 | A | B |
| Eng_22.2 | 28 | B | C |
| Eng_22.2 | 42 | B | C |
| MET_Math_OE_2019_102 | 32 | A | C |
| MET_Math_OE_2019_104 | 45 | C | D |
| Math_1 | 19 | B | D |
| Math_2 | 22 | A | C |
| Math_34 | 9 | A | B |
| Math_7 | 23 | A | C |
| Math_7 | 31 | A | C |

## English: 32 additional exams (October 2026)

Source: the book *45 đề thi thử Tiếng Anh THPT Quốc gia 2023 giống đề thi chính thức*
(PDF, 411 pages, 38 tests: Đề 1–39 without Đề 4). Text was extracted page by page;
underlined words were recovered from the drawn underline strokes and written as
`\underline{...}`. Every question keeps its instruction (and the reading/cloze passage)
in `Question`, as in the existing English files.

* train (30): Đề 1–3, 5–31 → `Eng_6`–`Eng_21`, `Eng_23`–`Eng_36` (`Eng_22` is skipped because
  `Eng_22.1` / `Eng_22.2` already exist)
* test (2): Đề 32 → `Eng_37`, Đề 34 → `Eng_38`
* Not used: Đề 33 (every option label C is printed as D), Đề 35–39 (spare).

Answers come from the book's answer key. Detailed explanations exist in the book only
for Đề 1–10 (and a few items of Đề 11–15); elsewhere `Explanation` is empty.

| Exam | Book | Split | Explanations |
| :--- | :--- | :--- | :--- |
| `Eng_6` | Đề 1 | train | có |
| `Eng_7` | Đề 2 | train | có |
| `Eng_8` | Đề 3 | train | có |
| `Eng_9` | Đề 5 | train | có |
| `Eng_10` | Đề 6 | train | có |
| `Eng_11` | Đề 7 | train | có |
| `Eng_12` | Đề 8 | train | có |
| `Eng_13` | Đề 9 | train | có |
| `Eng_14` | Đề 10 | train | có |
| `Eng_15` | Đề 11 | train | một phần (1 câu) |
| `Eng_16` | Đề 12 | train | một phần (1 câu) |
| `Eng_17` | Đề 13 | train | một phần (3 câu) |
| `Eng_18` | Đề 14 | train | một phần (5 câu) |
| `Eng_19` | Đề 15 | train | một phần (2 câu) |
| `Eng_20` | Đề 16 | train | không |
| `Eng_21` | Đề 17 | train | không |
| `Eng_23` | Đề 18 | train | không |
| `Eng_24` | Đề 19 | train | không |
| `Eng_25` | Đề 20 | train | không |
| `Eng_26` | Đề 21 | train | không |
| `Eng_27` | Đề 22 | train | không |
| `Eng_28` | Đề 23 | train | không |
| `Eng_29` | Đề 24 | train | không |
| `Eng_30` | Đề 25 | train | không |
| `Eng_31` | Đề 26 | train | không |
| `Eng_32` | Đề 27 | train | không |
| `Eng_33` | Đề 28 | train | không |
| `Eng_34` | Đề 29 | train | không |
| `Eng_35` | Đề 30 | train | không |
| `Eng_36` | Đề 31 | train | không |
| `Eng_37` | Đề 32 | test | không |
| `Eng_38` | Đề 34 | test | không |

Hand fixes (printing errors in the book):

* Options re-typed where a label was missing or duplicated: `Eng_10` Q32 (Đề 6), `Eng_37` Q12 (Đề 32, two "B"), and
  Đề 39 Q6 (not released).
* `Eng_15` Q14 (Đề 11): answer table says A, worked solution says B ("There being") → B.
* `Eng_23` Q3–4 and `Eng_24` Q3–4: the book prints the pronunciation instruction above
  stress questions; the stress instruction is used instead.
* Error-identification items whose underline was broken or missing in the PDF, options set
  from the labelled phrases: `Eng_7` Q48, `Eng_11` Q48, `Eng_13` Q47, `Eng_25` Q47,
  `Eng_28` Q46, `Eng_30` Q48, `Eng_33` Q46, `Eng_37` Q48.
* Typos of the original text (e.g. "inderlined", "leam", "bom") are kept as printed.

Checks run on all 1,600 items: 4 non-empty options A–D, answer in A–D, unique IDs,
question number = ID, 2 pronunciation items per exam with an underlined part in all four
options, underlined target word in every synonym/antonym item, every error-identification
option found verbatim in its sentence, Word rows = JSON items, no duplicate of any existing
English question. A random sample of 40 answer-key items was solved by hand: 40/40 agreed.
