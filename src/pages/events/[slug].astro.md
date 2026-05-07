---
import fs from 'fs';

export function getStaticPaths() {
  const files = fs.readdirSync('./src/content/events');

  return files.map(file => ({
    params: {
      slug: file.replace('.md', '')
    }
  }));
}

const { slug } = Astro.params;

const file = fs.readFileSync(
  `./src/content/events/${slug}.md`,
  'utf-8'
);

const title = file.match(/title: "(.*)"/)?.[1];
const date = file.match(/date: "(.*)"/)?.[1];
const location = file.match(/location: "(.*)"/)?.[1];
const body = file.split('---')[2];
---

<html lang="de">
  <head>
    <meta charset="UTF-8" />
    <title>{title}</title>

    <style>
      body {
        background: #0a0f1c;
        color: white;
        font-family: Arial;
        padding: 40px;
        line-height: 1.6;
      }

      .card {
        background: #121a2b;
        padding: 30px;
        border-radius: 16px;
      }

      .meta {
        color: #9aa4b2;
        margin-bottom: 10px;
      }
    </style>
  </head>

  <body>

    <div class="card">

      <h1>{title}</h1>

      <div class="meta">
        📅 {date}
      </div>

      <div class="meta">
        📍 {location}
      </div>

      <hr style="margin:20px 0;opacity:0.2;" />

      <div>
        {body}
      </div>

    </div>

  </body>
</html>