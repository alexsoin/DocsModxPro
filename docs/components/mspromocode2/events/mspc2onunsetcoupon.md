# mspc2OnUnsetCoupon

Срабатывает после отмены промо-кода у корзины или заказа.

## Параметры

- `array $coupon` — массив с промо-кодом
- `null|msOrder $order` — объект заказа `msOrder` или `null`, если промо-код отменён у корзины