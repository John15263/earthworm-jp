# Earthworm Japanese Courses

This repository provides a sample Japanese course that follows the same conjunction-based sentence building method used in the original Earthworm project. The goal is to learn Japanese by gradually joining words into phrases and sentences, starting from simple vocabulary and building up to more complex constructions.

## Structure
The course data lives under `packages/xingrong-courses/data/courses/`. Each course file is a JSON array of statements. Every statement has three fields:

- **chinese**: the Chinese translation for the word or sentence.
- **english**: the Japanese text (this field name is kept for compatibility with the original project; it now holds Japanese).
- **soundmark**: romanised Japanese (hiragana/katakana or romaji) to help with pronunciation.

The sample course included here is **ja-01.json**. It begins with single words (e.g. "我" → "私") and progressively joins them into phrases ("我喜欢寿司" → "私は寿司が好き"). You can create additional courses by following the same pattern.

## Using this repository
1. Clone or download this repository and extract the files.
2. Copy the contents of the `packages/xingrong-courses/data/courses/` directory into the corresponding directory of your existing Earthworm project. If the directories don’t exist, create them.
3. Run the Earthworm script below in the root of the original Earthworm project to import the course into the database:

```bash
pnpm run ts-node packages/xingrong-courses/src/addCourse.ts \
  --id=ja01 \
  --order=1 \
  --title="日语课程 01" \
  --course=ja-01.json
```

This command reads **ja-01.json** and inserts each statement into the `statements` table. You can specify a different id or order to control where the course appears in the course list.

If you want the UI to display a "Japanese" label instead of "English", update the Earthworm front-end labels from "English" to "日本語" wherever necessary. Similarly, you may extend the database schema to include a `japanese` column, but the existing `english` field can also hold the Japanese content.

Start the Earthworm application following its README (install dependencies, set up PostgreSQL and Redis, run migrations, and launch the server). The Japanese course will now appear alongside the English courses.

## Creating your own courses
To build additional Japanese lessons, copy **ja-01.json** and modify it or create new files (`ja-02.json`, `ja-03.json`, etc.). Ensure each entry includes a Chinese translation, the Japanese text, and a pronunciation guide. When importing each new course, increment the order so courses appear sequentially.

## License
This project follows the same license as the original Earthworm project. Please refer to the LICENSE in the original repository.
