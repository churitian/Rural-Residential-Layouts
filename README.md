# Rural Residential Layouts (RRL)

To systematically characterize the data composition and basic features of the Rural Residential Layouts (RRL) dataset, this repository provides statistics and descriptions from five aspects: graph-structured data organization, sample screening and cleaning, data sources, functional region distribution, and layout complexity.

## Graph Data Files

| File                   | Level       | Description                                                  |
| ---------------------- | ----------- | ------------------------------------------------------------ |
| `AttributeRoom.csv`    | Room        | Stores room-level attributes, including a unique index composed of the room ID and functional type, the functional type, area, and the center coordinates, width, and height of the bounding box. |
| `AttributeRegion.csv`  | Region      | Stores region-level attributes, including a unique index composed of the region ID and functional type, the functional type, area, and the center coordinates, width, and height of the bounding box. |
| `ConnectionRoom.csv`   | Room        | Stores connectivity relationships between room units established through door connections. |
| `ConnectionRegion.csv` | Region      | Stores connectivity relationships between region units established through door connections. |
| `affiliation.csv`      | Cross-level | Stores the cross-level affiliation relationships between room units and region units. |

`ConnectionRoom.csv` and `ConnectionRegion.csv` record the original connectivity relationships between spatial units, whereas the relationship edges used at the room and region levels in the model are reconstructed according to the relative distances and overlap between the bounding boxes of spatial units at the corresponding level.

Two types of relationships are considered:

- **Adjacency:** the gap between two BBoxes in either the horizontal or vertical direction is no greater than **2 px**, and their projected overlap in the other direction is greater than **0.5 px**.
- **Containment:** one BBox spatially contains the other in two dimensions.

## Data Screening and Cleaning

| Step                    | Criterion                         | Excluded samples | Remaining samples |
| ----------------------- | --------------------------------- | ---------------: | ----------------: |
| Initial collection      | —                                 |                — |              2912 |
| Room-type screening     | Undefined / extremely rare types  |               84 |              2828 |
| Quality inspection      | Incomplete / unreasonable layouts |              126 |              2702 |
| Near-duplicate removal  | mIoU > 0.87                       |               93 |              2609 |
| Region annotation check | Inconsistent region annotation    |               96 |              2513 |
| Final RRL               | —                                 |                — |          **2513** |

## Source Composition of the Final RRL Dataset

| Source category                         |         Samples |
| --------------------------------------- | --------------: |
| Team-collected / field survey materials |   1061 (42.22%) |
| Government rural housing atlases        |   1285 (51.13%) |
| Books and academic literature           |     167 (6.65%) |
| **Total**                               | **2513 (100%)** |

## Distribution of Functional Regions

| Number of regions |         Samples |
| ----------------- | --------------: |
| 1 region          |     212 (8.44%) |
| 2 regions         |   1329 (52.88%) |
| 3 regions         |    819 (32.59%) |
| 4 regions         |     153 (6.09%) |
| **Total**         | **2513 (100%)** |

## Layout Complexity Statistics

| Dataset | Mean number of rooms | Mean number of room types | Mean regions per sample | Mean rooms per region | Mean adjacency edges | Mean node degree |
| ------- | -------------------: | ------------------------: | ----------------------: | --------------------: | -------------------: | ---------------: |
| RRL     |                12.15 |                      9.20 |                    2.36 |                  5.14 |                23.01 |             3.79 |

## Data Availability

The data available for public release in this study have been organized in the `Rural Residential Layouts` folder, while some materials are not included in the public release due to copyright restrictions.
