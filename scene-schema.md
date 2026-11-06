# Script JSON schema (`remotion/src/scripts/<id>.json`, rendered by `Video5.tsx`)

Working example: `remotion/src/scripts/rzt_intro.json` (认证通简介). Copy it and replace the content.

```jsonc
{
  "meta": {"brand": "认证通", "watermark": "@认证通", "source": "信息来源：……", "mascot": "shield", "theme": "paper"},
  "beats": [  // one narration line = one shot; ids become mp3 names
    {"id": "r1", "scene": "hook", "text": "旁白一句", "pose": "surprised", "sfx": "ping"}
  ],
  "scenes": { "hook": {…}, "valid": {…}, … }   // fields below
}
```

- `pose`: `master` (待机) · `point` · `surprised` · `think` · `check` (欢呼) · `wave` · `none` (hide guide in that beat)
- `sfx`: `boom` (use sparingly) · `stamp` · `whoosh` · `tick` · `ping` · `pop` · `page`
- `title` (every scene): `[{"t": "出海合规"}, {"t": "有多难", "hl": true}]` — ≤ 8 字 total; `hl` = green (red in impact)
- Icon names: `doc box car sign nav shield refresh coin globe chip factory person clipboard lab wireless plug bolt passport fridge laptop bulb fire drop brick bowl` — new icons go in `ICONS` in `Video5.tsx` (flat, thick `{...S}` outline, spread `S` before `fill`)

| Scene | Fields | Beats used |
|---|---|---|
| hook | `badges` (≤ 6 short texts ≤ 4 字, 3 per row; text only — no flags/logos), `stickers` (optional icon names, a floating row under 3 badges, e.g. `fridge laptop bulb plug`), `chip`, `bubble` (shows on beat 2) | 2 |
| valid | `icon`, `stamp` (big rotated stamp text), `tag` (≤ 12 字, beat 2), `bubble` | 2 |
| analogy | `rows: [{l: {icon, label}, r: {icon, label}, sep?}]` (`sep` e.g. "VS" for a contrast row instead of "=") — row i appears on beat i; `sep` (optional, default `=`; use `→` for before/after) | 3 |
| chain | `cards: [{icon, text, sub?}]` (`sub` = small grey line under the text, ≤ 14 字) (card i on beat i, ≤ 8 字) + `mode`: `cards` = pain points with red ✕ (default) · `flow` = numbered steps with arrows (办证流程) · `plain` = parallel options, no marks (持证方式) · `grid` = up to 8 category cards `{icon, text, beat}` in two columns, dimmed on beat 0 and lit on their `beat` (八大品类 / 六步法); optional `note` (small dashed caption under the grid, `noteBeat`, `noteY` default 1110) | 3 |
| impact | `from {icon,label}` (with ⊘), `mid {icon,label}`, `result` (red chip) | 2 |
| timeline | `nodes: [{d, t?, now?}]` (3 nodes; `now` pulses orange; also works for cost breakdowns), `chip` (beat 2), `chipIcon` (default `refresh`, e.g. `coin`), `chipBeat` (default 1), `chipX` (default 600; ~670 when the guide's hand covers the icon) | 2 |
| check | `header`, `items` (5, up to 7 — rows tighten automatically above 5, ≤ 10 字; item i ticks on beat i+1), `titleSize` (default 112, use 104 for long titles) | 1 + N + 1 |
| outro | `sticker` (brand), `bubble` (slogan, beat 2), `bye` (optional — leave it out when the narration already says 下期见, otherwise it duplicates the subtitle), `next` (optional list ≤ 6 × ≤ 7 字: 「下期预告」card that pops item by item during beat 2 — 锐新 videos always use it) | 2 |

Scenes are matched by the `scene` of each beat in order; a scene may be skipped entirely (keep hook / valid / check / outro).

- A 3rd outro line (e.g. 下期预告) works with `next: ["一句话"]` — keep it one item when it is one question. A content line that is not 关注/预告 should move into an earlier scene rather than sit under the 关注认证通 title.
