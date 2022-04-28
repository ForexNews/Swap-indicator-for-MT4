# Swap-indicator-for-MT4
- Indicator showing Swap Rates for Metatrader 4
- Display Swap rate for a long and short positions on the screen.
- Coding for MetaTrader 4 platform and all brokers.

![Swap Indicator MT4 Screen](https://forexnew.org/Download/Swap-Indicator.png)

## Inputs Parameter
- Font Size : 11
- Space : 30
- Font Color : DeepSkyBlue

![Swap Indicator MT4 Input](https://forexnew.org/Download/Swap-indicator-input.png)

## Formula
- Swap Cost = (Swap rates x Pip Value x overnight) ÷ 10

### MQL4 Code

```
#property strict
#property copyright "Forexnew.org"
#property link      "https://forexnew.org"
#property version "1.0"
#property description "Swap indicator for Metatrader 4"

extern int Font_Size = 11;
extern int Space = 30;
extern color Font_Color = DeepSkyBlue;
string Font_Style = "Arial Black";
double swap_long,swap_short;
int spread;

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
   ObjectSetText("Swap monitor1","Spread : "+DoubleToStr(spread ,0), Font_Size, Font_Style, Font_Color);
   ObjectSet("Swap monitor", OBJPROP_CORNER, 0);
   ObjectSet("Swap monitor1", OBJPROP_XDISTANCE, 20);
   ObjectSet("Swap monitor1", OBJPROP_YDISTANCE, Space);
   ObjectSet("Swap monitor1", OBJPROP_HIDDEN, true);

   ObjectCreate("Swap monitor2", OBJ_LABEL, WindowFind("Swap monitor ("+Symbol()+")"), 0, 0);
   ObjectSetText("Swap monitor2","Buy Swap : "+DoubleToStr( swap_long ,2), Font_Size, Font_Style, Font_Color);
   ObjectSet("Swap monitor2", OBJPROP_CORNER, 0);
   ObjectSet("Swap monitor2", OBJPROP_XDISTANCE, 20);
   ObjectSet("Swap monitor2", OBJPROP_YDISTANCE, Space+Space);
   ObjectSet("Swap monitor2", OBJPROP_HIDDEN, true);

   ObjectCreate("Swap monitor3", OBJ_LABEL, WindowFind("Swap monitor ("+Symbol()+")"), 0, 0);
   ObjectSetText("Swap monitor3","Sell Swap : "+DoubleToStr( swap_short ,2), Font_Size, Font_Style, Font_Color);
   ObjectSet("Swap monitor3", OBJPROP_CORNER, 0);
   ObjectSet("Swap monitor3", OBJPROP_XDISTANCE, 20);
   ObjectSet("Swap monitor3", OBJPROP_YDISTANCE, Space+Space+Space);
   ObjectSet("Swap monitor3", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Swap monitor4", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Swap monitor4","Copyright: ForexNew.org - Free Opensource",9, "Arial", DeepSkyBlue);
   ObjectSet("Swap monitor4", OBJPROP_CORNER, 2);
   ObjectSet("Swap monitor4", OBJPROP_XDISTANCE, 10);
   ObjectSet("Swap monitor4", OBJPROP_YDISTANCE, 10);
   ObjectSet("Swap monitor4", OBJPROP_SELECTABLE, false);
   ObjectSet("Swap monitor4", OBJPROP_HIDDEN, true);
   return(0);
}

void OnDeinit(const int reason)
{
   ObjectsDeleteAll(0,"Swap monitor1");
   ObjectsDeleteAll(0,"Swap monitor2");
   ObjectsDeleteAll(0,"Swap monitor3");
   ObjectsDeleteAll(0,"Swap monitor4");
}
```
#### Visit our website
- [ForexNew.org](https://forexnew.org/)
