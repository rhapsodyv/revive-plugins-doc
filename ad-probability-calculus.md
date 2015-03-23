Ad Probability Calculus
==================

This doc describes how revive maintenance system calculates the ads probabilities for contract campaigns (without ecpm optimization).

Banner remaining impressions[1]:
```
[campaign targeting impressions] - [campaign delivered impressions]

==> Distributed to the campaign banners taking in account banner weights
```

Required impressions for banner in the next hour[2]:
```
                                                  [zone impressions delivered last hour]
[[1]banner remaining impressions] *  ----------------------------------------------------------------------------
                                    [sum zone impressions delivered from last hour to end of today 7 days ago]
```

Banner priority:
```
          [[2]banner required impressions]
--------------------------------------------------------
      [zone impressions delivered last hour]
```

**This equations are a rough representation of the real calculus. It has things like taking account of blocked impressions and other stuff.**
