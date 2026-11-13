# Cẩm nang 53 tool của MCP server hodl

Danh sách luôn cập nhật: https://hodl.vn/ai. Mỗi kết quả có dạng `{data, source{name, attribution, url, as_of}, disclaimer}`.
Gói: **Free** (mọi tài khoản) · **Beginner** · **Loyalty**. Tool ghi (thêm / sửa / xoá / tạo đơn) chỉ chạm tài khoản của chính người dùng.

**Quy tắc với tool ghi:** chỉ gọi khi người dùng yêu cầu rõ; nhắc lại điều sắp làm (mã, số lượng, giá, điều kiện) trước khi gọi tool sửa / xoá / tạo đơn — client sẽ hỏi xác nhận, đừng gọi lặp khi bị từ chối. Không tự ý tạo cảnh báo, nhập lệnh hay tạo đơn mua.

## Dữ liệu thị trường (chỉ đọc)

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
| `get_investor_flows` | Free | Khối ngoại / tự doanh cổ phiếu VN | `investor_type` foreign/proprietary, `symbol` (bỏ trống = toàn sàn), `exchange` HOSE/HNX/UPCOM/ALL, `period` day/month/quarter/year, `limit`, `basis` matched/total, `include_leaders` (top mua/bán ròng, chỉ chế độ toàn sàn) |
| `get_seasonality` | Free | Mùa vụ giá — % theo tháng nhiều năm | `symbol` (cổ phiếu hoặc chỉ số VN), `years` (bị cắt theo gói) — trả % từng tháng, cả năm, trung bình và tỷ lệ năm tăng của mỗi tháng |

## Cổ phiếu Việt Nam — lọc, so sánh, sự kiện (chỉ đọc)

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `screen_stocks` | Free (lọc LNST: Loyalty) | Lọc cổ phiếu theo tiêu chí | `exchange` HOSE/HNX/UPCOM/ALL, `group` all/vn30/vn100, `industry` (khớp một phần tên ngành), `pe_min/max`, `pb_min/max`, `roe_min/max`, `roa_min/max`, `rsi_min/max`, `min_vol20`, `above_ema200`; Loyalty: `rev_ttm_min`, `np_ttm_min`, `np_growth_min/max`, `exclude_np_spike`; `sort_by`, `order`, `limit` |
| `get_peers` | Free | Đặt một mã cạnh các mã cùng ngành | `symbol`, `limit` — P/E, P/B, ROE, tăng trưởng và trung vị ngành |
| `get_sector_overview` | Free | Ngành nào tăng mạnh, rẻ nhất | `exchange`, `sort_by` (mặc định `change_pct`), `order` |
| `get_corporate_events` | Free | Cổ tức, phát hành, ĐHCĐ, giao dịch nội bộ, niêm yết | `symbol` (bỏ trống = lịch toàn thị trường), `days_ahead` (mặc định 7), `limit` |
| `get_earnings_results` | Free | Mùa báo cáo: ai đã công bố, lãi tăng / giảm | `year`, `quarter` (bỏ trống = quý mới nhất), `exchange`, `sector` (tên ngành đúng bảng), `sort_by` (net_profit, np_growth, revenue_growth, disclosed_at), `order`, `limit` |
| `get_price_patterns` | **Loyalty** | Mô hình giá quét sau mỗi phiên | `symbol` (bỏ trống = toàn thị trường), `timeframe` D1/W1/MN1, `direction` bull/bear, `status` forming/breakout/complete, `kind` (double_bottom, head_shoulders, range, hammer…), `limit` |
| `get_top_shareholders` | Free | Người / tổ chức giàu nhất sàn | `owner_type` individual/corporate, `limit` |

## Crypto (chỉ đọc)

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `get_crypto_market` | Free | Toàn cảnh crypto: vốn hoá, tỷ trọng BTC/ETH, stablecoin, Sợ hãi & Tham lam, bảng xếp hạng | `offset`, `limit` (Free ≤ 50, Loyalty ≤ 200) |
| `get_crypto_coin` | Free | Hồ sơ một đồng: giá, hạng, vốn hoá, FDV, cung, đỉnh / đáy lịch sử, OI, link dự án | `code` (BTC, ETH, ARB…) |
| `get_crypto_coin_insights` | **Loyalty** | Dòng tiền theo cỡ lệnh, margin long/short, lịch mở khoá token, địa chỉ hợp đồng | `code`, `margin_hours` (mặc định 24) |
| `get_crypto_open_interest` | **Loyalty** | Chuỗi hợp đồng mở (USD và số đồng) | `code`, `timeframe` H1/H4/D1, `points` |

## Bài viết và mua hàng

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `read_article` | Free | Đọc toàn văn bài HODL.VN người dùng có quyền đọc (chưa có quyền → phần xem trước) | `slug` (từ `search_articles`), `offset` (đọc tiếp), `max_chars` |
| `list_membership_plans` | Free | Gói thành viên đang bán: giá, thời hạn | — |
| `create_membership_order` | Free · ghi | Tạo đơn chờ một gói, trả link thanh toán QR trên hodl.vn | `plan_slug` (từ `list_membership_plans`) |
| `buy_article` | Free · ghi | Tạo đơn mua lẻ một bài trả phí, trả link thanh toán QR | `slug` |
| `get_order_status` | Free | Đơn đã thanh toán chưa | `order_id` (do tool tạo đơn trả về) |

Tool tạo đơn chỉ tạo đơn **chờ** và trả link; người dùng tự thanh toán trên hodl.vn. Không bao giờ nói đơn đã thanh toán khi chưa kiểm `get_order_status`.

## Watchlist của người dùng

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `list_watchlists` | Free | Các watchlist: tên, id, số mã | — |
| `get_watchlist` | Free | Mã trong một watchlist kèm giá, %, RSI14 | `list_id` (bỏ trống = watchlist đầu), `limit`, `offset` |
| `add_watchlist_symbol` | Free · ghi | Thêm mã (chỉ khi được yêu cầu) | `symbol`, `list_id` (bỏ trống = watchlist đầu; chưa có thì tạo) |
| `remove_watchlist_symbol` | Free · ghi | Bỏ mã (client hỏi xác nhận) | `symbol`, `list_id` |

## Cảnh báo giá của người dùng

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `list_price_alerts` | Free | Cảnh báo đang có, số đang bật so với hạn mức | `status` active/paused/triggered/expired/all, `symbol`, `limit`, `cursor` |
| `get_price_alert_log` | Free | Các lần cảnh báo đã bắn, giá trị lúc bắn | `alert_id` (bỏ trống = mọi cảnh báo), `limit`, `before` |
| `create_price_alert` | Free · ghi | Tạo cảnh báo nhiều điều kiện: giá, khối lượng, RSI, MACD, EMA, SMA, Bollinger | `symbol`, `timeframe`, `conditions`, `frequency` (mặc định once_per_bar_close), `cooldown_seconds`, `expires_in_days`, `message` |
| `update_price_alert` | Free · ghi | Sửa điều kiện / khung / tần suất / hạn / lời nhắn (không đổi mã) | `alert_id`; `conditions` mới THAY THẾ toàn bộ; trường bỏ trống = giữ |
| `pause_price_alert` / `resume_price_alert` | Free · ghi | Tạm dừng / bật lại (bật lại cần còn chỗ trong hạn mức) | `alert_id` |
| `delete_price_alert` | Free · ghi | Xoá hẳn (lịch sử bắn vẫn giữ) | `alert_id` |

## Danh mục và tích sản

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `get_my_portfolio` | Beginner | Danh mục người dùng theo Ngắn hạn / Dài hạn / Tích sản: đang giữ, giá vốn, lãi tạm tính, lệnh chờ | `horizon` (bỏ trống = cả ba) |
| `list_my_symbol_deals` | Beginner | Mọi lệnh khớp / chờ ở một mã, kèm `deal_id` để sửa | `symbol` |
| `add_portfolio_deals` | Beginner · ghi | Nhập 1–50 lệnh (mua, bán, cổ tức, lệnh chờ), trọn gói | `deals` |
| `update_portfolio_deal` | Beginner · ghi | Sửa giá, KL, ngày, kỳ hạn, cắt lỗ / chốt lời, trạng thái (`filled` khi lệnh chờ đã khớp, `cancelled` khi huỷ) | `deal_id` + trường cần đổi (giá bằng đồng) |
| `delete_portfolio_deal` | Beginner · ghi | Xoá hẳn một lệnh | `deal_id` |
| `get_system_portfolio` | **Loyalty** | Danh mục HODL.VN đang nắm: rổ, từng lô kèm cắt lỗ / chốt lời, lệnh chờ mua | `horizon` long / T+ |
| `get_system_portfolio_performance` | **Loyalty** | Hiệu suất danh mục HODL.VN theo tháng / quý / năm | `horizon`, `group` month/quarter/year, `date_from`, `date_to` (mặc định 12 tháng) |
| `simulate_accumulation` | Free (1 mã; Beginner+ ≤ 10 mã) | Mô phỏng mua định kỳ trên giá quá khứ: vốn, giá trị, lãi, lợi suất năm | `legs` (mã + số cổ phiếu mỗi kỳ), `cadence`, `start_date`, `fee_percent` (mặc định 0,15), `months` |
| `list_accumulation_plans` | Beginner | Kế hoạch tích sản đã lưu | — |
| `create_accumulation_plan` | Beginner · ghi | Lưu kế hoạch để app nhắc mỗi kỳ | `name`, `cadence`, `start_date`, `legs`, `months` |
| `update_accumulation_plan` | Beginner · ghi | Sửa / tạm dừng (`active: false`) kế hoạch; `legs` mới THAY THẾ toàn bộ | `plan_id` + trường cần đổi |
| `delete_accumulation_plan` | Beginner · ghi | Xoá kế hoạch (lệnh đã ghi giữ nguyên) | `plan_id` |

## HODL Lab (script Python chạy trong trình duyệt)

| Tool | Gói | Dùng khi | Tham số chính |
|---|---|---|---|
| `write_lab_script` | Free | Lấy luật viết, hàm có sẵn và ví dụ gần nhất trước khi viết chỉ báo / chiến lược / danh mục | `kind`, `description` (ý tưởng) |
| `save_lab_script` | Beginner · ghi | Lưu script vừa viết vào thư viện HODL Lab riêng của người dùng, trả link mở và bấm Chạy | `kind`, `name`, `code` (theo luật của `write_lab_script`) |

Luôn gọi `write_lab_script` trước rồi mới viết code; không tự bịa hàm của HODL Lab.

## Hạn mức theo gói

| Hạng mục | Free | Loyalty |
|---|---|---|
| Lượt gọi | 10/phút, 100/ngày | 60/phút, 2.500/ngày |
| Nến lịch sử | D1 30, W1 12, H4 200 | 1.000 mọi khung |
| BCTC | 4 quý / 3 năm, chỉ tiêu chính | 8 quý / 5 năm, bảng đầy đủ |
| Kỳ vĩ mô | 12 | 240 |
| Kỳ ETF | 30 | 365 |
| Kỳ khối ngoại / tự doanh | 30 | 250 |
| Số năm mùa vụ giá | 5 | 20 |
| Ảnh chụp kỹ thuật | — | Có |

Bảng cập nhật mới nhất: https://hodl.vn/ai. Claude kết nối bằng connector chính chủ (đăng nhập HODL.VN, không key); client không hỗ trợ OAuth dùng 1 API key mỗi tài khoản (Free lẫn Loyalty).

## Mẹo

- Gộp câu hỏi: một `get_quote` đã có P/E, P/B, ROE — không cần gọi `get_financials` chỉ để lấy các số này.
- Gói Free muốn RSI/EMA: lấy `get_price_history` (D1, 30 nến) rồi tự tính, nói rõ số nến dùng.
- Vĩ mô so sánh nhiều nước: `get_macro_indicators` với `country: G7` + `query`, rồi gọi `get_macro_series` cho từng slug.
- Đơn vị BCTC là tỷ đồng; ETF là triệu USD; vĩ mô xem `unit` của từng chỉ số.
