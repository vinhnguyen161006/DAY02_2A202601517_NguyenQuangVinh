# Research Notes — RegWatch

**Access date:** 2026-07-27
**Selected problem:** RegWatch — Hệ thống giám sát thay đổi pháp lý và hỗ trợ Compliance trong lĩnh vực Ngân hàng - Tài chính.

## 1. Research questions

1. Nguồn pháp lý công khai nào có thể dùng cho pilot RegWatch?
2. Existing legal search/regulatory intelligence tools giải quyết được bước nào?
3. Gap còn lại của RegWatch là gì: search, monitoring, impact mapping, conflict detection hay HITL workflow?
4. Khi nào Rule đủ, khi nào cần Workflow, khi nào bounded Agent có giá trị?
5. Human boundary trong legal/compliance workflow phải đặt ở đâu?

---

## 2. Source log

| # | Title / source | Organization | URL | Summary | Claim used | Reliability |
|---:|---|---|---|---|---|---|
| 1 | Cổng thông tin Ngân hàng Nhà nước Việt Nam | SBV / NHNN | https://sbv.gov.vn/ | Trang chính thức của NHNN, có mục văn bản quy phạm pháp luật, dự thảo VBQPPL và thông tin ngành ngân hàng. | Có nguồn public để monitor văn bản ngân hàng và regulatory updates. | Official government source. |
| 2 | Cơ sở dữ liệu quốc gia về pháp luật | Bộ Tư pháp / VBPL | https://vbpl.vn/ | CSDL quốc gia phục vụ tra cứu văn bản pháp luật Việt Nam, gồm văn bản trung ương/địa phương. | Có legal corpus public để retrieval và metadata extraction. | Official legal database. |
| 3 | Giới thiệu CSDL quốc gia về pháp luật | VBPL | https://vbpl.vn/gioi-thieu | Mô tả phạm vi CSDL văn bản pháp luật. | Search database là input mạnh, nhưng chưa phải internal compliance workflow. | Official source. |
| 4 | Thư Viện Pháp Luật | Thư Viện Pháp Luật | https://thuvienphapluat.vn/ | Nền tảng tra cứu/cập nhật văn bản pháp luật phổ biến tại Việt Nam. | Existing legal search/content platform tồn tại; RegWatch không nên claim "chưa có search tool". | Commercial legal information source. |
| 5 | Thomson Reuters Regulatory Intelligence | Thomson Reuters | https://regintel-content.thomsonreuters.com/ | Regulatory Intelligence hỗ trợ monitoring global regulatory developments, customized profiles và API integration. | Regulatory intelligence/horizon scanning là pattern đã tồn tại ở thị trường quốc tế. | Official product source. |
| 6 | LexisNexis Regulatory Compliance | LexisNexis | https://www.lexisnexis.com/en-us/products/regulatory-compliance.page | Cung cấp obligations register, alerts và guidance cho GRC/compliance teams. | Obligation register + alerting là pattern quan trọng cho RegWatch. | Official product source. |
| 7 | CUBE regulatory intelligence | CUBE | https://cube.global/ | CUBE cung cấp automated regulatory intelligence/change management cho highly regulated industries. | Existing RegTech products kết hợp regulatory change monitoring và AI-assisted compliance workflows. | Official product source. |
| 8 | CUBE solutions | CUBE | https://cube.global/solutions | Mô tả track regulatory changes, integration với risk/policy/control frameworks. | Gap của RegWatch là local adaptation + Vietnamese banking/internal process mapping. | Official product source. |
| 9 | Regology Regulatory Change Agent | Regology | https://www.regology.com/regulatory-change-agent | Mô tả monitor incoming changes, customized alerts, map to risks/controls. | Agentic/regulatory change pattern có thật; nhóm cần bounded agent + HITL. | Official product source. |
| 10 | AscentAI Change Management | AscentAI | https://www.ascentregtech.com/our-difference/change-management/ | Mô tả obligations-based change management và hạn chế của horizon scanning top-down. | Search/monitoring chưa đủ; cần obligation/impact context. | Official product source. |

---

## 3. Verification notes

| Claim from discussion/slide | Verification | Final wording |
|---|---|---|
| "Có rất nhiều văn bản pháp lý ngân hàng thay đổi liên tục." | SBV public portal có mục văn bản quy phạm pháp luật và hiển thị các Thông tư/dự thảo gần đây. | Dùng wording định tính: văn bản ngân hàng được công bố/cập nhật thường xuyên trên nguồn public. |
| "Việt Nam chưa có solution nào." | Không thể chứng minh tuyệt đối qua desk research. | Không dùng. Viết: trong phạm vi desk research, nhóm chưa tìm thấy bằng chứng công khai về workflow end-to-end đúng scope RegWatch. |
| "Có thể tự động phát hiện mọi conflict." | Không có evidence. | Chỉ là design hypothesis; cần annotated pilot và human review. |
| "RegWatch giảm từ weeks xuống minutes." | Không có observed data của nhóm. | Chỉ có thể dùng như product vision, không dùng làm fact/metric. |
| "Qdrant/Neo4j/LangGraph là bắt buộc." | Đây là lựa chọn implementation, không phải yêu cầu bài toán. | Viết là implementation hypothesis: vector DB, knowledge graph, bounded orchestrator. |

---

## 4. Existing solution comparison

| Tool / pattern | Giải quyết bước nào | Điểm mạnh | Gap / risk | Bài học cho RegWatch |
|---|---|---|---|---|
| SBV / NHNN portal | Source monitoring cho văn bản ngành ngân hàng | Official source, gần domain ngân hàng | Không tự map impact vào policy/process nội bộ | Nên dùng làm source input thay vì tự bịa corpus. |
| VBPL | Search legal corpus, metadata, văn bản trung ương/địa phương | Nguồn pháp lý công khai, đáng tin | Không phải dashboard compliance nội bộ | Retrieval phải đi kèm traceability và version metadata. |
| Thư Viện Pháp Luật | Legal search, cập nhật văn bản, nội dung dễ đọc | Dễ dùng cho người tra cứu luật | Không chứng minh end-to-end regulatory change management nội bộ | RegWatch phải khác search database ở impact/action workflow. |
| Thomson Reuters Regulatory Intelligence | Horizon scanning, regulatory developments, profiles, API integration | Pattern regulatory intelligence mature | Commercial/global, không chứng minh local Vietnamese banking workflow | Monitoring + profile/filter là pattern cần học. |
| LexisNexis Regulatory Compliance | Obligations register, alerts, practical guidance | Tập trung vào obligation và action | Phạm vi jurisdiction/product khác | RegWatch nên map regulation → obligation → owner/action. |
| CUBE | Automated regulatory intelligence/change management | Có pattern AI + risk/policy/control framework | Claim product không thay validation của nhóm | RegWatch pilot nên đo recall/precision và reviewer effort. |
| Regology | Regulatory Change Agent, alerts, mapping to risks/controls | Gợi ý agentic workflow bounded theo task compliance | Không dùng claim của product như benchmark | Agentic orchestration có giá trị khi cần follow sources/tool calls. |
| AscentAI | Obligations-based change management | Nhấn mạnh hạn chế của horizon scanning document-level | Không phải source Việt Nam | RegWatch nên tránh chỉ keyword/top-down search. |

**Existing solution gap wording:**
Trong phạm vi desk research của nhóm, các nguồn pháp luật phổ biến tại Việt Nam chủ yếu mạnh về công bố/tra cứu văn bản. Nhóm chưa tìm thấy bằng chứng rõ ràng về một workflow end-to-end công khai kết hợp regulatory monitoring, impact mapping, conflict detection, departmental routing và HITL theo đúng scope RegWatch cho ngân hàng Việt Nam.

---

## 5. Design decisions

### Why Vector Search?

Vector search phù hợp cho semantic retrieval: một văn bản mới có thể không nhắc đúng keyword của policy nội bộ nhưng vẫn liên quan về nghĩa vụ, quy trình hoặc risk. Tuy nhiên vector search không đủ để chứng minh legal relationship.

### Why Graph?

Knowledge graph phù hợp cho explicit legal relationships:

- `references`
- `amends`
- `repeals`
- `supersedes`
- `related-to`

Graph giúp trace source và follow dẫn chiếu qua nhiều tầng. Nhưng graph không tự giải quyết semantic similarity.

### Why Hybrid?

Vector không đủ trace relationships. Graph không đủ semantic similarity. Keyword/BM25 vẫn cần cho số hiệu văn bản, điều/khoản, ngày hiệu lực và exact references. Vì vậy RegWatch nên dùng hybrid retrieval.

### Why HITL?

Legal/compliance là high-risk. Human-in-the-loop cần ở ba mức:

1. Compliance expert duyệt impact/conflict/risk.
2. CEO/BoD/C-level duyệt risk response/action plan.
3. Product/IT/Risk/Operations duyệt implementation update.

### Why agentic orchestration?

Một fixed workflow đủ cho happy path. Nhưng khi văn bản dẫn chiếu nhiều tầng hoặc reviewer yêu cầu phân tích sâu hơn, hệ thống cần branch:

- chọn retrieval path;
- gọi semantic search;
- truy vấn graph;
- rerun impact assessment;
- hỏi thêm expert input khi confidence thấp.

Đây là bounded agentic orchestration, không phải fully autonomous agent.

### Why not train new foundation model?

Không cần. Pilot có thể bắt đầu với existing LLM/embedding + domain corpus + retrieval + human review. Train model mới tốn dữ liệu, kiểm định và governance hơn mức cần thiết cho Day 02.

---

## 6. Metrics notes

| Metric | Type | Vì sao dùng |
|---|---|---|
| Relevant provision recall ≥90% | Pilot target | False negative là risk nguy hiểm nhất. |
| Alert relevance ≥80% | Pilot target | Nếu false positive quá nhiều, reviewer overload. |
| 100% material claim có source | Boundary metric | Legal output phải audit được. |
| Giảm ≥50% initial review effort | Productivity target | Đo được bằng reviewer time log. |
| 0 critical miss trong controlled test set | Safety target | Không dùng AI nếu miss material obligation. |

## 7. Claims not used

- Không dùng số lượng văn bản, tiền phạt hoặc market statistics chưa verify.
- Không claim "AI không bao giờ bỏ sót".
- Không claim "Việt Nam chưa có bất cứ solution nào".
- Không claim RegWatch đạt target trước pilot.
- Không claim commercial tools có feature cụ thể nếu source không nói rõ.

## 8. Research conclusion

RegWatch nên được framing là **bounded agentic workflow with HITL**, không phải chatbot luật và không phải fully autonomous agent. Existing sources/tools cho thấy regulatory intelligence và legal search đã có nhiều pattern tốt. Phần cần pilot của nhóm là local workflow:

```text
SBV/VBPL source monitoring
→ parse + metadata
→ hybrid retrieval
→ graph relationship
→ impact/conflict analysis
→ risk prioritization
→ compliance review
→ action plan
→ archive feedback
```

Kết luận quan trọng nhất: AI không phải người phê duyệt compliance. AI chỉ hỗ trợ tìm, so sánh, xếp rủi ro và draft có citation; người thật giữ quyền quyết định.
