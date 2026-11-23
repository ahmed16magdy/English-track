# Ahmed’s English Academy

## Open the academy

Open **index.html** in a full browser. The app, 12 short lessons, four longer stories, and two three-clip placement sets are embedded in that file. Nothing needs to be installed. Copy the file to your phone and open it in a browser that allows local HTML to run. If your phone opens a document preview or blocks the microphone, use a static HTTPS copy of the same file. Keep backups when switching browsers, moving the file, or changing from a local file to a web address.

Take the listening check, then pick 30, 60, or 90 minutes before starting the session. The running timer measures your chosen practice time. Tap **Done** when you’re ready to move on. Use **Cooking mode** for a hands-free queue of easier audio. For meaning-focused listening, choose audio you can follow with roughly 90–95% of its words familiar, leaning toward 95%. If you keep losing the story, move to an easier clip.

### YouTube and microphone access

YouTube needs internet and an identifiable web origin for the embedded controls. From the folder containing **index.html**, run this optional command and open **http://127.0.0.1:8000/** on the same computer.

```sh
python -m http.server 8000 --bind 127.0.0.1
```

On your phone, use HTTPS for embedded YouTube and the most reliable microphone access. In local-file mode, **Watch on YouTube** opens the publisher’s video at the start time. The browser and video publisher control which speeds are available and whether the video allows embedding. A timed transcript is required for sentence-by-sentence replay. [YouTube IFrame API](https://developers.google.com/youtube/iframe_api_reference) · [Microphone permission and secure contexts](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)

## Add clips

In **Library → Add a YouTube clip**, enter a title, a real YouTube URL, a start and end in seconds, a track, a listening level, and a pace. To enable sentence replay, optionally add one line per sentence in the form `start | end | sentence`. Video times are absolute seconds from the beginning of the video. During playback, use **Save a phrase at this time** to capture the timestamp and enter a full sentence containing the phrase.

**clips.json** is the editable starter video library and a working format example. The starter entries are already inside **index.html**. Edit a copy, then use **Import clips.json**. It accepts a top-level array or `{"version":1,"clips":[…]}`. Existing video/time combinations are skipped, and imports add new clips. The BIM video entry is an explicit placeholder. The app also includes original BIM audio lessons.

| Field | Values |
|---|---|
| `title`, `url`, `start`, `end` | A title, a YouTube video URL, and numeric bounds with `0 ≤ start < end` |
| `level`, `topic`, `speed` | Level: `A2`, `B1`, `B1+`, `B2`. Track: `General`, `Workplace`, `Engineering`. Pace: `Steady`, `Natural`, `Brisk`. |
| `has_transcript`, `transcript_url` | Transcript availability is derived from timed lines or an HTTPS publisher link. |
| Optional `id`, `focus`, `hook` | A stable ID, a focus of `sound`, `vocabulary`, `speed`, `attention` or `balanced`, and a short listening instruction. |
| Optional `lines`, `chunks` | Lines use `{start,end,text}`. Chunks use `{chunk,line,cue,priority}`, where `line` is the zero-based index of the full sentence containing the phrase. |

## How review and progress work

New phrases are due immediately. Say the missing phrase in the full sentence, reveal it, hear the source, then choose **Again**, **Hard**, **Good**, or **Easy**. The scheduler uses SM-2 grades 1, 3, 4, and 5, starting at ease 2.5 with a floor of 1.3. Successes schedule 1 day, 6 days, then the previous interval multiplied by the updated ease and rounded up, capped at 365 days. Again resets the success sequence and schedules the card for tomorrow. Hard is a successful review for scheduling. Learned and retained are separate self-review measures. **Learned** begins at the first Good/Easy. **Retained** begins after two Good/Easy reviews on different days with at least seven days since saving, and is cleared by Again. Dates and weeks use Abu Dhabi time. [Original SM-2](https://super-memory.org/english/ol/sm2.htm)

The progress log counts playback time, the completed shadowing task timer, and saved speaking time. A streak uses recorded practice or a completed session. Weekly comparison defaults to your first and latest weekly take. It keeps one take per week and the latest daily take. Recordings are browser-local and may be compressed to fit. Export your JSON occasionally from **Progress**. It contains your voice recordings. Import replaces the active data after confirmation.

## Research behind the features

- **Placement and monthly recheck** — comparing original, slower, and transcript passes supports reflection on listening difficulties. The estimates are informal app heuristics. [Vandergrift & Tafaghodtari](https://doi.org/10.1111/j.1467-9922.2009.00559.x)
- **Today’s plan** — the planned minutes are roughly balanced across meaning-focused input, meaning-focused output, language-focused learning, and fluency development. [Nation’s Four Strands](https://doi.org/10.2167/illt039.0)
- **Library, warm-up and cooking** — very familiar language frees attention for meaning. The recommendation starts at your estimate and adds challenge when the check suggests it is manageable. [Van Zeeland & Schmitt](https://doi.org/10.1093/applin/ams074)
- **Intensive listening and connected speech** — listen, check the transcript, and relisten to match familiar written phrases with their reduced or linked spoken forms. [Vandergrift & Tafaghodtari](https://doi.org/10.1111/j.1467-9922.2009.00559.x) · [BBC pronunciation workshop](https://feeds.bbci.co.uk/learningenglish/english/features/pronunciation/)
- **Notebook** — practise useful multiword expressions in full sentences, starting with frequent NGSL headwords and phrases you can use in meetings. [NGSL Project](https://www.newgeneralservicelist.com/new-general-service-list) · [Conrad & Biber](https://pdxscholar.library.pdx.edu/ling_fac/3/)
- **Spaced review** — recall before revealing, then review again after a delay. [Karpicke & Roediger](https://doi.org/10.1126/science.1152408) · [Cepeda et al.](https://doi.org/10.1037/0033-2909.132.3.354)
- **Shadowing and retells** — echo familiar phrases to focus on sound and rhythm, then repeat a message in less time to practise fluency. [Hamada](https://doi.org/10.1177/1362168815597504) · [De Jong & Perfetti](https://doi.org/10.1111/j.1467-9922.2010.00620.x)
- **Speaking and weekly review** — explain a real work decision and listen to a repeated prompt over time to choose a specific next practice target. [Nation’s Four Strands](https://doi.org/10.2167/illt039.0) · [De Jong & Perfetti](https://doi.org/10.1111/j.1467-9922.2010.00620.x)

## Limits and quick tests

The placement check estimates listening for practice. Its two forms are short and the repeated questions can themselves improve scores. Built-in audio uses synthetic voices, and the offline catalogue repeats during longer sessions. Authentic clips offer more variety. Speech recognition is optional, approximate, browser-dependent and may use a remote recognizer. The app cannot judge pronunciation, interaction skills, or accredited CEFR level. Keep a real English conversation or meeting practice each week to work on turn-taking, interruptions, and clarification.

1. **Today.** Pick 30 minutes, complete the listening check, then start the warm-up. Reload and select **Resume session**. In intensive listening, reveal the transcript, replay a sentence, and hide the transcript for the last pass.
2. **Library and speaking.** Add a real clip with timed lines. Save a phrase, reveal it in Notebook, and tap **Good**. Record a short answer, stop, and replay. Under an HTTP(S) origin, load a YouTube clip to check speed and looping in your browser.
3. **Progress and offline.** Export a backup, import it in a fresh browser profile, and verify your cards and recordings. Disconnect from the internet, reopen the file, and start the Cooking queue.
