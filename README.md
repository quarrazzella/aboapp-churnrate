## Предсказываем отток пользователей из мобильного банка на основе данных AppMetrica

Задача - "Создать таблицу данных по пользователям приложения АБО 3, на основе которой за счет моделей машинного обучения, используемых в банке, можно с 90% точностью предсказать месячный отток пользователей". Таблица доступна в репозитории (df_main.csv)

### Описание признаков

Ниже находится краткое описание признаков, данные за июнь 2018. 

**DeviceID** - Уникальный идентификатор устройства, который устанавливает AppMetrica.

**sessions_totalnumber** - Общее количество сессий, совершенных устройством.

**sessions_avgdaylag** - Среднее количество дней между сессиями. Например, пользователь был в приложении 1, 3 и 7 июня. sessions_avgdaylag = (1 + 3) / 2 = 2

**sessions_totaldaysactive** - Количество дней, в течение которых была зафиксирована хотя бы одна сессия. Например, у пользователя было 10 сессий 1 июня и 1 сессия 2 июня. sessions_totaldaysactive = 2

**sessions_daysSinceLastSession** - Количество дней, прошедших с последней сессии пользователя. Дата среза - 1 июля.

**payments_operationAmount_count** - Количество платежей на каждое устройство.

**payments_operationAmount_sum** - Сумма размеров платежей

**payments_operationAmount_median** - Медиана размеров платежей

**payments_operationAmount_min** - Минимальная сумма платежа

**payments_operationAmount_max** - Минимальная сумма платежа

**payments_sender_nunique** - Уникальное количество источников платежей. Например, карта или счет, иное.

**payments_recipient_nunique** - Уникальное количество получателей платежей.

**payments_operationMethod_nunique** - Уникальное количество способ проведения платежа. Например, стандарт, шаблон, автоплатеж.

**payments_avgdaylag** - Среднее количество дней между платежами.

**payments_daysactive** - Количество дней, в течение которых был хотя бы один платеж.

**payments_daysSinceLastPayment** -Количество дней, прошедших с последнего платежа пользователя. Дата среза - 1 июля.

**transfers_operationAmount_count** - Количество переводов на каждое устройство.

**transfers_operationAmount_sum** - Сумма переводов

**transfers_operationAmount_median** - Медиана размеров переводов.

**transfers_operationAmount_min** - Минимальный размер перевода.

**transfers_operationAmount_max** - Максимальный размер перевода.

**transfers_operationFee_sum** - Минимальный размер перевода.

**transfers_sender_nunique** -Уникальное количество источников платежей.

**transfers_recipient_nunique** - Уникальное количество получателей платежей.

**transfers_operationMethod_nunique** - Уникальное количество способ проведения платежа.

**transfers_senderCurrency_nunique** - Уникальное количество валют источников переводов.

**transfers_recipientCurrency_nunique** -никальное количество валют получателей переводов.

**transfers_avgdaylag** -Среднее количество дней между переводами.

**transfers_daysactive** - Среднее количество дней между переводами.

**fundTransfers_daysSinceLastTransfer** - Количество дней, в течение которых был хотя бы один перевод.

**churned** - 0 = в июле 2018 была зафиксирована хотя бы 1 сессия на данное устройство, 1 - ни одной сессии. 

## Особенности DataFrame 

Посмотрим на пропуски в данных

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 130885 entries, 0 to 130884
Data columns (total 31 columns):
DeviceID                               130885 non-null uint64
sessions_totalnumber                   130885 non-null int64
sessions_avgdaylag                     130885 non-null float64
sessions_totaldaysactive               130885 non-null int64
sessions_daysSinceLastSession          130885 non-null int64
payments_operationAmount_count         61798 non-null float64
payments_operationAmount_sum           61798 non-null float64
payments_operationAmount_median        61798 non-null float64
payments_operationAmount_min           61798 non-null float64
payments_operationAmount_max           61798 non-null float64
payments_sender_nunique                61798 non-null float64
payments_recipient_nunique             61798 non-null float64
payments_operationMethod_nunique       61798 non-null float64
payments_avgdaylag                     61798 non-null float64
payments_daysactive                    61798 non-null float64
payments_daysSinceLastPayment          61798 non-null float64
transfers_operationAmount_count        57108 non-null float64
transfers_operationAmount_sum          57108 non-null float64
transfers_operationAmount_median       57108 non-null float64
transfers_operationAmount_min          57108 non-null float64
transfers_operationAmount_max          57108 non-null float64
transfers_operationFee_sum             56377 non-null float64
transfers_sender_nunique               57108 non-null float64
transfers_recipient_nunique            57108 non-null float64
transfers_operationMethod_nunique      57108 non-null float64
transfers_senderCurrency_nunique       57108 non-null float64
transfers_recipientCurrency_nunique    57108 non-null float64
transfers_avgdaylag                    57108 non-null float64
transfers_daysactive                   57108 non-null float64
fundTransfers_daysSinceLastTransfer    57108 non-null float64
churned                                130885 non-null int64
```
