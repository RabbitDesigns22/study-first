# study-first

**Make your agent study what you asked, and every source behind it, before it answers. No vague answers, no invented details.**

`study-first` is an agent skill for Claude Code and any agent that reads `SKILL.md` skills. It fixes the most common root of agent mistakes: the agent skims, then answers as if it had studied.

Before answering, the agent has to:
1. **Break down everything you asked**, including messy dictated messages and "scratch that" corrections. The last version counts.
2. **Map the sources** for each point: the document, the past decisions, the live state.
3. **Read them in full**, and say how much it read. A "succeeded" label, a file name or a redirect is not proof.
4. **Cross-check** every important conclusion with a second source.
5. **Answer point by point** with short evidence, and **never write a detail it did not see** ("I did not see which").

## See the difference

> **You:** Study this chat and tell me why the task did not finish.

**Without the skill:** it reads the titles and the last message, sees "succeeded", and answers with a confident detail it never saw.

**With the skill:** it lists every part of your question, reads the sources in full, wants two signals that agree, and answers point by point. If it did not see a detail, it says so.

**Skip it if** you asked for a single fact that one lookup answers.

**Status:** in daily use in the author's own setup. Plain instructions, no scripts, no network calls. MIT. Issues and suggestions welcome.

## Does it work?

It was tested against the same model without the skill, on real cases:
- **"What errors has this client's app had?"** (a 131-line error log). Both versions found all 10 entries. With the skill the answer stuck to the question and flagged what could not be checked live. Without it, the agent also dumped dozens of unrelated entries.
- **"Did this morning's scheduled run work?"** (the app said "succeeded"; the run had died on a permission prompt). Both versions caught it. The first version of the skill invented which command had hung. That produced the "no detail you did not see" rule. With the fixed skill, the agent cross-checked 4 sources, wrote "I did not see which command" and marked its deduction as a deduction.

It is honest about the size of the gain. On short, clean questions a good model already reads well. The skill matters most in long, busy sessions, where agents skim most.

## Install

```bash
npx skills add RabbitDesigns22/study-first
```

Or copy `skills/study-first/` into `~/.claude/skills/`. To make every session use it, add one line to your global `CLAUDE.md`: "Before answering anything beyond a single fact, load the `study-first` skill."

## Works well with

- [`one-answer`](https://github.com/RabbitDesigns22/one-answer): one final answer, thought through, instead of a plan and then corrections.
- [`never-twice`](https://github.com/RabbitDesigns22/never-twice): a shared error log so the same mistake never happens twice.
- [`skill-harvest`](https://github.com/RabbitDesigns22/skill-harvest): this skill was found by reading real sessions.

## Español

**Que tu agente estudie a fondo lo que le pediste, y las fuentes, antes de responder.** Hace cuatro cosas:
- separa cada cosa que pediste;
- lee completo lo que hay que leer, sin quedarse con títulos ni con un "terminado";
- compara con una segunda fuente;
- responde punto por punto con la prueba, sin inventar ningún detalle.

Instalar: `npx skills add RabbitDesigns22/study-first`

## More skills from the same setup

These come from one real workflow: a small agency run with 15+ Claude Code sessions in parallel. Each skill fixes one problem that kept happening there.

| Skill | What it fixes |
|---|---|
| [one-pass](https://github.com/RabbitDesigns22/one-pass) | get it right the first time; stop paying tokens for rework |
| [hora-exacta](https://github.com/RabbitDesigns22/hora-exacta) | real date and time in every message, so nothing lands on the wrong day |
| [hands-on](https://github.com/RabbitDesigns22/hands-on) | the agent does what it can and only asks you for codes, keys and payments |
| [easy-for-them](https://github.com/RabbitDesigns22/easy-for-them) | steps people actually follow: direct link, one action per line |
| [one-answer](https://github.com/RabbitDesigns22/one-answer) | one thought-through answer instead of plan, fix, new plan |
| [never-twice](https://github.com/RabbitDesigns22/never-twice) | a shared error log so no session repeats a known mistake |
| [report-now](https://github.com/RabbitDesigns22/report-now) | status checked live this minute, stamped with the time |
| [sort-me-out](https://github.com/RabbitDesigns22/sort-me-out) | one ordered list of what is urgent, waiting and forgotten |
| [in-the-loop](https://github.com/RabbitDesigns22/in-the-loop) | a live board so parallel sessions know what the others changed |
| [session-watchdog](https://github.com/RabbitDesigns22/session-watchdog) | finds the sessions that got stuck mid-task and wakes them on your yes |
| [skill-harvest](https://github.com/RabbitDesigns22/skill-harvest) | reads your sessions and finds the skills you are missing |
| [small-budget-ads](https://github.com/RabbitDesigns22/small-budget-ads) | Meta Ads rules for 1-5 USD a day ad sets |
| [whatsapp-closer](https://github.com/RabbitDesigns22/whatsapp-closer) | evidence-ranked rules for a WhatsApp sales assistant that closes |
| [whatsapp-number-onboarding](https://github.com/RabbitDesigns22/whatsapp-number-onboarding) | connect a number to the WhatsApp Cloud API in the safe order |
| [proposal-pdf](https://github.com/RabbitDesigns22/proposal-pdf) | short PDF proposals with every price checked against its source |
| [published-vs-planned](https://github.com/RabbitDesigns22/published-vs-planned) | says "published" only for what it saw live on the public page, Facebook and Instagram checked apart |
| [source-every-fact](https://github.com/RabbitDesigns22/source-every-fact) | every price, phone and name on a post traced to its source, nothing added |
| [only-what-was-asked](https://github.com/RabbitDesigns22/only-what-was-asked) | "pause only Google Ads" pauses only Google Ads, and proves the rest did not move |
| [model-per-chat](https://github.com/RabbitDesigns22/model-per-chat) | the right model for each chat: top model where mistakes cost money, cheap or none where it only runs often |
| [music-by-niche](https://github.com/RabbitDesigns22/music-by-niche) | music that matches the client's business, never repeated for a client or across clients in 3 weeks |
| [full-power](https://github.com/RabbitDesigns22/full-power) | the best the model can do on high-stakes work: strongest model only for the hard step, best-of-N with a judge, fresh-eyes verifier |

If one of them saved you a redo, a star helps other people find it.

## License

MIT. Made by [Rabbit Designs](https://github.com/RabbitDesigns22).
