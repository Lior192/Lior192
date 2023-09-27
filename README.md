#include <Trade/Trade.mqh>
CTrade trade;

void CancelOrder(){
   for(int i = OrdersTotal()-1; i>=0; i--){
      ulong OrderTicket = OrderGetTicket(i);
      trade.OrderDelete(OrderTicket);
   }
}

void OnTick()
{
   if(PositionsTotal() == 1)
      CancelOrder();
        
            double PositionPriceOpen = PositionGetDouble(POSITION_PRICE_OPEN);
            double PositionStopLoss = PositionGetDouble(POSITION_SL);
            double Bid = SymbolInfoDouble(_Symbol,SYMBOL_BID);
            double Ask = SymbolInfoDouble(_Symbol,SYMBOL_ASK);
            long PositionType = PositionGetInteger(POSITION_TYPE);
               if(PositionType == 0 && Bid <= PositionStopLoss)
                  trade.Sell(0.7,_Symbol,Bid,PositionPriceOpen);
               else if(PositionType == 1 && Ask >= PositionStopLoss)
                  trade.Buy(0.7,_Symbol,Ask,PositionPriceOpen);

       

}
