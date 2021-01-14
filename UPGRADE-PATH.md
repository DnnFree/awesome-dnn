## DotNetNuke Suggested Upgrade Path

| FROM VERSION  | TO VERSION |
| ------------- | ------------- |
| 02.00.04 | 02.01.02 |
| 02.01.02 | 03.01.01 |
| 03.01.01 | 03.02.02 |
| 03.02.02 | 04.03.07 |
| 04.03.07 | 04.04.01 |
| 04.04.01 | 04.06.02 |
| 04.06.02 | 04.09.05 |
| 04.09.05 | 05.04.04 |
| 05.04.04 | 05.06.08 |
| 05.06.08 | 06.02.08 |
| 06.02.08 | [07.04.02](https://github.com/dnnsoftware/Dnn.Releases.Archive.7x/tree/master/07.04.02) |
| 07.04.02 | [08.00.04](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v8.0.4) |
| 08.00.04 | [09.01.01](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.1.1) |
| 09.01.01 | [09.03.02](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.3.2) |
| 09.03.02 | [09.08.00](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.8.0) |

**Notes** : 
- SolPartMenu been removed on DNN v8.0.4 (Remove any SolpartMenu from Containers should fix it)
- Framework Updates in v9.2.0+ [[link]](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.2.2)
  - Libraries updated to - jQuery 3.2.1, jQuery UI 1.12.1, Newtonsoft 10.0.3, Sharpzlib 0.86.0.518
  - Upgraded ClientDependency.Core to 1.9.3
  - Replaced 51 Degrees with local provider
  - Removed ~500 APIs deprecated prior to 7.0
  - New Integration Testing framework

ref : https://www.dnnsoftware.com/wiki/suggested-upgrade-path
