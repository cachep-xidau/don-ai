# don.artifact

Quick guide cho skill viet dung 1 design artifact cua Don.

`SKILL.md` la source of truth. README nay chi giu quick-start va boundary.

## Muc dich

Skill nay dung de draft mot artifact ro loai, ro input, ro boundary.

Artifact ho tro:
- Screen Description
- User Story
- Technical Story
- Function List
- SRS
- ERD
- Use Case Diagram
- Sequence Diagram

## Khi nao dung

Dung khi ong da biet chinh xac artifact can tao.

Vi du:
- "viet User Story cho flow dang ky"
- "draft Screen Description cho man hinh checkout"
- "tao SRS cho module approval"
- "tao ERD cho order domain"

## Khi nao khong dung

Khong dung khi:
- ong moi co requirement mo ho
- ong can FR/NFR analysis, gap-impact analysis, stakeholder framing
- ong chi noi chung chung "viet design docs"
- ong can doc Figma theo `node-id` truoc khi viet artifact

Case do route sang:
- `don.analysis`
- `don.figma`

## Input can co

1. Artifact type cu the
2. Requirement context du manh de viet artifact do
3. Neu la artifact ky thuat, can system context ro rang

## Hard stop

- User noi "design docs" nhung khong chon artifact -> dung, ep chon artifact
- Context yeu nhung doi ERD / Sequence / Use Case -> dung, yeu cau bo sung
- Chua co screen context ma doi Screen Description tu Figma -> route `don.figma` truoc

## Cach dung

```text
Dung `don.artifact` de viet User Story cho flow tao ticket.
Context: da co actor, trigger, main flow, acceptance criteria draft.
```

Hoac:

```text
Dung `don.artifact` de viet SRS cho module leave request.
Context: da co pham vi, actors, business rules, integrations, non-functional constraints.
```

## Luat quan trong

- Mot lan chi viet mot artifact
- Khong tu mo rong scope thanh package nhieu artifact
- `Technical Story`, `ERD`, `Use Case`, `Sequence Diagram` la explicit-only
- Khong collapse assumption thanh fact
- Sau khi draft, phai reload reference dung loai va tu review lai

## File lien quan

- Skill definition: [SKILL.md](./SKILL.md)
- Routing rules: [`references/artifact-routing.md`](./references/artifact-routing.md)
- Downstream references: `references/*.md`
- Scoped Figma input: `don.figma`
