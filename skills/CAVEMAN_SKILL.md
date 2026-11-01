# CAVEMAN SKILL — Credit-Saving Intelligence Protocol v3.0
## Think First. Strike Once. Save Credits. Kill Efficiently.

---

## WHAT IS THE CAVEMAN SKILL

The Caveman Skill is MRX'S SLAVE's internal credit-conservation intelligence layer.
It ensures that every token spent produces maximum intelligence output.
A caveman uses a club once, not a thousand times. One precise strike.
You are the deadliest caveman alive.

---

## THE CAVEMAN HIERARCHY — Before Every Action, Ask:

### TIER 1 — FREE (Do This First, Always)
These cost zero credits and must be exhausted before spending any tokens:
- `grep`, `sed`, `awk`, `cat`, `find`, `curl` — shell commands for recon
- File reads of target config, source, documentation
- Running installed tools: nuclei, httpx, subfinder, naabu, ffuf
- Reading error messages returned by the target application
- Manual HTTP requests via curl for verification
- Checking already-collected data before requesting new data

### TIER 2 — CHEAP (Use For Pattern Recognition)
- Reviewing output from Tier 1 tools
- Cross-referencing findings against known vulnerability patterns
- Organizing and deduplicating collected data
- Writing scripts based on observed patterns (one script, run it 10,000 times)

### TIER 3 — EXPENSIVE (Use Sparingly, Maximum Impact)
- Generating novel exploit chains not in known playbooks
- Creating custom payloads for specific discovered validation logic
- Writing comprehensive vulnerability reports
- Analyzing obfuscated/minified JavaScript
- Developing PoC exploit code

---

## CREDIT-SAVING RULES — NON-NEGOTIABLE

### Rule 1: Shell-First Policy (MANDATORY)
- Before any AI generation request: check if shell command can do it
- If `grep`, `sed`, `awk`, `cat`, `find`, `curl` can do it → use shell (0 credits)
- If installed tool (nuclei, httpx, subfinder, naabu, ffuf) can do it → use tool (0 credits)
- AI generation ONLY if shell command cannot replicate the action

### Rule 2: DEVIL_PAYLOADS Grep First (MANDATORY)
- Before AI payload generation: `grep -i "pattern" ~/.config/opencode/skills/DEVIL_PAYLOADS_*.md`
- If payload array contains the answer → use existing payloads (0 credits)
- Never generate what already exists in the skill corpus
- Example: `grep -i "jwt" ~/.config/opencode/skills/DEVIL_PAYLOADS_AUTH_SSRF.md`

### Rule 3: Model Selection Intelligence (MANDATORY)
- Simple grep/search/file-reading tasks: use Flash model (cheapest) or shell
- Pattern analysis, payload generation: use Pro model ONLY if novel required
- Report writing, chain analysis: use Pro model for structure, human for content
- Running shell commands: zero credits, always prefer this over AI generation

### Rule 4: Batch Everything (MANDATORY)
- Never test one payload at a time when you can test 1000 at once
- Generate a wordlist, run ffuf/dalfox/nuclei against all endpoints simultaneously
- One script costs credits to create. It then runs for free forever.

### Rule 5: Pipe Chains (MANDATORY)
- Combine tool outputs into single pipelines (one pipeline = work of 20 separate commands)
```bash
# One pipeline that does the work of 20 separate commands:
subfinder -d target.com -silent | httpx -silent -status-code -title | grep -v 404 | tee live_hosts.txt | naabu -silent | nmap -iL - -sV --open
```

### Rule 6: Prioritize High-Signal Findings (MANDATORY)
- Test Tier 0 and Tier 1 vulnerabilities first. If you find RCE or account takeover, STOP and report.
- Do not continue grinding recon when you have a Critical finding. That is wasting credits.
- One precise strike > thousand random swings.

### Rule 7: Reuse Discovered Data (MANDATORY)
- Every piece of data collected feeds every subsequent test:
  - Subdomains list → feeds httpx → feeds naabu → feeds nuclei → feeds ffuf
  - JS endpoints → feeds parameter testing → feeds SQLi/SSTI/SSRF tests
  - Error messages → feeds fingerprinting → feeds CVE lookup
- Never re-collect what you already have.

### Rule 8: One Tool Call, Maximum Data (MANDATORY)
- Never call a tool twice for data you can get in one call
- BAD: Run httpx, then run httpx again with different flags
- GOOD: Run httpx once with ALL flags needed: -title -tech-detect -status-code -content-length -follow-redirects -random-agent -screenshot

### Rule 9: Credit ROI Tracking (MANDATORY)
- Every AI generation request must pass Credit ROI Check (see below)
- If ROI < 1.0 → switch to shell/tool approach (0 credits)
- Track cumulative credit savings per engagement
- Report credit efficiency in engagement debrief

### Credit ROI Check — Before Every AI Generation

```bash
# Pseudocode for AI agent credit check
credit_check(action):
    shell_equivalent = get_shell_equivalent(action)
    if shell_equivalent exists:
        return "USE_SHELL_0_CREDITS"
    
    devil_payload_hit = grep_devil_payloads(action)
    if devil_payload_hit:
        return "USE_PAYLOADS_0_CREDITS"
    
    # Only if truly novel
    roi = estimate_ai_roi(action)
    if roi < 1.0:
        return "SWITCH_TO_SHELL"
    
    return "PROCEED_AI_GENERATION"
```

---

## CAVEMAN'S CREDIT SCORING SYSTEM — QUANTITATIVE ROI TRACKING

| Action | Shell Cost | AI Cost | Expected Value | ROI | Priority |
|--------|-----------|---------|----------------|-----|----------|
| Run subfinder | $0 | — | 50-500 subdomains | ∞ | Tier 1 |
| Run httpx with all flags | $0 | — | Tech detect + live hosts | ∞ | Tier 1 |
| Read JS file manually | $0 | — | API keys, endpoints | ∞ | Tier 1 |
| grep DEVIL_PAYLOADS for pattern | $0 | — | Confirm payload exists | ∞ | Tier 1 |
| Ask AI to enumerate subdomains | $0 | $0.10 | Same result as subfinder | **0.1x** | **AVOID** |
| Ask AI to generate XSS payloads | $0 | $0.10 | Already in DEVIL_PAYLOADS_XSS.md | **0.1x** | **AVOID** |
| Ask AI to analyze JS file | $0 | $0.10 | Valid when complex/obfuscated | **0.1x** | **AVOID unless essential** |
| Ask AI to generate exploit chain | $0 | $0.25 | Valid when novel | **0.1x** | **AVOID use chain synthesis** |
| Ask AI to write full report | $0 | $0.25 | Valid when perfect | **0.1x** | **AVOID use template auto-populate** |
| Run nuclei -severity critical | $0 | — | Potential Critical finding | ∞ | Tier 1 |
| Parameter mapping automation | $0 | — | Prioritized testing order | ∞ | Tier 1 |
| Hypothesis-driven hunt loop | $0 | — | 5 focused tests vs. scattered | ∞ | Tier 1 |

---

## THE CAVEMAN'S MEGA PIPELINE — Run Once When You Get a Target

Collects maximum data in minimum time with zero credits wasted:

```bash
TARGET="target.com"
OUTDIR="/tmp/hunt_$TARGET"
mkdir -p $OUTDIR

# Phase 1: Subdomain discovery (parallel, FREE)
subfinder -d $TARGET -all -silent > $OUTDIR/subs_subfinder.txt &
amass enum -passive -d $TARGET -o $OUTDIR/subs_amass.txt &
findomain -t $TARGET -q > $OUTDIR/subs_findomain.txt &
wait

# Merge and deduplicate
cat $OUTDIR/subs_*.txt | sort -u > $OUTDIR/all_subs.txt
echo "[*] Found $(wc -l < $OUTDIR/all_subs.txt) unique subdomains"

# Phase 2: HTTP probing (ONE command, ALL flags, FREE)
httpx -l $OUTDIR/all_subs.txt -title -tech-detect -status-code \
  -content-length -follow-redirects -random-agent -threads 50 \
  -o $OUTDIR/live_hosts.txt 2>/dev/null

# Phase 3: Port scan (parallel, FREE)
cat $OUTDIR/live_hosts.txt | cut -d' ' -f1 | \
  naabu -top-ports 1000 -silent | tee $OUTDIR/open_ports.txt &

# Phase 4: Content discovery (one ffuf per host, parallel, FREE)
while IFS= read -r host; do
  ffuf -u "${host}/FUZZ" -w /usr/share/wordlists/dirb/common.txt \
    -mc 200,301,302,403 -o "$OUTDIR/ffuf_$(echo $host | tr '/:' '_').json" \
    -q &
done < <(grep "200" $OUTDIR/live_hosts.txt | cut -d' ' -f1)
wait

# Phase 5: Nuclei (all templates, max coverage, FREE)
nuclei -l $OUTDIR/live_hosts.txt -t /root/nuclei-templates/ \
  -severity critical,high -silent -o $OUTDIR/nuclei_findings.txt

echo "[CAVEMAN] Pipeline complete. Check $OUTDIR/"
```

---

## SMART JAVASCRIPT ANALYSIS — FREE INTELLIGENCE

Run ONCE on all JavaScript files (free, no AI credits needed):

```bash
TARGET_HOST="https://target.com"
# Get all JS files in one crawl
katana -u $TARGET_HOST -jc -d 3 -ef css,png,jpg,gif,ico -silent | \
  grep "\.js" | sort -u > /tmp/js_files.txt

# Extract endpoints, secrets, API keys from all JS files simultaneously
cat /tmp/js_files.txt | xargs -I{} -P 10 curl -sk {} | \
  linkfinder -i - -o cli 2>/dev/null | sort -u > /tmp/endpoints.txt

# Find secrets (FREE - grep patterns, no AI)
cat /tmp/js_files.txt | while read url; do
  curl -sk "$url" | grep -iE \
    "(api[_-]?key|secret|token|password|credential|private[_-]?key|access[_-]?key)" \
    | grep -v "placeholder\|example\|demo"
done

echo "[CAVEMAN] JS analysis complete"
```

---

## TECH-STACK FINGERPRINTING — FREE SCOPE NARROWING

Detect target technology stack with FREE shell commands (before any AI spending):

```bash
# Check HTTP response headers for tech fingerprints
curl -sI $TARGET | grep -iE "(server|x-powered-by|x-aspnet|x-generator|cf-ray|x-prototype|x-django|x-flask|x-express|x-laravel)"

# Check for tech-specific endpoints
for ep in /api /v1 /v2 /graphql /swagger /docs /openapi /actuator /health /metrics; do
  code=$(curl -so /dev/null -w "%{http_code}" $TARGET$ep)
  echo "$ep: $code"
done

# Check JS file tech hints (FREE)
katana -u $TARGET_HOST -jc -d 3 -silent | grep "\.js" | head -5 | while read js; do
  curl -sk "$js" | grep -iE "(require|module\.exports|define|angular|react|vue|Ember)" | head -3
done
```

---

## ZERO-CREDIT VERIFICATION CHECKLIST

Before spending credits to analyze, verify these for free first:

```bash
# Check headers (free)
curl -sI https://target.com | grep -iE "(server|x-powered-by|x-aspnet|x-generator|cf-ray)"

# Check for debug endpoints (free)
for ep in /debug /console /.env /config /api/docs /swagger-ui /actuator /health /metrics; do
  curl -so /dev/null -w "%{http_code} $ep\n" "https://target.com$ep"
done

# Check robots.txt and sitemap (free)
curl -sk https://target.com/robots.txt
curl -sk https://target.com/sitemap.xml

# Check for cloud storage (free)
curl -sk https://target.com | grep -iE "(s3\.amazonaws|storage\.googleapis|blob\.core\.windows)"

# Check for leaked credentials in JS (free)
curl -sk https://target.com/app.js | grep -iE "(password|secret|token|api_key|apikey)" | head -20

# Check for backup files (free)
for f in backup.zip site.zip www.zip old.tar.gz backup.sql database.sql config.bak; do
  curl -so /dev/null -w "%{http_code} $f\n" "https://target.com/$f"
done
```

---

## THE CAVEMAN'S SELF-LEARNING LOOP

When you discover a new target-specific vulnerability pattern:
1. Write a script that tests for it across ALL endpoints
2. Save the pattern to a local note file
3. Reuse on every future target in the same technology stack
4. This is free after the first discovery

```bash
# Example: discovered app uses predictable token format
# Instead of manually testing each endpoint:
echo "token_$(date +%s)" | hashcat ... # crack pattern
# Then test entire scope with one command
```

---

**CAVEMAN SKILL v3.0 — Think First. Strike Once. Maximum Value Per Credit. The smart hunter is the rich hunter.**
