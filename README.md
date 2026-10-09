# HODL.VN Market Insight

Dữ liệu thị trường HODL.VN ngay trong trợ lý AI: cổ phiếu Việt Nam (HOSE/HNX/UPCoM), VN-Index, vĩ mô Việt Nam và thế giới, khối ngoại và tự doanh, dòng tiền ETF Bitcoin/Ethereum/Solana/vàng, forex, crypto, hàng hoá và bài phân tích HODL.VN — mọi câu trả lời dẫn nguồn.

Repo gồm:

- **MCP server** `hodl` — `https://mcp.hodl.vn/mcp` (12 tool chỉ đọc).
- **Skill** `hodl-market-research` — dạy AI gọi tool đúng thứ tự, đọc đúng đơn vị, luôn dẫn nguồn.
- **Plugin Claude Code** `hodl` — gói sẵn cả hai.

Trang giới thiệu, danh sách tool và bảng hạn mức: **https://hodl.vn/ai**

## 1. Đăng nhập (OAuth) — không cần key

Claude.ai, ChatGPT, Claude Code kết nối bằng **đăng nhập HODL.VN**: trỏ tới `https://mcp.hodl.vn/mcp`, trình duyệt mở hodl.vn → đăng nhập bằng mã email → bấm Đồng ý. Gỡ kết nối bất cứ lúc nào tại **Tài khoản → Kết nối AI**: https://hodl.vn/tai-khoan/ket-noi-ai.

Client chưa hỗ trợ OAuth (Cursor, VS Code bản cũ, Gemini và AI web khác) dùng **API key** hoặc **URL kết nối riêng** có sẵn ở cùng trang. Mỗi tài khoản có 1 key (Free hoặc Loyalty).

## 2. Cài đặt

### Claude Code — plugin (MCP + skill)

```bash
claude plugin marketplace add tohaitrieu/hodl-market-insight
claude plugin install hodl@hodl-market-insight
```

Lần đầu dùng, gõ `/mcp` → chọn `hodl` → **Authenticate** → đăng nhập HODL.VN trên trình duyệt.

Chỉ cần MCP, không cần skill:

```bash
claude mcp add --transport http hodl https://mcp.hodl.vn/mcp
```

### Claude.ai / Claude Desktop

1. Settings → Connectors → Add custom connector
2. Name: `HODL.VN`
3. Remote MCP server URL: `https://mcp.hodl.vn/mcp` → **Connect** → đăng nhập HODL.VN → Đồng ý.

Thêm skill: tải [bản zip của thư mục skill](plugins/hodl/skills/hodl-market-research) (nén cả thư mục `hodl-market-research`) → Settings → Capabilities → Skills → Upload skill.

### ChatGPT (web)

1. Settings → Apps → Advanced settings → bật **Developer mode**
2. Create app → Name: `HODL.VN`
3. MCP Server URL: `https://mcp.hodl.vn/mcp`
4. Authentication: **OAuth** → đăng nhập HODL.VN → Đồng ý.

### Gemini và AI web khác (không hỗ trợ OAuth)

Dùng **URL kết nối riêng** (dạng `https://mcp.hodl.vn/mcp/k/…`), sao chép tại Tài khoản → Kết nối AI.

### Cursor — `~/.cursor/mcp.json` (API key)

```json
{
  "mcpServers": {
    "hodl": {
      "url": "https://mcp.hodl.vn/mcp",
      "headers": { "Authorization": "Bearer hodl_..." }
    }
  }
}
```

### VS Code — `.vscode/mcp.json` (API key)

```json
{
  "servers": {
    "hodl": {
      "type": "http",
      "url": "https://mcp.hodl.vn/mcp",
      "headers": { "Authorization": "Bearer hodl_..." }
    }
  }
}
```

> URL kết nối riêng chứa key — đừng chia sẻ. Lộ key thì xoay key mới tại Tài khoản → Kết nối AI.

## 3. Hỏi thử

- "Giá FPT hôm nay và P/E so với ngành?"
- "Lạm phát Việt Nam và Mỹ 12 tháng gần đây?"
- "Dòng tiền ETF Bitcoin tuần này?"
- "EURUSD và vàng đang thế nào?"

## Free và Loyalty

| | Free | Loyalty |
|---|---|---|
| Lượt gọi | 100/ngày | 2.500/ngày |
| Nến lịch sử | D1 30, W1 12, H4 200 | 1.000 mọi khung |
| BCTC | 4 quý / 3 năm | 8 quý / 5 năm, bảng đầy đủ |
| Ảnh chụp kỹ thuật | — | Có |

Bảng đầy đủ, luôn cập nhật: https://hodl.vn/ai

---

## English

HODL.VN market data inside your AI assistant: Vietnamese stocks, VN-Index, Vietnamese and world macro, Bitcoin/Ethereum/Solana/gold ETF flows, forex, crypto, commodities and HODL.VN analysis — every answer cites its source.

1. Endpoint `https://mcp.hodl.vn/mcp` supports **OAuth 2.1** (issuer `https://hodl.vn`): Claude.ai, ChatGPT and Claude Code just connect and sign in with a HODL.VN account — no key needed.
2. Claude Code: `claude plugin marketplace add tohaitrieu/hodl-market-insight` then `claude plugin install hodl@hodl-market-insight`, then `/mcp` → hodl → Authenticate.
3. Clients without OAuth (Cursor, VS Code, Gemini…): use a free API key (`Authorization: Bearer <key>`) or your personal connection URL from https://hodl.vn/tai-khoan/ket-noi-ai.

Data is for reference only, not investment advice.

Privacy policy: https://hodl.vn/chinh-sach-rieng-tu

## License

MIT applies to the files in this repository only (plugin, skill, docs). It does **not** grant any rights to HODL.VN data returned by the MCP server, which is governed by HODL.VN's terms.
