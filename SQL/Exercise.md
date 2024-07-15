---
aliases: []
---
#### SQL to get play name with most medals
---
- matches
- | match_id | gold  | silver | bronze |
| -------- | ----- | ------ | ------ |
| 1        | Messi | Leo    | Kenny  |
| 2        | Leo   | Kenny  | Messi  |
| 3        | Kenny | Messi  | Leo    |
| 4        | Messi | Kenny  | Leo    |
| 5        | Leo   | Messi  | Kenny  |
| 6        | Kenny | Leo    | Messi  |

- players
- | name  |
| ----- |
| Messi |
| Leo   |
| Kenny |

#### Answer
    select b.name, 
	    sum((b.name = a.gold) + (b.name = a.silver) + (b.name = a.bronze)) as total
    from a inner join b
    on b.name in (a.gold,a.silver,a.bronze)
    group by b.name;

| name  | total |
| ----- | ----- |
| Kenny | 6     |
| Leo   | 6     |
| Messi | 6     |

---
