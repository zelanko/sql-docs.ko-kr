---
title: RStudio의 sparklyr 사용
titleSuffix: SQL Server big data clusters
description: RStudio의 sparklyr를 사용하여 빅 데이터 클러스터에 연결합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 375993e4fd9506c129e4f98d9ad2193472e03edb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73531624"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에서 sparklyr를 사용합니다.

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr는 Apache Spark를 위한 R 인터페이스를 제공합니다. Sparklyr는 R 개발자가 Spark를 사용하는 데 널리 사용되는 방법입니다. 이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에서 RStudio를 사용하여 sparklyr를 사용하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터 배포](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>RStudio Desktop 설치

다음 단계에 따라 **RStudio Desktop**을 설치 및 구성합니다.

1. Windows 클라이언트에서 실행 중인 경우 [R 3.4.4를 다운로드하여 설치합니다](https://cran.rstudio.com/bin/windows/base/old/3.4.4).

1. [RStudio Desktop을 다운로드하여 설치합니다](https://www.rstudio.com/products/rstudio/download/).

1. 설치가 완료되면 RStudio Desktop에서 다음 명령을 실행하여 필수 패키지를 설치합니다.

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>빅 데이터 클러스터에서 Spark에 연결

sparklyr를 사용하여, Livy 및 HDFS/Spark 게이트웨이를 사용하여 클라이언트에서 빅 데이터 클러스터에 연결할 수 있습니다. 

RStudio에서 다음 예제처럼 R 스크립트를 만들고 Spark에 연결합니다.

> [!TIP]
> `<AZDATA_USERNAME>` 및 `<AZDATA_PASSWORD>` 값의 경우, 빅 데이터 클러스터 배포 중에 설정한 사용자 이름(예: root)과 암호를 사용하세요. `<IP>` 및 `<PORT>` 값의 경우, [빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)에 관해 설명하는 설명서를 참조하세요.

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<AZDATA_USERNAME>", password = "<AZDATA_PASSWORD>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>sparklyr 쿼리 실행

Spark에 연결했다면 sparklyr를 실행할 수 있습니다. 다음 예제에서는 sparklyr를 사용하여 iris 데이터 세트를 대상으로 쿼리를 실행합니다.

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>분산 R 계산

sparklyr의 기능 중 하나는 [spark_apply](https://spark.rstudio.com/reference/spark_apply/)를 사용하여 [R 계산을 분산](https://spark.rstudio.com/guides/distributed-r/)하는 것입니다.

빅 데이터 클러스터는 Livy 연결을 사용하므로 **spark_apply**를 호출할 때 `packages = FALSE`를 설정해야 합니다. 자세한 내용은 분산 R 계산에 대한 sparklyr 설명서에서 [Livy 섹션](https://spark.rstudio.com/guides/distributed-r/#livy)을 참조하세요. 이렇게 설정하면 **spark_apply**로 전달한 R 코드에서 Spark 클러스터에 이미 설치한 R 패키지만 사용할 수 있습니다. 다음 예제에서 이 기능을 보여 줍니다.

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
