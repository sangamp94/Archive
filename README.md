# Archive URL Uploader

A small Render Background Worker for uploading **videos you own or are authorized to redistribute** to Internet Archive. It fetches a source URL on the worker, so the video does not need to be saved on your phone.

## Important limits

- This is not a way to hide copyrighted uploads or bypass takedowns. Use accurate titles and metadata.
- The source must provide a directly downloadable media file and permit downloading.
- Large files need enough Render disk and worker runtime. The worker uses a temporary file and deletes it after upload.
- Do not commit credentials or source URLs containing private tokens to GitHub.

## Deploy on Render

1. Open Render and create a **Background Worker** from this repository.
2. Build command: `pip install -r requirements.txt`
3. Start command: `python worker.py`
4. Add the environment variables below in Render's dashboard.
5. Deploy. Check the worker logs for the result.

## Environment variables

Required:

- `SOURCE_URL`: direct URL to a video you are authorized to archive.
- `IA_ACCESS_KEY`: Internet Archive S3 access key.
- `IA_SECRET_KEY`: Internet Archive S3 secret key.
- `IA_IDENTIFIER`: descriptive, unique item identifier (lowercase letters, numbers, and hyphens).
- `IA_TITLE`: accurate title for the item.
- `IA_DESCRIPTION`: description of the content and rights/permission basis.

Optional:

- `IA_CREATOR`: creator or rights holder.
- `IA_LICENSE_URL`: applicable license URL, if any.
- `MAX_BYTES`: maximum download size in bytes (default 2 GB).

Set your Internet Archive credentials privately in Render; never place them in source code or public GitHub files.

## Run locally

Install dependencies with `pip install -r requirements.txt`, then set the environment variables in your shell and run `python worker.py`.

The worker stops if the URL does not look like a direct media download, if the size limit is exceeded, or if required metadata/credentials are missing.
