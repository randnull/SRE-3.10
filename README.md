Немного меняем docker-compose для создания общей сети:


networks:
  monitoring:
    driver: bridge

Разворачием и добавляем текстовые данные:

![Иллюстрация к проекту](https://github.com/randnull/SRE-3.10/blob/main/images/first.png)


На данном дашборде изначально не видно проблем, так как установлены неккоректные параметры

1. Переменная timeWindow задает фиксированное количество времени, за которое берется максимум, но из-за этого мы можем пропустить "плохое" значние
2. Не задан параметр min_interval, поэтому не выполнено условие об ограничении снизу (x2 от интервала скрейпа)
3. step аналогочно фиксированный

Решение:

1. уберем переменную timeWindow, заменив ее на __interval. Это позволит не пропускать "плохих значений"
2. как видно по метрикам, scape interval = 30s, поэтому установим min_interval = 1m
3. для переменной step аналогично зададим __interval в качестве значения 

Итоговый дашборд (видны пики на первом графике и максимальное значение за последние 5m на втором)

![Иллюстрация к проекту](https://github.com/randnull/SRE-3.10/blob/main/images/solve.png)
