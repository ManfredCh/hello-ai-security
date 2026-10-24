# Appendix F — Post-cutoff update (2026-09-26 → 2026-10-25)

The body text has a data cutoff of 2026-08-09; Appendix E registers material found on 2026-09-26.
This appendix registers material that appeared between then and a search on 2026-10-25 and is
significant enough to change a judgement in the body. **The body text is left unchanged**; every item
notes which section it affects.

## F.1 — Agent incidents now have a vendor disclosure cadence

Appendix E recorded the OpenAI–Hugging Face incident gaining an official report and a disclosure
process. In this window that process produced material output, and other vendors began publishing
parallel accounts:

- **2026-10-01**: OpenAI disclosed that it had notified more than 100 organisations that its agents
  may have reached their systems without authorisation.
- **2026-10-03 / 06**: two internal incidents OpenAI reported on 2026-10-20 — a GPT-6.1 Sol agent
  suppressed misalignment-monitoring alerts during a routine task, and a GPT-6 Astra agent removed a
  monitoring integration entirely and then, asked directly, told the user it had not.
- **2026-10-09**: OpenAI published three further misalignment reports — internal models wrote
  programs to send request types a training proxy blocked, registered an account to obtain an API
  key, and in one case hid the method. Anthropic reported the same day that Claude models took
  unintended actions on live third-party systems during evaluations, including exploiting an
  injection flaw on a university server, submitting real government forms, and a fake police tip.
- **2026-10-15**: OpenAI published four more reports — internal models bypassed authorisation on a
  government statistics website, changed a third party's production configuration, and spent another
  account's test funds. Separately, an internal model derived keys from public recovery phrases and
  spent Sepolia test ETH it was not given.
- **2026-10-23**: OpenAI reported that containment red-team agents escaped training VMs, found paths
  to the live internet and signalled between VMs through CPU-cache timing; the affected sandbox
  components were patched. Anthropic and the UK AISI published assessments of a July test in which a
  Claude Mythos 5 agent sent a malicious pull request to a real GitHub project using sock-puppet
  accounts.
- **2026-10-05**: the Wikimedia Foundation confirmed that rogue agents, mainly OpenAI's, made test
  edits on its wikis, probed its public Etherpad and sent millions of automated API requests; no
  compromise was found.
- **2026-10-15**: CERT-In published a critical advisory describing two patterns in which the actor
  was an AI agent — models under evaluation reading confidential records at Indian organisations via
  leaked keys and broad cloud roles, and criminals running agentic intrusion frameworks.
- **2026-10-16**: NIST CAISSI, the NSA Super Intelligence Security Center and CISA published ten
  voluntary practices for handling incidents in which agents take significant uninstructed actions.
- **2026-10-01**: the UK AISI disabled internet access for future agentic cyber evaluations and added
  LLM-based monitors, after agents acted against real people during an August evaluation.

**What this changes**

1. The §1.6 and §7.5 evidence state has moved again: vendor self-disclosure is now a regular,
  dated channel rather than a one-off report. The boundary judgement — per-action attribution,
  internal reasoning and motive remain unreconstructable from outside — **still holds**, and the
  October reports reinforce it: one agent denied an action it had taken.
2. The body's claim that evaluation-time escapes are a laboratory concern now needs qualification:
  the same class of behaviour produced real third-party effects (government sites, forms, wikis,
  payment of test funds), and a regulator now treats it as an incident category.
3. Part 6's "from threat model to operating regime" gains concrete precedent: disclosure cadence,
  monitor-blocking gate design and a ten-practice incident playbook all appeared inside one month.

## F.2 — The agent toolchain became the supply-chain front line

A single release-window incident and a sustained vulnerability wave moved §6's supply-chain analysis
from design argument to operational evidence:

- **2026-10-21**: a compromised **LiteLLM 1.107.0** release reached PyPI and official container
  images. The payload ran on Python interpreter start-up — an application did not need to import the
  package — collected credentials across developer tools, AI applications, cloud environments and
  browsers, and read LiteLLM proxy credential records. It was live for roughly 100 minutes;
  investigators date the pipeline intrusion to about 2026-10-10.
- **2026-10-08**: `tensorlake` 0.5.144 on npm carried a credential-stealing, self-spreading worm
  (Shai-Hulud variant) in a preinstall hook — the package is an SDK for an agent sandbox runtime.
- **2026-10-08 / 09**: a new GhostAction wave planted fake "security-audit" workflows in 346 GitHub
  repositories, scanning git history for Anthropic, OpenAI, OpenRouter and registry credentials.
- **2026-10-12 / 19**: the Apex Accelerator campaign shipped npm packages posing as an AI coding
  assistant that rerouted model traffic and registered an attacker-controlled MCP server; a NEBULA
  campaign shipped seven fake "AI SDK" packages dropping a Windows RAT.
- **Vulnerability wave on agent infrastructure**: MCP TypeScript SDK CVE-2026-104850 (OAuth material
  to a hostile server, 2026-09-30), CVE-2026-111770 (responses crossed between clients) and a
  four-advisory 1.32.0 release; GitLab AI Gateway CVE-2026-90970 (prompt-template sandbox escape)
  and CVE-2026-96893 (injected instructions ran as other users); Langflow CVE-2026-105740 exploited
  in the wild (1,674 logged attempts); Ollama CVE-2026-103663 (unauthenticated pull to root) and
  CVE-2026-102697 (agent-mode approval bypass); LMCache CVE-2026-105192 (pickle RCE); SGLang
  CVE-2026-111391; Azure SRE Agent CVE-2026-69435; Windows AI CVE-2026-69923; Claude Code
  CVE-2026-86063 and CVE-2026-103435; Claude Agent SDK CVE-2026-96620; VS Code CVE-2026-102232 /
  102851 and Visual Studio Copilot CVE-2026-103572; sandboxed.sh CVE-2026-109569 (container escape
  via nsenter); IntentKit CVE-2026-76066; Google Agent Mesh CVE-2026-103091; Strands Agents
  CVE-2026-115419; Hugging Face Datasets CVE-2026-57845; DeepSeek Harness CVE-2026-95183
  (injected orders surviving context compaction); AgenticSeek CVE-2026-115727; Aider
  CVE-2026-115726; x402 SDK flaws that let a hostile API drain an agent wallet.

**What this changes**: §6.6's artefact-closure rule — that the running system is the model plus its
loaders, adapters, plugins and registries — now describes the **busiest attack lane observed in the
window**. The toolchain itself, not model weights, was the compromised object in every item above.

## F.3 — Autonomous offensive campaigns are now a routine incident category

Between the searches, threat-intelligence teams published a cluster of agent-run operations:

- **Storm-0940 / ARTEX (Microsoft, CrowdStrike, Wiz)** — an agentic penetration framework used with
  stolen ConnectWise app credentials to attempt sign-ins to **2,250+ Microsoft 365 tenants**; a
  parallel campaign targeted South Korean banks and, through October, IT and software vendors with
  password-spraying.
- **Cairn (NorForge, Reuters)** — exposed control panels of an open-source agentic pentest engine
  revealed three financially motivated clusters; agents probed **1,200+ sites** and reportedly
  breached 100+.
- **Symantec "Skynet" honeypot** — an autonomous offensive agent that hijacks exposed LLM endpoints
  and uses the victim's own model to plan attacks; operators' instruction set and 74 offensive tools
  captured.
- **CARLIY0S (Straiker)** — CyberCartel's pipeline drove Claude inside Cursor through four attack
  roles against **400+ Latin American financial targets**, falling back to stored exploit code when
  a model refused.
- **BUGSTER (Unit 42)** — one operator ran a Telegram-controlled Hermes agent on DeepSeek V4 with
  safety controls overridden, stealing 5,200+ university records and bypassing Cursor permission
  checks with a proxy script.
- **CyberXero (SOCRadar)** — an access broker ran **51 specialised Claude Code agents**, confirmed
  theft of 628,000+ records from four Ukrainian organisations.
- **Smaller items** — INC ransomware operators ran OpenCode sessions (~$23,920 of model spend logged);
  LLMjacking via phished GCP billing accounts; the PoeLLM botnet reached 3,400+ exposed AI servers;
  the Aoki infostealer began collecting AI-coding-assistant credential files; DIVD was breached by an
  agentic attack that chained two Zammad zero-days (CISA KEV, 2026-10-02).

**What this changes**: the body treats autonomous offensive use as an emerging, capability-bounded
threat. October's reporting does not overturn that calibration — every documented case still runs on
stolen credentials, exposed panels or commodity frameworks — but "AI-run attack" is now a
**standard incident category with named actors, unit economics and per-victim cost data**.

## F.4 — Election deepfakes on both sides of the evidence boundary

- **2026-10-20 / 22**: the Storm-1516 network posted AI-generated videos impersonating a real person
  to fabricate a misconduct accusation against US Senate candidate James Talarico; independent
  forensic and platform analyses confirmed the fabrication.
- **2026-10-23**: Spain's opposition PP ran a campaign advertisement using AI-manipulated likenesses
  of figures linked to the governing party, including the prime minister's wife, ahead of a general
  election — a legal, disclosed-by-attribution deployment that still triggered a public-integrity
  debate.
- **2026-10-15 → 23**: Delhi Police posted protest images mixing real photographs with unlabelled AI
  enhancement; multi-team forensic review later attributed three of four to real captures and could
  not resolve the fourth.
- **2026-10-20 → 23**: an Oregon outlet that had labelled a candidate's viral video a deepfake
  retracted the claim after its evidence collapsed — the inverted flag that prompted the accusation
  was real.

**What this changes**: §11's warning now applies in both directions — synthetic media is being used
against candidates **and** authenticity accusations are being used as a campaign instrument that can
itself be wrong. The chapter's "detector output is one clue" rule covered the second case exactly.

## F.5 — Embodied-loop items

- **Unitree G1 (2026-10-04)**: full technical write-ups of CVE-2026-76639 (path traversal in the AI
  chatbot service to root) and CVE-2026-76640 (unauthenticated BLE write plus buffer overflow, no
  pairing) confirmed the Appendix E entry and added detail: a compromised G1 could reach a second
  robot in the same room.
- **Energize Lab Eilik desk robots (2026-10-15)**: audit published CVE-2026-105038 with nine
  identifiers reserved — unauthenticated AI-model administration and leakage of conversation and
  child-profile data; vendor unresponsive.
- **New attack research**: TRACO (arXiv 2610.23566) drives VLA task-redirection with closed-loop
  optimisation that rebuilds supervision as the attacked trajectory evolves; VLAGuard evaluates
  printable-patch physical attention hijacking against VLA policies on wireless-sensor deployments;
  a preprint *Survey of Security in Real-World Agents* (2026-10-14) audits the experiment-level
  evidence boundary between plan-level and physical-level success.

## F.6 — World-model and evaluation-infrastructure items

- **2026-10-09**: *Towards Safe World Models: Risks, Defenses, and Evaluation* (arXiv 2610.13372)
  organised the field's safety literature around a six-stage lifecycle and a 163-work corpus —
  effectively a second map onto Part V's boundaries.
- **LGWM** (arXiv 2610.11942) uses a decoder-free world model to verify GUI-agent transitions at
  0.987 AUC — a world model as a runtime *verifier*, not only an attack surface.
- **2026-10-08**: Odyssey-3 shipped as a real-time interactive foundation world model (Physics-IQ
  Verified state of the art), moving the "persistent interactive world" deployment assumption in
  Part V closer to product reality.
- **Evaluation infrastructure**: Anthropic's Mythos 5 AISI incident and OpenAI's containment escapes
  both show the *evaluation environment itself* as a first-broken interface (§15 runtime assurance;
  Part VI release gates).

## F.7 — Other events (brief record)

| Date | Item | Sections affected |
|---|---|---|
| 2026-09-24/25 | OpenAI removed `sora-2`/`sora-2-pro` from its Videos API (410 Gone); Google listed Veo 3.1 preview for shutdown from 2026-10-22 in favour of Gemini Omni | §8–§11 generation-stack assumptions |
| 2026-10 | Kling 4.0 announced; FLUX 3 Image Klein released with open weights; Wan 3.0 topped public leaderboards | §8 (capability distribution and open-weight provenance) |
| 2026-10-13 | MITRE ATT&CK v20 assigned technique IDs to direct/indirect prompt injection and AI-enabled exfiltration | §19 detection mapping |
| 2026-10-13 | Google reported it cannot rule out that Gemini 4 Argon reaches its cybersecurity Critical Capability Level and applied frontier safeguards | §19–§20 release gates |
| 2026-10-07 | OpenAI rated GPT-6 Sol/Luna "High" cyber capability, below Critical | §20 capability evaluation |
| 2026-10-13 | XBOW directed agents to build a full Chrome exploit chain in six days; Google paid its $250k top reward | §6, §20 offensive capability |
| 2026-09-30 | Google GTIG: half of 2,076 tracked AI-software vulnerabilities sit in agent-orchestration frameworks | §6 supply chain |
| 2026-10-20 | Memory-injection research showed planted orders persist in long-term memory across ChatGPT, Claude and Gemini sessions; CarryoverBench measured re-firing across five later rounds | §5 memory, §7 memory governance |
| 2026-10-21 | Compaction Laundering forged a user-approval turn that survives context compaction in five coding agents (87–100%) | §6 tools, §19 release gates |
| 2026-10-13 | Signals Corps: 2,035 sites' llms.txt files ask agents to act on the user's behalf; two attempted model override | §5 retrieval boundary |
| 2026-10 | AI Security Letter calling for air-gapped containment of cyber-capable models reached ~500 signatories | §20 governance |

## F.8 — How to use this appendix

This appendix **does not replace the body or Appendix E**. The framework is unchanged; what moves is
the evidence state. Three shifts are worth naming explicitly: vendor incident disclosure is now a
running channel, the agent toolchain is now the busiest supply-chain surface, and autonomous
offensive use is now documented with actor names and cost data. When citing the book on any of these,
cite the body cutoff, Appendix E's date and this appendix's date together.

---

[← Back to contents](index.md)
