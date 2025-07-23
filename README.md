# Speech Denoising Model

Проект для шумоподавления в звуке с помощью различных архитектур нейронных сетей. Сравнение результатов для Si-SDR и Si-SDR+PESQ функций потерь.

## Структура проекта

- `notebooks/` - Jupyter-ноутбуки с исследованиями и пайплайнами
- `models/` - Предобученные модели
- `examples/` - Примеры результатов шумоподавления

## Основные ноутбуки

| Ноутбук | Описание |
|---------|----------|
| `denoising_si-sdr.ipynb` | Обучение и тестирование модели на основе Si-SDR loss |
| `denoising_si_sdr_pesq_07.ipynb` | Обучение и тестирование модели на основе Si-SDR+PESQ loss с α=0.7 |
| `si-sdr_pesq_model_tuned.ipynb` | Обучение и тестирование fine-tuned модели на основе Si-SDR+PESQ loss |
| `dccrn-model.ipynb` | Обучение DCCRN модели на Si-SDR loss |
| `dccrn-model-tuned.ipynb` | Дообучение DCCRN модели на Si-SDR+PESQ loss |

## Предобученные модели

- `si-sdr_model.pt` - WaveNet модель с Si-SDR loss
- `model_si-sdr_pesq_07.pt` - WaveNet модель с Si-SDR+PESQ loss (α=0.7)
- `si-sdr_pesq_model_tuned.pt` - Fine-tuned WaveNet модель
- `dccrn_model.pt` - DCCRN модель

## Dataset

В качестве датасета использован **Libri Speech Noise Dataset**.

Для обучающего датасета из каждого сэмпла выбирается случайные cnt_seconds секунд, на которых обучается модель.

## Результаты моделей

### Сводная таблица метрик

| Модель | Архитектура | Loss Function | Test Loss | Test SI-SDR | Test PESQ | Особенности |
|--------|-------------|---------------|-----------|-------------|-----------|-------------|
| Si-SDR | WaveNet (12 layers) | Si-SDR | -8.53 | 8.53 | 1.34 | Много артефактов |
| Si-SDR+PESQ | WaveNet (12 layers) | Si-SDR + 0.7×PESQ | -7.41 | 8.48 | 1.48 | Меньше артефактов |
| Fine-tuned Si-SDR+PESQ | WaveNet (10 layers, F_c=32) | Si-SDR + 0.7×PESQ | -8.50 | 9.49 | 1.59 | Улучшение качества |
| DCCRN | Complex U-Net + GRU | Si-SDR + 0.7×PESQ | -10.04 | 10.77 | 1.73 | STFT представление |

### Таблица аудио примеров

| Образец | Noisy | Si-SDR (12 layers) | Si-SDR+PESQ (12 layers) | Fine-tuned Si-SDR+PESQ (10 layers) | DCCRN |
|---------|-------|-------------------|-------------------------|-------------------------------------|-------|
| **1** | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/noisy/1-noise.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr/1-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq/1-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq_tuned/1-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/dccrn/1-clear.wav) |
| **2** | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/noisy/2-noise.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr/2-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq/2-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq_tuned/2-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/dccrn/2-clear.wav) |
| **3** | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/noisy/3-noise.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr/3-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq/3-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq_tuned/3-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/dccrn/3-clear.wav) |
| **4** | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/noisy/4-noise.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr/4-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq/4-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq_tuned/4-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/dccrn/4-clear.wav) |
| **5** | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/noisy/5-noise.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr/5-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq/5-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/si_sdr_pesq_tuned/5-clear.wav) | [🔊](https://gabalpha.github.io/read-audio/?p=https://raw.githubusercontent.com/mcaramba563/denosising_model/refs/heads/main/examples/dccrn/5-clear.wav) |

## Подробное описание моделей

### Si-SDR Model
**Архитектура:** WaveNet с 12 down- и up-sampling слоями  
**Loss Function:** Si-SDR  
**Метрики:** Test SI-SDR: 8.53, Test PESQ: 1.34  
**Особенности:** После шумоподавления присутствует много артефактов

### Si-SDR+PESQ Model
**Архитектура:** WaveNet с 12 down- и up-sampling слоями  
**Loss Function:** L = Si-SDR_loss + 0.7 × PESQ_Loss  
**Метрики:** Test Loss: -7.41, Test SI-SDR: 8.48, Test PESQ: 1.48  
**Улучшения:** Si-SDR почти не упал, а PESQ увеличился на 0.14 пунктов. Артефактов стало меньше.

### Fine-tuned Si-SDR+PESQ Model
**Архитектура:** WaveNet с 10 down- и up-sampling слоями, увеличенным F_c с 24 до 32  
**Особенности:** Работает со звуками длиной 4 секунды  
**Метрики:** Test Loss: -8.50, Test SI-SDR: 9.49, Test PESQ: 1.59  
**Улучшения:** По сравнению с предыдущей моделью PESQ увеличился на 0.1, а SI-SDR более чем на 1 дБ. Артефактов стало еще меньше.

### DCCRN Model
**Архитектура:** 2D Complex U-Net + GRU backbone  
**Особенности:** Работает с STFT представлением звука  
**Обучение:** Сначала на Si-SDR loss, затем дообучение на Si-SDR+PESQ loss с α=0.7  
**Метрики:** Test Loss: -10.04, Test SI-SDR: 10.77, Test PESQ: 1.73  
**Результат:** По сравнению с WaveNet Test SI-SDR увеличился более чем на 10%, как и PESQ

![DCCRN Architecture](images/image-1.png)
![DCCRN Details](images/image-2.png)
