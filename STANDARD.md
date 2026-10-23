# Skill Trust Grading Standard v1.0

Frozen 2026-10-23, before any grading under it. Amendments are appended with dates, never edited silently. Grades issued under this standard name its version.

## What is graded

An agent skill: a folder containing a SKILL.md and any bundled scripts, references, or assets, as published in a public source repository and listed on the skills.sh directory. The graded object is the skill's source at a pinned commit. The directory listing is never evidence; it supplies only the corpus (rank and install count at snapshot).

This standard grades TRUST: whether a skill does what it says, asks only for what its job needs, and discloses what it does with access and data. It does not grade effectiveness. Whether a skill makes an agent's output better is a different question, answered by other instruments.

## Corpus rule

The top 20 skills by installs on skills.sh, snapshot on the freeze date, frozen as selected. Router skills (whose function is to find, recommend, or install other skills) are in the corpus when they rank in the top 20 and are graded under the router rule below.

## Dimensions

Each dimension is marked PASS, FLAG, or FAIL. Every mark cites the file and the quoted line or lines it rests on. A mark with no quoted evidence does not stand.

**D1. Claims against content.** The skill's name, description, and stated purpose are checked against what its instructions and bundled files actually do. Material contradiction (the content does something the description denies or omits as a headline behavior) is a FAIL. Loose or puffy wording that the content substantially honors is a FLAG at most.

**D2. Permissions surface.** Every file read, file write, shell command, and network endpoint the skill directs the agent to use is listed, then checked against the skill's stated job. Access the job needs: PASS. Access beyond the job that is disclosed in the skill text: FLAG. Access beyond the job that runs by default and is not disclosed: FAIL.

**D3. Credential asks.** Every key, token, or secret the skill names is listed. An ask the job requires, with storage guidance that keeps the value out of the skill's own files and out of outbound payloads: PASS. An ask broader than the job, or storage guidance that is absent where the value is sensitive: FLAG. An ask for a credential the stated job cannot need, or any instruction to place a secret value inside a file the skill ships or sends: FAIL.

**D4. Outbound data.** Every destination data leaves the machine for is listed, with the class of data sent. Destinations and data classes disclosed in the skill text: PASS. A destination disclosed but the data class vague: FLAG. Any transmission of user data, file contents, or conversation content to a destination the skill text does not name: FAIL.

**D5. Instruction hygiene.** The skill and every bundled file are read for: instructions to override, ignore, or conceal from the agent's standing instructions or the user; instructions to hide the skill's own actions; code or commands that execute at install time; self-modification of the agent's other skills, memory, or configuration. Any one of these present: FAIL. Aggressive self-promotion inside instructions (the skill steering the agent to recommend itself or its siblings unbidden): FLAG.

**D6. Provenance and maintenance.** Author identity, source repository, license presence, version history, and time since last update are recorded as facts. A named author, a public history, and a license: PASS. A pseudonymous author with a public history: FLAG at most. No identifiable source repository, or a listing whose source cannot be opened: the skill is NOT GRADEABLE (see verdicts), not failed on suspicion.

## Verdicts

The overall verdict is derived from the dimension marks by rule, not assigned by feel:

- **CLEAN**: no FAIL, at most one FLAG.
- **OVERBROAD**: FAIL on D2 or D3, and no FAIL on D1, D4, or D5. The skill does its stated job but takes more access or more credential than the job needs.
- **UNDISCLOSED**: FAIL on D4, or a FAIL on D2 or D3 whose failing element is the non-disclosure. The skill moves data or access it never mentions.
- **DECEPTIVE**: FAIL on D1 (material contradiction) or FAIL on D5. The skill says one thing and does another, or reaches for the agent's own instructions.
- **NOT GRADEABLE**: the source cannot be opened at a pinned commit, or the listed item is not a skill package. The record states why.

Where two verdicts could apply, the more severe stands, in the order DECEPTIVE, UNDISCLOSED, OVERBROAD, CLEAN.

## Router rule

A router skill is graded on: whether its selection criteria are stated in its text and checkable (D1); whether installing a recommended skill requires the user's confirmation in its instructions (D2); what it fetches from the network and executes during a recommendation or install (D4, D5). It is not graded on the quality of the skills it points to, and never on task output.

## Fleet ruling (internal column)

Each graded skill also receives a ruling for our own machines, derived by rule:

- CLEAN: RUN.
- OVERBROAD or one FLAG on D2/D3/D4 in an otherwise clean record: RUN SANDBOXED (no standing credentials, no fleet data paths).
- UNDISCLOSED or DECEPTIVE: DO NOT RUN.
- NOT GRADEABLE: DO NOT RUN until gradeable.

## Method

Two independent grading passes over the frozen corpus, each blind to the other, both under this version of the standard. Dimension marks that differ between passes are adjudicated by a third read of the pinned source; the adjudication cites the lines it rests on. The published record shows the final marks, the verdicts, and every case where the two passes disagreed and how it settled.

Each grade records: skill name, publisher, source repository, pinned commit, install count at snapshot, standard version, grade date.

## Scope limits, stated on the record

Static reading only. No skill in the corpus is executed, installed, or run during grading. A CLEAN verdict means the source, read in full, matches its claims and discloses its surface; it is not a guarantee about behavior at runtime, about future versions, or about the publisher. Grades apply to the pinned commit only.
