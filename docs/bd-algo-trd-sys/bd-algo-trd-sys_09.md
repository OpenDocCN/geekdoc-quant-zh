# 附录 A

猴子交易示例，TradeStation 简易语言代码

## ![images](img/gbox.jpg) 策略 1：基线策略（无随机性）

```py

input: nContracts(1);
var:ssl1(1);
var:ssl(2000);
    if date >= 1070316 and date < 1080314 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1080314 and date < 1090311 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1090311 and date < 1100310 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1100310 and date < 1110309 then
begin
        ssl1 = 0.5 ;
    end ;

    if date >= 1110309 and date < 1120310 then
   begin
        ssl1 = 0.5 ;
    end ;
    if date >= 1120310 and date < 1130308 then
   begin
        ssl1 = 1.25 ;
    end ;
    if date >= 1130308 and date < 1140308 then
   begin
        ssl1 = .75 ;
    end ;

	 if date >= 1070316 then begin

if close<close[1] and close[1]<close[2] then begin
buy ncontracts Contracts next bar at market;
End;

if close>close[1] and close[1]>close[2] then begin
SellShort ncontracts Contracts next bar at market;
End;

SetStopContract;

setstoploss(minlist(ssl1*BigPointValue*avgtruerange(14),ssl));

end; 
```

## ![images](img/gbox.jpg) 策略 2：随机入场，基线出场策略

```py

input:
iter(1),percentlong(.400),holdbars(2.5),exitclose(0),oddstradetoday(.47),begindate(1070319);
var:posstradetoday(0);

//entry is random

input: nContracts(1);
var:ssl1(1);
var:ssl(2000);
    if date >= 1070316 and date < 1080314 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1080314 and date < 1090311 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1090311 and date < 1100310 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1100310 and date < 1110309 then
    begin
        ssl1 = 0.5 ;
    end ;

    if date >= 1110309 and date < 1120310 then
    begin
        ssl1 = 0.5 ;
    end ;
    if date >= 1120310 and date < 1130308 then
   begin
        ssl1 = 1.25 ;
    end ;
    if date >= 1130308 and date < 1130501 then
   begin
        ssl1 = .75 ;
    end ;

 if date >= 1070316 then begin

if close<close[1] and close[1]<close[2] then begin
sell ncontracts Contracts next bar at market;
End;

if close>close[1] and close[1]>close[2] then begin
buytocover ncontracts Contracts next bar at market;
End;

SetStopContract;

setstoploss(minlist(ssl1*BigPointValue*avgtruerange(14),ssl));

end;

posstradetoday=random(1); //random number for today’s trade

If date>begindate then begin

If posstradetoday<=oddstradetoday then begin //trade will occur today

    //enter trade
    If random(1)<percentlong then buy this bar at close
    Else sellshort this bar at close;
  end;
end; 
```

## ![images](img/gbox.jpg) 策略 3：基线入场，随机出场策略

```py

input:
iter(1),percentlong(.400),holdbars(2.5),exitclose(0),oddstradetoday(.47),begindate(1070319);
var:posstradetoday(0);

//exit is random

input: nContracts(1);
var:ssl1(1);
var:ssl(2000);
    if date >= 1070316 and date < 1080314 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1080314 and date < 1090311 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1090311 and date < 1100310 then
    begin
        ssl1 = 0.75 ;
    end ;
    if date >= 1100310 and date < 1110309 then
    begin
        ssl1 = 0.5 ;
    end ;

    if date >= 1110309 and date < 1120310 then
    begin
        ssl1 = 0.5 ;
    end ;
    if date >= 1120310 and date < 1130308 then
   begin
        ssl1 = 1.25 ;
    end ;
    if date >= 1130308 and date < 1140308 then
   begin
        ssl1 = .75 ;
    end ;

 if date >= 1070316 then begin

if close<close[1] and close[1]<close[2] and marketposition=0 then begin
buy ncontracts Contracts next bar at market;
End;

if close>close[1] and close[1]>close[2] and marketposition=0 then begin
SellShort ncontracts Contracts next bar at market;
End;

end;

posstradetoday=random(1); //random number for today’s trade

If barssinceentry>=random(2*holdbars) then begin
  Sell this bar at close;
  Buytocover this bar at close;
end;

 If exitclose=1 then setexitonclose; 
```

## ![images](img/gbox.jpg) 策略 4：随机入场，随机出场策略

```py

input:
iter(1),percentlong(.400),holdbars(2.5),exitclose(0),oddstradetoday(.48),begindate(1070319);
var:posstradetoday(0);

posstradetoday=random(1); //random number for today’s trade

If date>begindate then begin

 If posstradetoday<=oddstradetoday then begin //trade will occur today
    //enter trade
    If random(1)<percentlong then buy this bar at close
     Else sellshort this bar at close;

  end;
end;

If barssinceentry>=random(2*holdbars) then begin
    Sell this bar at close;
    Buytocover this bar at close;
end;

    If exitclose=1 then setexitonclose; 
```
