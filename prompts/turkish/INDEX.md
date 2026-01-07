# Türkçe Prompt İndeksi

> **Yapay Zeka Kodlama Asistanları İçin Optimize Edilmiş Türkçe Prompt'lar**

## Genel Bakış

Bu prompt'lar özellikle Claude Code, GitHub Copilot ve benzeri yapay zeka kodlama asistanları için tasarlanmıştır.

- ✅ **Token-Optimize**: Minimum token ile maksimum etkinlik
- ✅ **Agent-Hazır**: Otonom çalışma için yapılandırılmış
- ✅ **Aksiyon-Odaklı**: Net komutlar ve iş akışları
- ✅ **Evrensel**: Her kod tabanı veya dil ile çalışır

---

## Mevcut Prompt'lar

### 1. Claude Agent Sistem Prompt'u ⭐ (Buradan Başla)
**Dosya**: [claude-agent-system-prompt-tr.md](agents/claude-agent-system-prompt-tr.md)

**Amaç**: Yapay zeka kodlama ajanları için temel işletim sistemi. APEI döngüsünü (Analiz → Plan → Uygula → İterasyon) ve tüm temel davranışları içerir.

**Ne Zaman Kullanılır**:
- Herhangi bir kodlama görevi başlatırken
- Tam bir agent sistem prompt'u gerektiğinde
- Sistematik, iteratif geliştirme istendiğinde

**Temel Özellikler**:
- APEI geliştirme döngüsü
- Commit standartları
- Kod kalite kontrol listesi
- İletişim şablonları

---

### 2. Claude Temel Sistem Prompt'u
**Dosya**: [claude-foundation-prompt-tr.md](base/claude-foundation-prompt-tr.md)

**Amaç**: Her proje için evrensel en iyi uygulamalar ve temel prensipler.

**Ne Zaman Kullanılır**:
- Herhangi yeni bir projeye başlarken
- Evrensel en iyi uygulamalar gerektiğinde
- Birden fazla alanda çalışırken

**Temel Özellikler**:
- Analiz → Plan → Uygula → İterasyon döngüsü
- Commit mesaj standartları
- Hata analiz metodolojisi
- Kod kalite prensipleri
- Test stratejileri

---

## Nasıl Kullanılır

### Seçenek 1: Tam Agent Kurulumu
**Claude Agent Sistem Prompt'unu** temel olarak kullan. Otonom çalışma için gereken her şeyi içerir.

```
[claude-agent-system-prompt-tr.md içeriğini yapay zekaya ver]

Şimdi, bu kod tabanını analiz et ve iyileştirmeler öner...
```

### Seçenek 2: Görev-Spesifik
Spesifik görevler için özelleştirilmiş prompt'lar ekle:

**Hata ayıklama için**:
```
[Temel prompt] + [Hata Analizi Prompt'u]
```

**Proje geliştirme için**:
```
[Temel prompt] + [Proje İş Akışı Prompt'u]
```

---

## En İyi Uygulamalar

### YAP ✅
- Agent Sistem Prompt'u ile başla
- Ajanın APEI döngüsünü tamamlamasına izin ver
- İteratif sürece güven
- Basit görevler için Hızlı Referans kullan

### YAPMA ❌
- Döngü ortasında gereksiz yere kesme
- Analiz fazını atlama
- Test hatalarını görmezden gelme
- Doğrulama olmadan "bitti"ye acele etme

---

## Yakında Eklenecekler

Aşağıdaki prompt'ların Türkçe çevirileri yakında eklenecektir:

- [ ] Hata Analizi Prompt'u
- [ ] Proje İş Akışı Prompt'u
- [ ] Kod İnceleme Prompt'u
- [ ] Güvenlik Denetimi Prompt'u
- [ ] Refactoring Prompt'u
- [ ] Test Stratejileri Prompt'u
- [ ] Dokümantasyon Prompt'u
- [ ] Performans Optimizasyonu Prompt'u

---

## Katkıda Bulunma

Türkçe prompt'ları iyileştirmek veya yeni prompt'lar eklemek isterseniz:

1. İngilizce versiyonu inceleyin
2. Teknik doğruluğu koruyarak çevirin
3. Türkçe programlama terminolojisini kullanın
4. Pull request gönderin

---

## Daha Fazla Kaynak

- [İngilizce Prompt İndeksi](../english/INDEX.md) - Tüm prompt'ların tam listesi
- [Ana README](../../README.md) - Proje genel bakışı
- [CONTRIBUTING.md](../../CONTRIBUTING.md) - Katkıda bulunma rehberi

---

> **Unutma**: Bu prompt'lar Claude'un daha iyi yazılım geliştirmenize yardımcı olmasını sağlar. Sistematik iterasyon ve kalite odağı ile.
