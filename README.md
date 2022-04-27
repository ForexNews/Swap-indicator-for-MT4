# Swap-indicator-for-MT4
![Swap Indicator MT4 Screen](https://forexnew.org/wp-content/uploads/2021/09/Swap-Indicator.png)
- Indicator showing Swap Rates for Metatrader 4
- Coding for MetaTrader 4 platform and all brokers.

## Inputs Parameter
![Swap Indicator MT4 Input](https://forexnew.org/Download/Swap-indicator-input.png)
- Font Size : 11
- Space : 30
- Font Color : DeepSkyBlue

## Formula
- Swap Cost = (Swap rates x Pip Value x overnight) ÷ 10
- 
### MQL4 Code

```
#property strict
#property copyright "Forexnew.org"
#property link      "https://forexnew.org"
#property version "1.0"
#property description "Swap indicator for Metatrader 4"

double swap_long,swap_short;
int spread;
extern int Font_Size = 11;
extern int Space = 30;
extern color Font_Color = DeepSkyBlue;

int init()
{
   IndicatorShortName("Swap monitor ("+Symbol()+")");
   return(0);
}

int start()
{
   spread=MarketInfo(Symbol(),13);
   swap_long=NormalizeDouble(MarketInfo(Symbol(),18),2);
   swap_short=NormalizeDouble(MarketInfo(Symbol(),19),2);

   ObjectCreate("Swap monitor1", OBJ_LABEL, WindowFind("Swap monitor ("+Symbol()+")"), 0, 0);
   ObjectSetText("Swap monitor1","Spread : "+DoubleToStr(spread ,0), Font_Size, "Arial Black", Font_Color);
   ObjectSet("Swap monitor", OBJPROP_CORNER, 0);
   ObjectSet("Swap monitor1", OBJPROP_XDISTANCE, 20);
   ObjectSet("Swap monitor1", OBJPROP_YDISTANCE, Space);
   ObjectSet("Swap monitor1", OBJPROP_HIDDEN, true);

   ObjectCreate("Swap monitor2", OBJ_LABEL, WindowFind("Swap monitor ("+Symbol()+")"), 0, 0);
   ObjectSetText("Swap monitor2","Buy Swap : "+DoubleToStr( swap_long ,2), Font_Size, "Arial Black", Font_Color);
   ObjectSet("Swap monitor2", OBJPROP_CORNER, 0);
   ObjectSet("Swap monitor2", OBJPROP_XDISTANCE, 20);
   ObjectSet("Swap monitor2", OBJPROP_YDISTANCE, Space+Space);
   ObjectSet("Swap monitor2", OBJPROP_HIDDEN, true);

   ObjectCreate("Swap monitor3", OBJ_LABEL, WindowFind("Swap monitor ("+Symbol()+")"), 0, 0);
   ObjectSetText("Swap monitor3","Sell Swap : "+DoubleToStr( swap_short ,2), Font_Size, "Arial Black", Font_Color);
   ObjectSet("Swap monitor3", OBJPROP_CORNER, 0);
   ObjectSet("Swap monitor3", OBJPROP_XDISTANCE, 20);
   ObjectSet("Swap monitor3", OBJPROP_YDISTANCE, Space+Space+Space);
   ObjectSet("Swap monitor3", OBJPROP_HIDDEN, true);
   return(0);
}

void OnDeinit(const int reason)
{
   ObjectsDeleteAll(0,"Swap monitor1");
   ObjectsDeleteAll(0,"Swap monitor2");
   ObjectsDeleteAll(0,"Swap monitor3");
}
```
#### Visit our website
- [ForexNew.org](https://forexnew.org/)
