# Türkçe Prompt İndeksi

> Claude Code, GitHub Copilot ve benzeri AI kodlama ajanları için Türkçe prompt'lar.

## Mevcut Prompt'lar

| # | Prompt | Amaç | Dosya |
|---|--------|------|-------|
| 1 | **Agent Sistem** ⭐ | Temel APEI işletim sistemi | [View](agents/claude-agent-system-prompt-tr.md) |
| 2 | **Temel Prompt** | Evrensel en iyi uygulamalar | [View](base/claude-foundation-prompt-tr.md) |
| 3 | **Kod İnceleme** | Sistematik PR inceleme | [View](agents/code-review-prompt-tr.md) |
| 4 | **Hata Analizi** | Kök neden analizi & düzeltme | [View](agents/error-analysis-prompt-tr.md) |

---

## Kullanım

### Seçenek 1: Tam Agent Kurulumu
Agent Sistem Prompt'unu temel olarak kullan:

```
[claude-agent-system-prompt-tr.md içeriğini yapay zekaya ver]
→ Görevini tanımla → APEI döngüsü otomatik çalışır
```

### Seçenek 2: Görev-Spesifik
Agent Sistem + uzman prompt kombinasyonu:

| Görev | Kombine Et |
|-------|-----------|
| Hata ayıklama | Agent Sistem + Hata Analizi |
| Kod inceleme | Agent Sistem + Kod İnceleme |

---

## Çeviri Durumu

| Prompt | Durum |
|--------|-------|
| Agent Sistem | ✅ Tamamlandı |
| Temel Prompt | ✅ Tamamlandı |
| Kod İnceleme | ✅ Tamamlandı |
| Hata Analizi | ✅ Tamamlandı |
| Proje İş Akışı | ⏳ Planlandı |
| Güvenlik Denetimi | ⏳ Planlandı |
| Refactoring | ⏳ Planlandı |
| Test Stratejileri | ⏳ Planlandı |
| Dokümantasyon | ⏳ Planlandı |
| Performans | ⏳ Planlandı |

---

## Kaynaklar

| Kaynak | Açıklama |
|--------|----------|
| [İngilizce İndeks](../english/INDEX.md) | Tüm İngilizce prompt'lar |
| [Agent İndeksi](../english/agents/INDEX.md) | Agent prompt kataloğu |
| [README](../../README.md) | Proje genel bakışı |
| [CONTRIBUTING](../../CONTRIBUTING.md) | Katkıda bulunma rehberi |
