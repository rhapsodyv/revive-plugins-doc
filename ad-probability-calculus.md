Ad Probability Calculus
==================

This doc describes how revive maintenance system calculates the ads probabilities.

Required impressions for banner in the next hour:
```
                                                  [zone impressions delivered last hour]
[banner remaining impressions] *  ----------------------------------------------------------------------------
                                    [sum zone impressions delivered from last hour to end of today 7 days ago]
```

Banner priority:
```
          [banner remaining impressions]
--------------------------------------------------------
      [zone impressions delivered last hour]
```

**This equations are a rough representation of the real calculus. It has things like taking account of blocked impressions and other stuff.**
