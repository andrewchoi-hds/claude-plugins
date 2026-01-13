# Changelog

All notable changes to session-wrap plugin will be documented in this file.

---

## [1.1.0] - 2026-01-13

### Added

#### Dynamic Language Detection
- Automatic language detection based on trigger language
- `[LANG: ko]` tag for Korean output
- `[LANG: en]` tag for English output
- All 5 agents now support bilingual output templates

#### Expanded Triggers (24 → 65+)
New trigger categories:
| Category | Examples |
|----------|----------|
| Spacing variants | 세션정리, 세션 정리 |
| Ending variants | 정리하자, 정리할까, 정리해줘 |
| Honorifics | 정리해주세요, 마무리해주세요 |
| English variants | wrap it up, let's wrap, done for today |
| Mixed (KR/EN) | wrap 해줘, 세션 wrap |

#### Phase 3 User Selection
Complete implementation with 5 action options:
1. Create commit
2. Update CLAUDE.md
3. Create automation
4. Save to TIL.md
5. Save to TODO.md

### Changed

#### Improved Output Format
- All agents now use table-based structured output
- Consistent format across all 5 agents:
  - doc-updater
  - automation-scout
  - learning-extractor
  - followup-suggester
  - duplicate-checker

**Before:**
```markdown
- [Section]: [Content] — [Reason]
```

**After:**
```markdown
| Item | Content |
|------|---------|
| **Content to Add** | [Specific content] |
| **Rationale** | [Pattern found in session] |
```

### Files Changed
- `.claude/agents/*.md` - All 5 agent files
- `.claude/commands/wrap.md` - Language detection + Phase 3 logic
- `.claude/settings.json` - Trigger expansion (v1.1.0)
- `CLAUDE.md` - Updated improvement checklist

---

## [1.0.0] - 2026-01-12

### Initial Release

#### Features
- `/wrap` command for session wrap-up
- 5 analysis agents:
  - doc-updater: Documentation update suggestions
  - automation-scout: Automation opportunity detection
  - learning-extractor: TIL extraction
  - followup-suggester: Follow-up task suggestions
  - duplicate-checker: Duplicate validation
- Phase-based workflow (parallel → sequential → interactive)
- 24 Korean/English triggers
- Korean-first output

---

## Roadmap

### P1 (High)
- [ ] English README

### P2 (Medium)
- [ ] Phase 3 action validation
- [ ] TODO.md auto-save verification

### P3 (Low)
- [ ] Japanese/Chinese support
- [ ] Performance optimization
