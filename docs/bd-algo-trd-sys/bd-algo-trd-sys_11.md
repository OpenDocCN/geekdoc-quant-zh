# 附录 C

欧元日策略，TradeStation 简易语言格式

```py

var:xb(2),xb2(50),pipadd(1),Stopl(400),proft(5000);
    if date >= 1091118 and date < 1101025 then
    begin
       xb = 4 ;
       xb2 = 70 ;
       pipadd = 2 ;
       Stopl = 275 ;
    end ;
    if date >= 1101025 and date < 1110929 then
    begin
       xb = 4 ;
       xb2 = 72 ;
       pipadd = 5 ;
       Stopl = 225 ;
    end ;
    if date >= 1110929 and date < 1120904 then
    begin
       xb = 3 ;
       xb2 = 74 ;
       pipadd = 8 ;
       Stopl = 425 ;
end ;
    if date >= 1120904 and date < 1130812 then
    begin
       xb = 3 ;
       xb2 = 74 ;
       pipadd = 11 ;
       Stopl = 425 ;
    end ;
    if date >= 1130812 and date < 11400101 then
    begin
       xb = 5 ;
       xb2 = 80 ;
       pipadd = 8 ;
       Stopl = 425 ;
    end ;

var:cs(0),tradestoday(0),startprof(0),starttrades(0),stoplo(0);

cs=currentsession(0);

If cs<>cs[1] then begin
    tradestoday=0;
    startprof=NetProfit + OpenPositionProfit;
    starttrades=TotalTrades;
    Stoplo=stopl;
end;

If totaltrades<>starttrades or marketposition<>0 or startprof<>NetProfit + OpenPositionProfit then tradestoday=1;

If tradestoday=0 and time<1500 and date >= 1091118 then begin

//entry rules

If (high>=highest(high,xb) and close<close[xb2] ) then begin
    sellshort next bar at high+pipadd/10000 limit;
end;

If low<=lowest(low,xb) and close>close[xb2] then begin
    buy next bar at low-pipadd/10000 limit;
end;

end;

//exit rules

Setstopposition;
setstoploss(stoplo);
setprofittarget(proft);

setexitonclose; 
```
