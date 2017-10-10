orm事件 当`sale_status`改变时记录
```
if ($order->isDirty('sale_status')) {
    $log              = new OrderSaleStatusLog();
    $log->order_id    = $order->id;
    $log->staff_id    = auth()->user()->id;
    $log->staff_name  = auth()->user()->name;
    $log->sale_status = $order->sale_status;
    $log->reason      = "从" . Config('status.sale')[$order->getOriginal('sale_status')]
        . "变为" . Config('status.sale')[$order->sale_status];
    $log->save();
}
```