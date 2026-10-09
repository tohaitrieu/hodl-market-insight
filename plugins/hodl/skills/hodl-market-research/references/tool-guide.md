# Cẩm nang 10 tool của MCP server hodl

Mọi tool chỉ đọc. Mỗi kết quả có dạng `{data, source{name, attribution, url, as_of}, disclaimer}`.

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `search_instruments` | Free | Chưa chắc mã | `query` (mã/tên VI/EN), `asset_class` (stock, index, forex, crypto, commodity), `limit` ≤ 20 |
| `get_quote` | Free | Giá hiện tại | `symbol` (FPT, VNINDEX, EURUSD, BTCUSD, GOLD…) |
| `get_market_overview` | Free | Toàn cảnh thị trường | `asset_class` (mặc định stock: độ rộng, VN-Index, Hot VN30; lớp khác: mã biến động mạnh nhất) |
| `get_price_history` | Free | Nến OHLCV | `symbol`, `timeframe` D1/W1/H4, `bars` |
| `get_financials` | Free | BCTC cổ phiếu VN | `symbol`, `period` quarter/year, `statement` (bảng đầy đủ — Loyalty) |
| `get_technical_snapshot` | **Loyalty** | Chỉ báo kỹ thuật | `symbol`, `timeframe` — RSI14, MACD, EMA20/50/200, Bollinger, Stochastic, áp lực mua–bán, động lượng 1T/3T/6T/1N |
| `search_articles` | Free | Bài phân tích, bài học | `query`, `limit` ≤ 10 — chỉ tiêu đề, trích đoạn, link |
| `get_macro_indicators` | Free | Tìm chỉ số vĩ mô | `country`, `category` (inflation, growth, trade, labor, monetary, demographics, market_participation), `query`, `headline_only` |
| `get_macro_series` | Free | Chuỗi số một chỉ số | `indicator` (slug), `date_from`, `date_to`, `points` |
| `get_etf_flows` | Free | Dòng tiền ETF | `asset` (bitcoin, ethereum, solana, gold), `timeframe` D/W/M/Q/Y, `periods`, `fund` (vàng: GLD, GLDM, SGLD) |

## Hạn mức theo gói

| Hạng mục | Free | Loyalty |
|---|---|---|
| Lượt gọi | 10/phút, 100/ngày | 60/phút, 2.500/ngày |
| Nến lịch sử | D1 30, W1 12, H4 200 | 1.000 mọi khung |
| BCTC | 4 quý / 3 năm, chỉ tiêu chính | 8 quý / 5 năm, bảng đầy đủ |
| Kỳ vĩ mô | 12 | 240 |
| Kỳ ETF | 30 | 365 |
| Ảnh chụp kỹ thuật | — | Có |

Bảng cập nhật mới nhất: https://hodl.vn/ai. Mỗi tài khoản (Free lẫn Loyalty) có 1 API key.

## Mẹo

- Gộp câu hỏi: một `get_quote` đã có P/E, P/B, ROE — không cần gọi `get_financials` chỉ để lấy các số này.
- Gói Free muốn RSI/EMA: lấy `get_price_history` (D1, 30 nến) rồi tự tính, nói rõ số nến dùng.
- Vĩ mô so sánh nhiều nước: `get_macro_indicators` với `country: G7` + `query`, rồi gọi `get_macro_series` cho từng slug.
- Đơn vị BCTC là tỷ đồng; ETF là triệu USD; vĩ mô xem `unit` của từng chỉ số.
