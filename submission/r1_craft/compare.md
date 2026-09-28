# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_152940.jpg
- R6 mid MISSING
## adasind_167700.jpg
- L6 mid IGNORE_SCOPE
- L7 mid IGNORE_SCOPE
- L8+R6 edge WRONG_CLASS
- R2 mid MISSING
- R8 center MISSING
## adasind_212280.jpg
- L3 mid IGNORE_SCOPE
- L4+R3 edge WRONG_CLASS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 10 | 9 | 1 | 0 |
| mid | 6 | 4 | 2 | 0 |
| edge | 2 | 0 | 2 | 2 |
