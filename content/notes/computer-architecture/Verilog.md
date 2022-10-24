```
module hello_world_tb;
  initial begin
    $display("Hello, world!");
  end
endmodule
```

Initial -- блок кода, начиная с которого прога выполняется

```
#t command
```

`#t` -- delay перед выполнением данной команды

Бывают переменные 2 видов:
- провода (keyword: `reg`)
- регистры

У них может быть 4 состояния:
- 0
- 1
- x -- неизвестное состояние (синие провода в logisim)
- z -- отсутствие состояния


Многобитовые регистры:
```
reg[3:0] b; // потому что [3, 2, 1, 0]
```

Форматы чисел:
- `4'b1001` -- двоичная
- `4'd42` -- десятичная
Первое число -- количество бит

Схемы можно дебажить: `$monitor` -- похож на `$display`, но вывод каждый раз, когда изменяются его аргументы

Отдельная функция для инвертора:
```
module not_switch(
  output wire out,
  input wire in
);
  supply1 PWR;
  supply0 GRD;
  
  pmos p1(out, PWR, in);
  nmos n1(out, GRD, in);
endmodule
```

`supply0` -- земля
`supply1` -- питание
`pmos` -- p транзистор
`pmos(drain, source, gate)`


```
module not_switch(
  output wire out,
  input wire in
);
  supply1 PWR;
  supply0 GRD;
  
  pmos p1(out, PWR, in);
  nmos n1(out, GRD, in);
endmodule

module nand_switch(
  output wire out,
  input wire A,
  input wire B,
);
  supply0 GRD;
  supply1 PWR;
  
  wire w;
  
  pmos p1(w, PWR, A);
  pmos p2(out, w, B);
  
  nmos n1(out, GRD, A);
  nmos n2(out, GRD, B);
endmodule
```