# don-ai

Subset chia se de cai nhanh 2 skill Don cho dong nghiep, kem `AGENTS.md` va cac rule file ma no tham chieu.

## Goi nay chua gi

- `AGENTS.md`
- `.claude/rules/development-rules.md`
- `.claude/rules/primary-workflow.md`
- `.claude/rules/documentation-management.md`
- `skills/don.figma/`
- `skills/don.artifact/`

## Boundary

- Day khong phai full Don package
- Chi ship 2 skill phuc vu doc Figma co scope va draft artifact
- Khong copy rieng `SKILL.md` roi bo `references/`, vi skill se vo path

## Khi nao nen dung

- Can share nhanh 2 skill Don cho team
- Can mot bo cai dat toi thieu, de copy vao may dong nghiep
- Can giu nguyen reference files de skill chay on dinh

## Khi nao khong nen dung

- Ong muon full Don orchestrator, commands, workflows, docs phase-gate
- Repo dich da co `AGENTS.md` rieng va governance khac

Neu repo dich da co `AGENTS.md`, dung overwrite mu. Merge co chu dich tung rule.

## Cai dat

### Cach 1: Cai vao skill registry cua may local

```bash
git clone https://github.com/cachep-xidau/don-ai.git
cd don-ai

mkdir -p "$HOME/.agents/skills"
cp -R skills/don.figma "$HOME/.agents/skills/"
cp -R skills/don.artifact "$HOME/.agents/skills/"
```

Neu can dung rule workspace:

```bash
cp AGENTS.md /path/to/your/project/AGENTS.md
mkdir -p /path/to/your/project/.claude/rules
cp -R .claude/rules/* /path/to/your/project/.claude/rules/
```

### Cach 2: Vendor vao repo noi bo

```bash
mkdir -p /path/to/your/project/skills
cp -R skills/don.figma /path/to/your/project/skills/
cp -R skills/don.artifact /path/to/your/project/skills/
cp AGENTS.md /path/to/your/project/AGENTS.md
mkdir -p /path/to/your/project/.claude/rules
cp -R .claude/rules/* /path/to/your/project/.claude/rules/
```

## Cach dung

### `don.figma`

Dung khi can:
- fetch dung 1 `node-id`
- lay layout, text labels, CTA, states
- cap context sach cho artifact downstream

Doc them:
- `skills/don.figma/README.md`
- `skills/don.figma/SKILL.md`

### `don.artifact`

Dung khi can draft dung 1 artifact:
- Screen Description
- User Story
- Technical Story
- Function List
- SRS
- ERD
- Use Case Diagram
- Sequence Diagram

Doc them:
- `skills/don.artifact/README.md`
- `skills/don.artifact/SKILL.md`

## Cau truc

```text
.
├── .claude
│   └── rules
│       ├── development-rules.md
│       ├── documentation-management.md
│       └── primary-workflow.md
├── AGENTS.md
├── README.md
└── skills
    ├── don.artifact
    │   ├── README.md
    │   ├── SKILL.md
    │   └── references/
    └── don.figma
        ├── README.md
        ├── SKILL.md
        └── references/
```

## Luu y van hanh

- `don.figma` uu tien scope hep, can `node-id` ro rang
- `don.artifact` chi viet mot artifact moi lan
- Artifact ky thuat la explicit-only. Khong hoi mo ho "design docs" roi tu mo rong scope
- `AGENTS.md` trong repo nay la ban share tu workspace goc. Co the qua chat voi mot so repo nho. Can review truoc khi ap dung team-wide
- 3 file trong `.claude/rules/` duoc bundle chi de tranh broken reference. Chung khong bien repo nay thanh full workspace template

## Sync cap nhat

Khi source goc thay doi:

1. Cap nhat file trong repo nguon noi bo
2. Replace lai `skills/don.figma`, `skills/don.artifact`, `AGENTS.md` o repo nay
3. Review diff truoc khi push
