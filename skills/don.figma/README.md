# don.figma

Quick guide cho skill đọc Figma theo `node-id` để cấp context sạch cho artifact BSA.

`SKILL.md` là source of truth. README này chỉ giữ quick-start và boundary vận hành.

## Mục đích

Skill này dùng để:
- Fetch đúng scope của một screen/component Figma
- Kiểm tra `accessState` trước khi tin dữ liệu
- Ghi output có cấu trúc để đưa sang `don.artifact`

## Khi nào dùng

Dùng khi bạn cần:
- đọc 1 màn hình Figma theo `node-id`
- lấy layout, text labels, CTA, states
- chuẩn bị input cho Screen Description / SRS / User Story
- xử lý case MCP bị `429`, throttled, gated, ambiguous

Không dùng khi:
- chỉ có file URL chung, chưa có `node-id`
- đang brainstorm UI chung chung, chưa cần source-of-truth từ Figma
- muốn viết artifact hoàn chỉnh mà bỏ qua bước screen-context extraction

## Input cần chuẩn bị

1. `figma_url` có `node-id` hoặc `node-id` cụ thể
2. `scope`
   Ví dụ: `screen layout`, `text labels`, `CTA buttons`, `states`
3. `artifact target`
   Ví dụ: `Screen Description`, `User Story`, `SRS`, `ERD`
4. `access`
   Ví dụ: `team file`, `locked file`

## Hard stop

- Không có `node-id` -> dừng, yêu cầu scope hẹp hơn
- Không rõ target screen/component -> dừng, yêu cầu xác định lại node
- User muốn full document -> fetch context trước, rồi mới route sang `don.artifact`

## Cách dùng

```text
Dùng `don.figma` để fetch màn hình này:
https://www.figma.com/design/FILE_KEY/NAME?node-id=254-732
Scope: screen layout, text labels, CTA buttons
Artifact target: Screen Description
Access: team file
```

## Flow thực thi

- MCP-first
- Chrome remote-debug fallback khi bị throttle, gate, ambiguity
- Luôn classify lỗi trước khi retry
- Luôn verify đúng node và `gated=false`

Chi tiết flow nằm ở:
- `SKILL.md`
- `references/fetch-and-fallback.md`

## Luật quan trọng

- Không fetch cả file nếu chỉ cần 1 screen
- Không assume dữ liệu hợp lệ nếu chưa xác nhận `gated=false`
- Exact text only, không paraphrase label/CTA
- Nếu dữ liệu partial, phải đánh dấu partial thay vì điền bù

## Output contract

```text
{output_folder}/figma-data-{node-id}.md
```

Output tối thiểu gồm:
- `Date`
- `Node ID`
- `Figma URL`
- `Fetch method`
- `accessState`
- `Scope captured`
- `Verification status`
- `Screen Layout`
- `Text Labels`
- `CTA / Action Buttons`
- `States`
- `Components Referenced`
- `Partial Areas / Verification Notes`
- `Open Questions for BA`

## Gate check trước khi đưa sang artifact

- `accessState` đã là `gated=false`
- `node-id` đúng với màn hình cần lấy
- text labels là exact strings, không paraphrase
- CTA và states đã đủ
- partial area hoặc blocked area đã được gọi ra nếu có
- open questions đã được liệt kê

## Kết hợp với skill khác

- Dùng tiếp `don.artifact` để tạo:
  - Screen Description
  - User Story
  - SRS
- Nếu cần output compact hơn cho downstream parsing, dùng bước compact context tương ứng

## File liên quan

- Skill definition: [SKILL.md](./SKILL.md)
- Fetch flow: [`references/fetch-and-fallback.md`](./references/fetch-and-fallback.md)
- Downstream artifact skill: `don.artifact`
- Compact context step: compact context tương ứng
