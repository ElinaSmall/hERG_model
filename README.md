# hERG_model
Кардиотоксичность  наиболее часто наблюдается при приеме препаратов, имеющих высокие показатели аффинности к hERG-каналам (hERG: human ether-à-go-go  related gene кодирует альфа-субъединицу калиевых каналов KCNH2). Доказано, что блокада калиевых каналов KCNH2 приводит к QT-пролонгации на ЭКГ. Впоследствии это приводит к возникновению у пациента аритмии по типу Torsades de Pointes (TdP), риска желудочковой фибрилляция и спонтанной смерти. Согласно гайдлайну ICH E14  строго рекомендуется на ранних стадиях разработки учитывать потенциальную кардиотоксичность разрабатываемой молекулы.
Работа состояла из следующих этапов:
1. Работа с открытыми базами данных соединений.
  i. ChEMBL
    - Анализ всех методов исследования  аффинности к hERG in vitro (PatchXpress, флуоресцентный анализ, метод радиолигандного связывания и др.)
    - Извлечение и объединение результатов in-vitro исследований по оценке аффинности соединений к hERG-каналам. Принимались во внимание исключительно исследования на белке калиевого канала, полученного от вида Homo sapiens.
    - Исключение всех записей, относящихся к исследованиям на мутантах hERG-каналов.
    - Удаление дубликатов соединений по ChEMBL ID
    - Приведение единиц измерения IC50  к nM , расчет pIC50, исключение неопределенных размерностей, а также пропущенных значений.
    - Исключение солевых форм, стандартизация соединений с помощью RDkit.
  ii. hERG-central
    - Приведение единиц измерения IC50  к nM , расчет pIC50, исключение неопределенных размерностей, а также пропущенных значений.
    - Создание тестовой (валидационной) выборки.
2. Анализ датасета.
  i. Статистический анализ по целевому значению переменной.
  ii. Анализ на схожесть обучающей и тестовой выборок.
  iii. Оценка возможного влияния стереоизомеров на модель.
3. Подбор и анализ дескрипторов. Построение моделей.
  i. Morgan fingerprints (ECFP). 
  ii. Поиск корреляции целевого значения со структурными, физико-химическими дескрпторами, наличием отдельных фрагментов.
  iii. Поиск корреляции целевого значения с рядом дескрипторов, вычисленных программой Shroedinger.
  iiii. Использование PaDEL программы для расчета дескрипторов.
  iiiii. Использование фармакофорных 2D fingerprints.
4. Оценка модели на независимой выборке из hERG-central.
