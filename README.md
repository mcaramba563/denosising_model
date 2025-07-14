# WaveNet for Speech Denoising with Si-SDR and Si-SDR+PESQ Losses
Проект для шумоподавления в звуке с помощью Wave-Net. Сравнение результатов для Si-SDR and Si-SDR+PESQ лоссов.

## Структура проекта
- notebooks/ - Jupyter-ноутбуки с исследованиями и пайплайнами
- models/ - Предобученные модели
- examples/ - примеры шумоподавления в звуках

## Использование
Основные ноутбуки:
- denoising_si-sdr.ipynb - Обучение и тестирование модели на основе si-sdr loss
- denoised_si-sdr_pesq_07.ipynb - Обучение и тестирование модели на основе si-sdr+pesq loss с alpha=0.7

## Модели
- si-sdr_model.pt
- si-sdr_pesq_model.pt

## Dataset
В качестве датасета использован Libri Speech Noise Dataset.

Для train датасета из каждого сэмпла выбирается случайные 3 секунды.

Для valid и test датасета каждый звук полностью разбивается на отрезки длинной 3 секунды и вводится в модель.

## Si-SDR model
В качестве модели использован WaveNet c 12 down- и up- sampling.

В результате получили следующие метрики:

Test SI-SDR: 8.529809951782227, Test PESQ: 1.3428624216526268

Несколько примеров:

Noised:

<audio controls src="./examples/si_sdr/1-noise.wav" title="Title"></audio>
<audio controls src="./examples/si_sdr/2-noise.wav" title="Title"></audio>

Clear:

<audio controls src="./examples/si_sdr/1-clear.wav" title="Title"></audio>
<audio controls src="./examples/si_sdr/2-clear.wav" title="Title"></audio>

Слышно, что после шумоподавления присутствует много артефактов


## Si-SDR_PESQ model
Здесь использован лосс: L = SI-DSR_loss + alpha * PESQ_Loss

Лучшая, показавшая себя alpha равна 0.7

Test Loss: -7.4072041511535645, Test SI-SDR: 8.480247497558594, Test PESQ: 1.4842217170151453

Видно, что SI-SDR почти не упал, а PESQ увеличился на 0.14 пунктов

Также слышно, что артефактов стало меньше


Noised:

<audio controls src="examples/si_sdr_pesq/1-noise.wav" title="Title"></audio>
<audio controls src="examples/si_sdr_pesq/2-noise.wav" title="Title"></audio>

Clear:

<audio controls src="examples/si_sdr_pesq/1-clear.wav" title="Title"></audio>
<audio controls src="examples/si_sdr_pesq/2-clear.wav" title="Title"></audio>
