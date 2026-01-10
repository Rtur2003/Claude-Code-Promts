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

### 2. Entegrasyon Gardiyanı Prompt'u 🛡️
**Dosya**: [entegrasyon-gardiyani-agent-prompt-tr.md](agents/entegrasyon-gardiyani-agent-prompt-tr.md)

**Amaç**: Sistem bütünlüğünü bozmadan çalışmak için tam kapsamlı kontrol listesi. Çeviri, tema, API sözleşmesi, güvenlik ve performans risklerini entegre biçimde yönetir.

**Ne Zaman Kullanılır**:
- Yeni özellik eklerken mevcut sistemle uyumdan emin olmak gerektiğinde
- Çeviri/tema/konfigürasyon/şema değişikliklerinin yan etkilerini kontrol etmek için
- Token tasarrufu ile kısa ama kanıtlı yanıtlar istenirken

**Temel Özellikler**:
- Haritalandırma → Çakışma Tarama → Risk Analizi → Plan → Uygula → Doğrula
- i18n, tema/design token, veri modeli, API sözleşmesi, güvenlik ve performans kontrol listeleri
- Gerçek sorun kanıtı olmadan farazi öneri yapılmaz; çıktılar kısa tutulur

---

### 3. Claude Temel Sistem Prompt'u
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

### 4. Kod İnceleme Prompt'u 🔍
**Dosya**: [code-review-prompt-tr.md](agents/code-review-prompt-tr.md)

**Amaç**: Sistematik kod inceleme ile kalite güvencesi sağla.

**Ne Zaman Kullanılır**:
- Pull request incelerken
- Kod kalitesini değerlendirirken
- Takım arkadaşlarına geri bildirim verirken

**Temel Özellikler**:
- ANLA protokolü (Anla, Not Al, Listele, Aktar)
- Güvenlik, performans ve bakım kontrol listeleri
- Geri bildirim şablonları
- Yaygın kod pattern'leri

---

### 5. Hata Analizi Prompt'u 🐛
**Dosya**: [error-analysis-prompt-tr.md](agents/error-analysis-prompt-tr.md)

**Amaç**: Sistematik hata tespiti, kök neden analizi ve güvenilir düzeltmeler.

**Ne Zaman Kullanılır**:
- Hata ayıklama yaparken
- Üretim sorunlarını çözerken
- Test hatalarını analiz ederken

**Temel Özellikler**:
- BULAR protokolü (Bul, Understand, Listele, Aksiyon, Raporla)
- 5 Neden tekniği
- Hata sınıflandırması (P0-P3)
- Düzeltme doğrulama

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

**Kod inceleme için**:
```
[Temel prompt] + [Kod İnceleme Prompt'u]
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

- [x] ~~Hata Analizi Prompt'u~~ ✅
- [ ] Proje İş Akışı Prompt'u
- [x] ~~Kod İnceleme Prompt'u~~ ✅
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
