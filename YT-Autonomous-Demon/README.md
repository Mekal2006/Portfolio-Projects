<div align="center">
  <h1>YT Autonomous Demon</h1>
  <h3>Software Technical Documentation — v1.0</h3>
  <p><b>Automated YouTube Shorts Pipeline & Influencer Engine</b></p>
  <p><i>Lead Architect & Developer: Mekal Butt | Contact: mekalbutt.services@gmail.com</i></p>
</div>

<hr size="4" color="#d3d3d3">

<h2>1. Executive Summary & Architectural Philosophy</h2>
<p><b>System Name:</b> YT Autonomous Demon (Influencer Automation Engine)</p>
<p><b>Core Philosophy:</b> YT Autonomous Demon is a highly advanced Just-In-Time (JIT) processing pipeline engineered specifically to dominate the YouTube Shorts algorithm. Rather than pre-rendering and warehousing large libraries of finished video, it materializes each YouTube Short exactly at the moment of execution, processes it, ships it, and ruthlessly reclaims disk space immediately.</p>
<p>The Python codebase is engineered with strict C++-style discipline—featuring explicit resource lifecycles, bounds-checked buffer handling, and deterministic cleanup via <code>try/finally</code> blocks. This prevents the long-running, unattended daemon from leaking memory, disk space, or file handles over a rigorous 90-day operating lifecycle.</p>

<h3>The "Smart" Autonomy Matrix</h3>
<p>This engine is not a simple script; it is a self-regulating, autonomous brain governed by five architectural pillars:</p>
<ul>
  <li><b>Zero-Bloat Garbage Collection:</b> Every heavy artifact (raw chunks, rendered Shorts, extracted frames) is deleted the instant it is no longer needed. Local SSD storage remains pristine.</li>
  <li><b>Smart Cache Hit:</b> Before touching the network or invoking the CPU-heavy FFmpeg codec, the daemon intelligently checks for existing payloads.</li>
  <li><b>Hardware Interrupt Execution:</b> The daemon does not rely on volatile 24-hour Python RAM sleeps. It executes via Windows Task Scheduler, firing a hardware-level OS interrupt at a precise daily time.</li>
  <li><b>Quota-Aware State Machine:</b> Distinguishes between transient network errors and API quota exhaustion (429/400). It triggers an immediate, clean self-termination to protect the database.</li>
  <li><b>Infinite JIT Allocation:</b> Dynamically scans the timeline for the absolute tail pointer, compiling the next 180-video matrix in RAM.</li>
</ul>

<hr size="2" color="#e1e4e8">

<h2>2. Full Tech Stack & Toolchain Matrix</h2>
<table border="1" width="100%" cellspacing="0" cellpadding="8">
  <tr bgcolor="#f6f8fa">
    <th><b>Layer</b></th>
    <th><b>Tool / Library</b></th>
    <th><b>Protocol / Version</b></th>
    <th><b>Role in System</b></th>
  </tr>
  <tr>
    <td><b>Language & Paradigm</b></td>
    <td>Python</td>
    <td>3.14+</td>
    <td>Host language; C++-style bounds-checked data structures for frame buffers.</td>
  </tr>
  <tr>
    <td><b>Scraper / Downloader</b></td>
    <td>yt-dlp</td>
    <td>Latest Stable</td>
    <td>Partial time-slice extraction (1080p60) without pulling full source videos.</td>
  </tr>
  <tr>
    <td><b>AI Vision Engine</b></td>
    <td>Google Gemini</td>
    <td>google-genai / httpx</td>
    <td>Frame-level scene understanding → optimized title, description, and hashtags.</td>
  </tr>
  <tr>
    <td><b>Media Engine</b></td>
    <td>FFmpeg + MoviePy</td>
    <td>FFmpeg ≥ 6.0</td>
    <td>Format conform (16:9 → 9:16 Shorts format), audio ducking, text burn-in.</td>
  </tr>
  <tr>
    <td><b>Cloud API</b></td>
    <td>YouTube Data API v3</td>
    <td>google-api-python</td>
    <td>Authenticated upload, metadata attach, scheduled publish directly to Shorts.</td>
  </tr>
  <tr>
    <td><b>Orchestration</b></td>
    <td>Windows Task Scheduler</td>
    <td>OS-native</td>
    <td>Daily hardware-level trigger at 12:05 PM PKT.</td>
  </tr>
  <tr>
    <td><b>Database</b></td>
    <td>Local JSON</td>
    <td><code>queue.json</code></td>
    <td>Durable job/state ledger; no external DB dependency.</td>
  </tr>
</table>

<hr size="2" color="#e1e4e8">

<h2>3. Micro-Level Component Architecture (File-by-File)</h2>

<h3><code>main.py</code> — The Demon's Brain & State Machine</h3>
<p><b>Responsibility:</b> The absolute orchestrator. Owns the daily session lifecycle from OS wake to clean memory exit.</p>
<ul>
  <li><code>is_connected(host, port, timeout)</code>: C-style raw socket handshake against Cloudflare DNS.</li>
  <li><code>process_job(job)</code>: Returns JobState (SUCCESS, ERROR, or QUOTA_EXCEEDED).</li>
  <li><b>Constants:</b> <code>UPLOAD_LIMIT = 8</code> — A hardcap that keeps the system invisible to spam-detection algorithms.</li>
  <li><b>Exit Protocol:</b> <code>sys.exit(0)</code> acts as the ultimate thread killer via a <code>finally</code> block.</li>
</ul>

<h3><code>scheduler.py</code> — The Roster Architect</h3>
<p><b>Responsibility:</b> Generates the 90-day time horizon. Distributes robust blueprints (<code>FORTNITE_TREND</code>, <code>SPEED_RAGE_HIGHLIGHTS</code>, <code>GTA_RAW_COMEDY</code>).</p>
<ul>
  <li><b>Dynamic Memory Allocator:</b> Scans the JSON array to locate the absolute highest <code>publish_time</code> tail pointer, autonomously appending new batches.</li>
</ul>

<h3><code>vision_ai.py</code> — Multimodal Context Engine</h3>
<p><b>Responsibility:</b> Injects dynamic intelligence into the payload using Gemini Flash to analyze visual frames.</p>
<ul>
  <li><b>Fault Tolerance Masterclass:</b> If the AI API returns a 429 RESOURCE_EXHAUSTED, it catches the exception, injects generic fallback metadata, and pushes the pipeline forward.</li>
</ul>

<h3>Supporting Modules</h3>
<ul>
  <li><code>queue_manager.py</code>: The sole atomic controller of <code>queue.json</code>, preventing destructive race conditions.</li>
  <li><code>downloader.py</code>: Surgical extraction using yt-dlp to pull exact time-slices.</li>
  <li><code>processor.py</code>: The heavy-lifting CPU engine conforming 16:9 widescreen to 9:16 vertical, dynamically routing audio.</li>
  <li><code>uploader.py</code>: Handles OAuth2 handshakes and schedules the <code>publishAt</code> payloads.</li>
</ul>

<hr size="2" color="#e1e4e8">

<h2>4. Step-by-Step Autonomous Lifecycle Guide</h2>
<ol>
  <li><b>OS Awakening:</b> 12:05 PM PKT Windows Task Scheduler fires an OS-level interrupt; <code>main.py</code> boots.</li>
  <li><b>Network Handshake:</b> C-style socket ping to Cloudflare (1.1.1.1).</li>
  <li><b>Queue Polling:</b> Queries <code>queue.json</code> for the next pending task.</li>
  <li><b>JIT Allocation Check:</b> If 0 pending jobs remain, the allocator triggers and injects 180 new scheduled posts into the database atomically.</li>
  <li><b>Smart Cache Check:</b> Searches local SSD for pre-compiled payloads.</li>
  <li><b>Surgical Extraction:</b> <code>downloader.py</code> pulls the exact video chunk into memory.</li>
  <li><b>Vision AI Pass:</b> Gemini analyzes the visual frame to construct dynamic Shorts metadata.</li>
  <li><b>FFmpeg Matrix:</b> 9:16 vertical conversion, audio ducking, text burning, and high-bitrate export.</li>
  <li><b>API Push:</b> Payload authenticated and shipped to Google servers with an ISO-8601 publish date.</li>
  <li><b>Garbage Collection:</b> <code>finally</code> block ruthlessly wipes temp files and rendered assets from the SSD.</li>
  <li><b>Power Down:</b> Upon hitting 8 uploads, the Demon executes <code>sys.exit(0)</code>.</li>
</ol>

<hr size="2" color="#e1e4e8">

<h2>5. The Loophole Matrix: Obvious & Silent Traps Neutralized</h2>
<table border="1" width="100%" cellspacing="0" cellpadding="8">
  <tr bgcolor="#f6f8fa">
    <th><b>The Loophole / Trap</b></th>
    <th><b>The Engineered Solution</b></th>
  </tr>
  <tr>
    <td><b>Volatile RAM Persistence (Silent Trap):</b> Using a 24-hour Python <code>time.sleep()</code> loop keeps the script in memory, risking silent thread death.</td>
    <td><b>Hardware OS Interrupts:</b> The Python script is shut down completely after every run. Booted daily at 12:05 PM directly by the kernel.</td>
  </tr>
  <tr>
    <td><b>API Spam Flagging (Obvious Trap):</b> Pushing too many videos via API triggers Google's bot-detection algorithms.</td>
    <td><b>The Hardcap Limit:</b> Injected an <code>UPLOAD_LIMIT = 8</code> counter to cleanly self-terminate.</td>
  </tr>
  <tr>
    <td><b>Quota Exhaustion Corruption (Silent Trap):</b> Hitting a 429 Limit error mid-upload marks the video as "failed" permanently in standard loops.</td>
    <td><b>Quota-Aware State Machine:</b> Intercepts 429/400 codes explicitly, reverts the job to "pending", and shuts down safely.</td>
  </tr>
  <tr>
    <td><b>SSD Asphyxiation (Obvious Trap):</b> Rendering high-bitrate video daily consumes hundreds of gigabytes.</td>
    <td><b>Zero-Bloat Garbage Collection:</b> A strict <code>finally</code> block guarantees chunks/outputs are permanently deleted instantly.</td>
  </tr>
  <tr>
    <td><b>Database Overwrite Collisions (Silent Trap):</b> Naively running a 90-day generator mid-cycle overwrites existing scheduled posts.</td>
    <td><b>Absolute Tail-Pointer Tracking:</b> Dynamic allocator scans the JSON array, finds the absolute max date, and appends exactly +1 day later.</td>
  </tr>
</table>

<hr size="2" color="#e1e4e8">

<h2>6. Proof of Work</h2>
<p><i>(Note: The source code for this proprietary JIT architecture remains closed-source to protect the intellectual property.  Below are the snapshots of the modular file hierarchy and the terminal on the host machine.)</i></p>

<h3>Internal System Architecture Snapshot</h3>

<img width="163" height="425" alt="image" src="https://github.com/user-attachments/assets/81ed7533-d264-44ed-8ce1-33b46db132e6" />

<img width="585" height="448" alt="image" src="https://github.com/user-attachments/assets/db9a5c22-64fd-4331-85cc-a40618107d7f" />

