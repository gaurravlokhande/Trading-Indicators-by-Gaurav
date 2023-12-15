# Trading-Indicators

## Ut Bot Combined

```
//@version=4

study("UT Bot - Instances", shorttitle="UT Bot", overlay=true)
src = close

// Instance 1
keyvalue = input(3, title="Key Value - Instance 1", step=.5)
atrperiod = input(10, title="ATR Period - Instance 1")
xATR = atr(atrperiod)
nLoss = keyvalue * xATR

xATRTrailingStop = 0.0
xATRTrailingStop := iff(src > nz(xATRTrailingStop[1], 0) and src[1] > nz(xATRTrailingStop[1], 0), max(nz(xATRTrailingStop[1]), src - nLoss),
   iff(src < nz(xATRTrailingStop[1], 0) and src[1] < nz(xATRTrailingStop[1], 0), min(nz(xATRTrailingStop[1]), src + nLoss),
   iff(src > nz(xATRTrailingStop[1], 0), src - nLoss, src + nLoss)))

pos = 0
pos := iff(src[1] < nz(xATRTrailingStop[1], 0) and src > nz(xATRTrailingStop[1], 0), 1,
   iff(src[1] > nz(xATRTrailingStop[1], 0) and src < nz(xATRTrailingStop[1], 0), -1, nz(pos[1], 0)))

xcolor = pos == -1 ? color.new(color.red, 0) : pos == 1 ? color.new(color.green, 0) : color.new(color.blue, 0)

plot(xATRTrailingStop, color=xcolor, title="Trailing Stop - Instance 1")
buy = crossover(src, xATRTrailingStop)
sell = crossunder(src, xATRTrailingStop)
barcolor = src > xATRTrailingStop

plotshape(buy, title="Buy - Instance 1", text='Buy', style=shape.labelup, location=location.belowbar, color=color.new(color.green, 0), textcolor=color.white, size=size.tiny)
plotshape(sell, title="Sell - Instance 1", text='Sell', style=shape.labeldown, color=color.new(color.red, 0), textcolor=color.white, size=size.tiny)

barcolor(barcolor ? color.new(color.green, 0) : color.new(color.red, 0))

alertcondition(buy, title='UT BOT Buy - Instance 1', message='UT BOT Buy - Instance 1')
alertcondition(sell, title='UT BOT Sell - Instance 1', message='UT BOT Sell - Instance 1')


// Instance 2
keyvalue2 = input(3, title="Key Value - Instance 2", step=.5)
atrperiod2 = input(10, title="ATR Period - Instance 2")
xATR2 = atr(atrperiod2)
nLoss2 = keyvalue2 * xATR2

xATRTrailingStop2 = 0.0
xATRTrailingStop2 := iff(src > nz(xATRTrailingStop2[1], 0) and src[1] > nz(xATRTrailingStop2[1], 0), max(nz(xATRTrailingStop2[1]), src - nLoss2),
   iff(src < nz(xATRTrailingStop2[1], 0) and src[1] < nz(xATRTrailingStop2[1], 0), min(nz(xATRTrailingStop2[1]), src + nLoss2),
   iff(src > nz(xATRTrailingStop2[1], 0), src - nLoss2, src + nLoss2)))

pos2 = 0
pos2 := iff(src[1] < nz(xATRTrailingStop2[1], 0) and src > nz(xATRTrailingStop2[1], 0), 1,
   iff(src[1] > nz(xATRTrailingStop2[1], 0) and src < nz(xATRTrailingStop2[1], 0), -1, nz(pos2[1], 0)))

xcolor2 = pos2 == -1 ? color.new(color.red, 0) : pos2 == 1 ? color.new(color.green, 0) : color.new(color.blue, 0)

plot(xATRTrailingStop2, color=xcolor2, title="Trailing Stop - Instance 2")
buy2 = crossover(src, xATRTrailingStop2)
sell2 = crossunder(src, xATRTrailingStop2)
barcolor2 = src > xATRTrailingStop2

plotshape(buy2, title="Buy - Instance 2", text='Buy', style=shape.labelup, location=location.abovebar, color=color.new(color.green, 0), textcolor=color.white, size=size.tiny)
plotshape(sell2, title="Sell - Instance 2", text='Sell', style=shape.labeldown, color=color.new(color.red, 0), textcolor=color.white, size=size.tiny)

barcolor(barcolor2 ? color.new(color.green, 0) : color.new(color.red, 0))

alertcondition(buy2, title='UT BOT Buy - Instance 2', message='UT BOT Buy - Instance 2')
alertcondition(sell2, title='UT BOT Sell - Instance 2', message='UT BOT Sell - Instance 2')

```
