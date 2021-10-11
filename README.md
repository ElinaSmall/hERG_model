# hERG_model
Кардиотоксичность  наиболее часто наблюдается при приеме препаратов, имеющих высокие показатели аффинности к hERG-каналам (hERG: human ether-à-go-go  related gene кодирует альфа-субъединицу калиевых каналов KCNH2). Доказано, что блокада калиевых каналов KCNH2 приводит к QT-пролонгации на ЭКГ. Впоследствии это приводит к возникновению у пациента аритмии по типу Torsades de Pointes (TdP), риска желудочковой фибрилляция и спонтанной смерти. 

![me](https://github.com/ElinaSmall/hERG_model/blob/main/images/ecg-qrscomplex.gif)
![me](https://github.com/ElinaSmall/hERG_model/blob/main/images/Torsades_de_Pointes_heart_monitor_animation.gif)

Согласно гайдлайну [ICH E14](https://pubmed.ncbi.nlm.nih.gov/18329284/)  строго рекомендуется на ранних стадиях разработки учитывать потенциальную кардиотоксичность разрабатываемой молекулы. Известные лекарства были ограничены в применениии или сняты с производства в связи с высоким риском кардиотоксичности: Astemizole, Terfenadine, Grepafloxacine, Cisapride.

> Raschi E. et al. The hERG K+ channel: target and antitarget strategies in drug development //Pharmacological research. – 2008. – Т. 57. – №. 3. – С. 181-195.

Обзор существующих моделей: 
![Image alt](https://github.com/ElinaSmall/hERg_model/raw/main/images/Обзор.JPG)

> Rácz A. et al. Machine learning models for classification tasks related to drug safety //Molecular Diversity. – 2021. – С.1-16.

 В [данной статье](https://www.nature.com/articles/s41598-019-47536-3) авторы также отмечают, что в случае использования дескрипторов ECFP c алгоритмом SVM при обучении на выборке из одного датасета и проверке на тестовой выборке из принципально разного источника, результаты  ROC scores максимум достигают 0.694, а значенний около 0.870 можно получить только в том случае, если обучающая и тестовая выборка составлены из одного датасета. В данной статье датасет получен из всех возможных источников, далее все соединения были кластеризованы и из каждого выбрано наиболее репрезентативное соединение (87 361). Из дескрипторов помимо ECFP_4 используют около 400 других дескрипторов (посчитанных в том числе квантово-химическими методами) (ECFP+72 дескриптора), а затем отбор дескрипторов по генетическому алгоритму. В результате всех перечисленных действий авторы статьи смогли добиться результата ROC_AUC = 	0.962.
Сходимого результата добились [авторы применения метода 3D-QSAR](https://www.frontiersin.org/articles/10.3389/fchem.2017.00007/full). 

Работа состояла из следующих этапов:
1. Работа с открытыми базами данных соединений.
  - ChEMBL
    - Анализ всех методов исследования  аффинности к hERG in vitro (PatchXpress, флуоресцентный анализ, метод радиолигандного связывания и др.)
    - Извлечение и объединение результатов in-vitro исследований по оценке аффинности соединений к hERG-каналам. Принимались во внимание исключительно исследования на белке калиевого канала, полученного от вида Homo sapiens.
    - Исключение всех записей, относящихся к исследованиям на мутантах hERG-каналов.
    - Удаление дубликатов соединений по ChEMBL ID
    - Приведение единиц измерения IC50  к nM , расчет pIC50, исключение неопределенных размерностей, а также пропущенных значений.
    - Исключение солевых форм, стандартизация соединений с помощью RDkit.
  - hERG-central
    - Приведение единиц измерения IC50  к nM , расчет pIC50, исключение неопределенных размерностей, а также пропущенных значений.
    - Создание тестовой (валидационной) выборки.
2. Анализ датасета.
  - Статистический анализ по целевому значению переменной.
  - Анализ на схожесть обучающей и тестовой выборок.
  - Оценка возможного влияния стереоизомеров на модель.
3. Подбор и анализ дескрипторов. Построение моделей.
  - Morgan fingerprints (ECFP). 
  - Поиск корреляции целевого значения со структурными, физико-химическими дескрпторами, наличием отдельных фрагментов.
  - Поиск корреляции целевого значения с рядом дескрипторов, вычисленных программой Shroedinger.
  - Использование PaDEL программы для расчета дескрипторов.
  - Использование фармакофорных 2D fingerprints.
4. Оценка модели на независимой выборке из hERG-central (in-house данных).

С результатами работы можно ознакомиться по ссылке: <https://github.com/ElinaSmall/hERG_model/blob/main/Results.md>
