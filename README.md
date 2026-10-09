# HODL.VN Market Insight

Dữ liệu thị trường HODL.VN ngay trong trợ lý AI: cổ phiếu Việt Nam (HOSE/HNX/UPCoM), VN-Index, vĩ mô Việt Nam và thế giới, dòng tiền ETF Bitcoin/Ethereum/Solana/vàng, forex, crypto, hàng hoá và bài phân tích HODL.VN — mọi câu trả lời dẫn nguồn.

Repo gồm:

- **MCP server** `hodl` — `https://mcp.hodl.vn/mcp` (10 tool chỉ đọc).
- **Skill** `hodl-market-research` — dạy AI gọi tool đúng thứ tự, đọc đúng đơn vị, luôn dẫn nguồn.
- **Plugin Claude Code** `hodl` — gói sẵn cả hai.

Trang giới thiệu, danh sách tool và bảng hạn mức: **https://hodl.vn/ai**

## 1. Lấy API key (miễn phí)

Đăng nhập HODL.VN → **Tài khoản → Kết nối AI**: https://hodl.vn/tai-khoan/ket-noi-ai. Mỗi tài khoản có 1 key (Free hoặc Loyalty); sao chép lại bao nhiêu lần cũng được.

## 2. Cài đặt

### Claude Code — plugin (MCP + skill)

```bash
claude plugin marketplace add tohaitrieu/hodl-market-insight
claude plugin install hodl@hodl-market-insight
```

Lúc cài, Claude Code hỏi **HODL.VN API key** và cất vào kho bảo mật của máy (không ghi ra file cấu hình).

Chỉ cần MCP, không cần skill:

```bash
claude mcp add --transport http hodl https://mcp.hodl.vn/mcp --header "Authorization: Bearer hodl_..."
```

### Claude.ai / Claude Desktop

1. Settings → Connectors → Add custom connector
2. Name: `HODL.VN`
3. Remote MCP server URL: **URL kết nối riêng** của bạn (dạng `https://mcp.hodl.vn/mcp/k/…`), sao chép tại Tài khoản → Kết nối AI.

Thêm skill: tải [bản zip của thư mục skill](plugins/hodl/skills/hodl-market-research) (nén cả thư mục `hodl-market-research`) → Settings → Capabilities → Skills → Upload skill.

### ChatGPT (web)

1. Settings → Apps → Advanced settings → bật **Developer mode**
2. Create app → Name: `HODL.VN`
3. MCP Server URL: URL kết nối riêng (như trên)
4. Authentication: No authentication

### Cursor — `~/.cursor/mcp.json`

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

### VS Code — `.vscode/mcp.json`

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

1. Get a free API key at https://hodl.vn/tai-khoan/ket-noi-ai (sign-in required).
2. Claude Code: `claude plugin marketplace add tohaitrieu/hodl-market-insight` then `claude plugin install hodl@hodl-market-insight` — you'll be asked for the API key, stored in secure storage.
3. Other clients (Claude.ai, ChatGPT, Cursor, VS Code): see the snippets above; the endpoint is `https://mcp.hodl.vn/mcp` with `Authorization: Bearer <key>`, or your personal connection URL for Claude.ai / ChatGPT.

Data is for reference only, not investment advice.

Privacy policy: https://hodl.vn/chinh-sach-rieng-tu

## License

MIT applies to the files in this repository only (plugin, skill, docs). It does **not** grant any rights to HODL.VN data returned by the MCP server, which is governed by HODL.VN's terms.
