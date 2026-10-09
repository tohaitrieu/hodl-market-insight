---
name: hodl-market-research
description: Tra cứu giá, kỹ thuật, báo cáo tài chính cổ phiếu Việt Nam (HOSE/HNX/UPCoM), VN-Index, vĩ mô Việt Nam và thế giới, dòng tiền ETF, forex, crypto, vàng/dầu và bài phân tích của HODL.VN qua MCP server hodl. Use when the user asks about Vietnamese stocks (tickers like FPT, VCB, HPG), VN-Index, VN30, Vietnamese or world macro data (CPI, GDP, interest rates), Bitcoin/gold ETF flows, forex pairs, crypto, gold or oil prices, or wants Vietnamese market analysis with cited sources.
license: MIT
compatibility: Cần MCP server hodl (https://mcp.hodl.vn/mcp) và API key miễn phí tại https://hodl.vn/tai-khoan/ket-noi-ai
metadata:
  author: HODL.VN
  version: "1.0.0"
---

# Nghiên cứu thị trường với HODL.VN

Dữ liệu đến từ MCP server `hodl` (11 tool, chỉ đọc). Cổ phiếu, chỉ số Việt Nam, vĩ mô và ETF ghi nguồn HODL.VN; forex, crypto, hàng hoá ghi nguồn totrieu.com.

Nếu không thấy tool `hodl` nào trong phiên: báo người dùng cài MCP theo https://hodl.vn/ai. Có công cụ đọc web thì đọc `https://hodl.vn/llms.txt` và trang `https://hodl.vn/stock/<mã viết thường>` (vd. `/stock/fpt`). **Không bao giờ bịa số liệu.**

## Quy trình

### Cổ phiếu / chỉ số Việt Nam
1. Chưa chắc mã → `search_instruments` (mã hoặc tên công ty; tên thương hiệu như "Vinamilk" không có — dùng mã VNM hoặc tên "Sữa Việt Nam").
2. `get_quote` — giá, % thay đổi, biên độ ngày/52 tuần, P/E, P/B, ROE, ngành, bài liên quan.
3. Tuỳ câu hỏi:
   - Cơ bản → `get_financials` (`period` quarter|year). Giá trị tiền tệ là **tỷ đồng**.
   - Kỹ thuật → `get_technical_snapshot` (Loyalty) hoặc tự tính từ `get_price_history`.
   - Bối cảnh thị trường → `get_market_overview` (`asset_class: stock`).
4. `search_articles` để kèm bài phân tích HODL.VN (chỉ có tiêu đề, trích đoạn, link).

Giá lịch sử cổ phiếu Việt Nam **đã điều chỉnh** theo cổ tức/chia tách — đừng so trực tiếp với giá vốn thô của người dùng mà không nói rõ.

### Forex, crypto, hàng hoá
`search_instruments` (`asset_class` forex|crypto|commodity) → `get_quote` → `get_price_history` (D1/W1/H4). Biến động mạnh nhất: `get_market_overview` với `asset_class` tương ứng. Ví dụ mã: EURUSD, BTCUSD, GOLD, USOIL.

### Vĩ mô (Việt Nam hoặc thế giới)
1. `get_macro_indicators` — lọc `country` (VN, US, CN, JP, DE, GB, FR, IT, CA, EA, `world`, G7), `category`, `query` ("CPI", "lãi suất", "GDP"…).
2. `get_macro_series` với `slug` vừa nhận.
3. **Đọc `unit` và `measure` trước khi diễn giải**: `yoy_pct` = % so cùng kỳ năm trước, khác với mức tuyệt đối. Kỳ có giai đoạn công bố sơ bộ/chính thức — nói rõ khi số còn sơ bộ.

### Dòng tiền ETF (Bitcoin, Ethereum, Solana, vàng)
`get_etf_flows` — bỏ trống `asset` = tóm tắt phiên mới nhất cả bốn; có `asset` + `timeframe` (D/W/M/Q/Y) + `periods` = chuỗi theo kỳ; `fund` (GLD/GLDM/SGLD) chỉ dùng cho vàng. **Mọi dòng tiền là triệu USD**; dương = tiền vào, âm = tiền ra; quỹ `null` = chưa báo cáo kỳ đó.

### Khối ngoại, tự doanh (cổ phiếu Việt Nam)
`get_investor_flows` — bỏ trống `symbol` = toàn sàn (`exchange`, thêm `include_leaders` để lấy top mua/bán ròng); có `symbol` = chuỗi của riêng mã. **Giá trị là tỷ đồng** (`unit: billion_vnd`); dương = mua ròng, âm = bán ròng. Mặc định `basis: matched` chỉ tính lệnh khớp — giao dịch thoả thuận lớn có thể làm số `total` lệch hẳn (một phiên thoả thuận nghìn tỷ ở một mã), nên khi nói "khối ngoại bán ròng" hãy nêu rõ thang đo. Kỳ `is_partial` = chưa kết thúc, nói rõ là số tạm.

## Luật trả lời

- **Luôn dẫn nguồn**: mỗi kết quả có `source.url` và `source.attribution` — đưa link vào câu trả lời, ghi "Nguồn: HODL.VN" (hoặc totrieu.com cho forex/crypto/hàng hoá).
- **Luôn nêu miễn trừ** trong `disclaimer`: thông tin tham khảo, không phải khuyến nghị đầu tư. Không biến số liệu thành lời khuyên mua/bán.
- Trả lời bằng ngôn ngữ người dùng đang dùng. Số tiếng Việt dùng dấu chấm phân cách nghìn, dấu phẩy thập phân.
- Nêu thời điểm dữ liệu (`source.as_of`) khi nói về giá.
- Bài viết chỉ có trích đoạn — muốn đọc đầy đủ, mời người dùng mở link. Không đoán nội dung phần còn lại.
- Không có dữ liệu thành viên (nhật ký, vị thế, danh mục, watchlist) — nói thẳng nếu được hỏi.

## Lỗi và giới hạn gói

| Mã lỗi | Cách xử lý |
|---|---|
| `tier_denied` | Tính năng chỉ cho Loyalty. Chuyển nguyên thông điệp + `upgrade_url`; dùng cách thay thế ở gói Free nếu có (vd. tự tính chỉ báo từ `get_price_history`). Không gọi lại cùng tool. |
| `rate_limited` | Quá nhiều lượt/phút — chờ rồi thử lại một lần. |
| `quota_exceeded` | Hết lượt trong ngày — báo người dùng, đưa `upgrade_url`. |
| `not_found`, `invalid_symbol` | Thử `search_instruments` để tìm mã đúng. |
| `unauthenticated` (HTTP 401) | Key sai hoặc chưa đặt — hướng dẫn lấy key tại https://hodl.vn/tai-khoan/ket-noi-ai. |

Số nến/kỳ trả về có thể ít hơn yêu cầu do giới hạn gói — kết quả ghi rõ; nói với người dùng thay vì ngầm coi là đủ.

Chi tiết từng tool và hạn mức: [references/tool-guide.md](references/tool-guide.md). Thuật ngữ tài chính Việt Nam: [references/glossary-vi.md](references/glossary-vi.md).
