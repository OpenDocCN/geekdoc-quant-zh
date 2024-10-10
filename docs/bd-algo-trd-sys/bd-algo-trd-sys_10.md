# 附录 B

欧洲夜间策略，TradeStation 易语言格式

```py

vars: FirstTime (1800),
    LastTime (2359),
    ATRmult (3),
    TRmult (.5),
    Nb (10),
    NATR (60),
    Stoplo(275);

    FirstTime = 1800 ;
    LastTime = 2359 ;

  if date >= 1090721 and date < 1100104 then
  begin
    Nb = 9 ;
    NATR = 93 ;
    ATRmult = 3.15 ;
    TRmult = 0.51 ;
    Stoplo= 425 ;
  end ;
  if date >= 1100104 and date < 1100617 then
  begin
    Nb = 9 ;
NATR = 93 ;
    ATRmult = 2.55 ;
    TRmult = 0.66 ;
    Stoplo= 375 ;
  end ;
  if date >= 1100617 and date < 1101129 then
  begin
    Nb = 14 ;
    NATR = 83 ;
    ATRmult = 2.75 ;
    TRmult = 0.71 ;
    Stoplo= 425 ;
  end ;
  if date >= 1101129 and date < 1110515 then
  begin
    Nb = 14 ;
    NATR = 83 ;
    ATRmult = 2.75 ;
    TRmult = 0.66 ;
    Stoplo= 425 ;
  end ;
  if date >= 1110515 and date < 1111026 then
  begin
    Nb = 19 ;
    NATR = 93 ;
    ATRmult = 3.15 ;
    TRmult = 0.56 ;
    Stoplo= 425 ;
  end ;
  if date >= 1111026 and date < 1120412 then
  begin
    Nb = 14 ;
    NATR = 83 ;
    ATRmult = 2.95 ;
    TRmult = 0.61 ;
    Stoplo= 425 ;
  end ;
  if date >= 1120412 and date < 1120924 then
  begin
    Nb = 14 ;
    NATR = 93 ;
    ATRmult = 2.95 ;
    TRmult = 0.61 ;
    Stoplo= 425 ;
  end ;
if date >= 1120924 and date < 1130310 then
  begin
    Nb = 19 ;
    NATR = 73 ;
    ATRmult = 3.15 ;
    TRmult = 0.71 ;
    Stoplo= 425 ;
  end ;
  if date >= 1130310 and date < 1130826 then
  begin
    Nb = 14 ;
    NATR = 93 ;
    ATRmult = 2.95 ;
    TRmult = 0.51 ;
    Stoplo= 425 ;
  end ;
  if date >= 1130826 and date < 1140101 then
  begin
    Nb = 14 ;
    NATR = 93 ;
    ATRmult = 2.55 ;
    TRmult = 0.71 ;
    Stoplo= 425 ;
  end ;
Var: LongPrice(0), ShortPrice(0), LongTarget(0), ShortTarget(0);

//limit entry prices
ShortPrice = Average(Low, Nb) + ATRmult * AvgTrueRange(NATR);
LongPrice = Average(High, Nb) - ATRmult * AvgTrueRange(NATR);

{code to ensure only 1 order is entered at each bar - order closest to price}
var:diff1(0),diff2(0),EntrytoPick(0);
EntrytoPick=0;
diff1=absvalue(close-LongPrice);
diff2=absvalue(close-ShortPrice);
If diff1<=diff2 then EntryToPick=1;
If diff1>diff2 then EntryToPick=2;

if date >= 1090721 and MarketPosition = 0 and EntriesToday(Date) < 1 and Time >= FirstTime and Time < LastTime then begin

If EntryToPick=1 then begin
    Buy(“Long Entry”) next bar at LongPrice limit;
end;

If EntryToPick=2 then begin
    Sell short(“Short Entry”) next bar at ShortPrice limit;
end;

end;

If MarketPosition=-1 then begin
    ShortTarget = EntryPrice - TRmult * TrueRange;
    Buy to cover(“Short Exit”) next bar at ShortTarget limit;
end;

If MarketPosition =1 then begin
    LongTarget = EntryPrice + TRmult * TrueRange;
    Sell(“Long Exit”) next bar at LongTarget limit;
end;

Setstopposition;
setstoploss(stoplo);

SetExitOnClose; 
```
