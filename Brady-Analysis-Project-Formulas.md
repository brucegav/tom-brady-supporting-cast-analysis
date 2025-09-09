# Brady Analysis Project Formulas

##Quarterly QB EPA

$$
QB\_EPA_{quarter} = \frac{1}{n} * \sum(QB\_EPA_{i}) \text{ for all plays in quarter q}
$$

## Clutch 4th Quarter QB EPA:

$$
Clutch\_EPA = \frac{1}{n} * \sum(QB\_EPA_{i}) \\
 \text { where: quarter = 4 AND |score differential| <= 10}
$$

## Third Down EPA:

$$
Third\_Down\_EPA = \frac{1}{n} * \sum(QB\_EPA_{i})\\ \text{ where: down = 3}
$$

## QB Composite Z-Score:

$$
Z\_Score = \frac{X-\mu}{\sigma} \\ \text { where } \mu = \text{ season mean}, \sigma =\text{ season std dev}
$$

$$
QB\_{Composite} = 0.35 \cdot Z\_{pass\_{yds}} + 0.25 \cdot Z\_{pass\_{TDs}} + 0.20 \cdot Z\_{comp\_{pct}} + 0.15 \cdot Z\_{rush\_{yds}} + 0.10 \cdot Z\_{rush\_{TDs}} - 0.20 \cdot Z\_{interceptions}
$$

$$
QB\_{Value\_{Above\_{Replacement}} = QB\_{Composite} - P\_{20}(QB\_{Composite})}
$$

$$
Qualified\_{Season} = \begin{cases} 
True & \text{if attempts} \geq 250 \\
False & \text{otherwise}
\end{cases}
$$

## RB Composite Z-Score:

$$
RB\_{Composite} = 0.30 \cdot Z\_{rush\_{yds}} + 0.20 \cdot Z\_{rush\_{TDs}} + 0.20 \cdot Z\_{yds\_{per\_{carry}}} + 0.10 \cdot Z\_{rec\_{yds}} + 0.10 \cdot Z\_{rec\_{TDs}} + 0.05 \cdot Z\_{receptions}
$$

$$
RB\_{Value\_{Above\_{Replacement}} = RB\_{Composite} - P\_{20}(RB\_{Composite})}
$$

$$
RB\_{Qualified\_{Season}} = \begin{cases} 
True & \text{if carries} \geq 50 \\
False & \text{otherwise}
\end{cases}
$$

## WR Composite Z-Score:

$$
WR\_{Composite} = 0.25 \cdot Z\_{rec\_{yds}} + 0.20 \cdot Z\_{rec\_{TDs}} + 0.15 \cdot Z\_{receptions} + 0.15 \cdot Z\_{catch\_{rate}} + 0.15 \cdot Z\_{YAC} + 0.10 \cdot Z\_{yds\_{per\_{rec}}}
$$

$$
WR\_{Value\_{Above\_{Replacement}} = WR\_{Composite} - P\_{20}(WR\_{Composite})}
$$

$$
WR\_{Qualified\_{Season}} = \begin{cases} 
True & \text{if receptions} \geq 30 \text{ OR targets} \geq 40 \\
False & \text{otherwise}
\end{cases}
$$

## TE Composite Z-Score:

$$
TE\_{Composite} = 0.25 \cdot Z\_{rec\_{yds}} + 0.20 \cdot Z\_{rec\_{TDs}} + 0.15 \cdot Z\_{receptions} + 0.15 \cdot Z\_{catch\_{rate}} + 0.15 \cdot Z\_{YAC} + 0.10 \cdot Z\_{yds\_{per\_{rec}}}
$$

$$
TE\_{Value\_{Above\_{Replacement}} = TE\_{Composite} - P\_{20}(TE\_{Composite})}
$$

$$
TE\_{Qualified\_{Season}} = \begin{cases} 
True & \text{if receptions} \geq 20 \text{ OR targets} \geq 30
False & \text{otherwise}
\end{cases}
$$