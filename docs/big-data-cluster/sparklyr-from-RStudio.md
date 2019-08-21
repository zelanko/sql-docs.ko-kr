---
title: RStudio에서 sparklyr 사용
titleSuffix: SQL Server big data clusters
description: RStudio에서 sparklyr를 사용 하 여 빅 데이터 클러스터에 연결 합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d23ce447f097d092059f7298ca5478ed6c3f19fc
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653328"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에서 sparklyr 사용

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr는 Apache Spark에 대 한 R 인터페이스를 제공 합니다. Sparklyr는 R 개발자가 Spark를 사용 하는 데 널리 사용 되는 방법입니다. 이 문서에서는 rstudio를 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 사용 하 여에서 sparklyr를 사용 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터를 배포](quickstart-big-data-cluster-deploy.md)합니다.

### <a name="install-rstudio-desktop"></a>RStudio Desktop 설치

다음 단계로 **Rstudio Desktop** 을 설치 하 고 구성 합니다.

1. Windows 클라이언트에서 실행 하는 경우 [R 3.4.4를 다운로드 하 여 설치](https://cran.rstudio.com/bin/windows/base/old/3.4.4)합니다.

1. [RStudio Desktop을 다운로드 하 여 설치](https://www.rstudio.com/products/rstudio/download/)합니다.

1. 설치가 완료 되 면 RStudio Desktop 내에서 다음 명령을 실행 하 여 필요한 패키지를 설치 합니다.

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>빅 데이터 클러스터의 Spark에 연결

Sparklyr를 사용 하 여 Livy 및 HDFS/Spark 게이트웨이를 사용 하 여 클라이언트에서 빅 데이터 클러스터에 연결할 수 있습니다. 

RStudio에서 R 스크립트를 만들고 다음 예제와 같이 Spark에 연결 합니다.

> [!TIP]
> `<USERNAME>` 및`<PASSWORD>` 값의 경우 빅 데이터 클러스터 배포 중에 설정한 사용자 이름 (예: root) 및 암호를 사용 합니다. `<IP>` 및`<PORT>` 값은 [빅 데이터 클러스터에 연결 하는 방법](connect-to-big-data-cluster.md)에 대 한 설명서를 참조 하세요.

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Sparklyr 쿼리 실행

Spark에 연결한 후 sparklyr을 실행할 수 있습니다. 다음 예에서는 sparklyr를 사용 하 여 iri 데이터 집합에 대 한 쿼리를 수행 합니다.

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>분산 R 계산

Sparklyr의 한 가지 기능은 [spark_apply](https://spark.rstudio.com/reference/spark_apply/)를 사용 하 여 [R 계산을 배포](https://spark.rstudio.com/guides/distributed-r/) 하는 기능입니다.

빅 데이터 클러스터는 Livy 연결을 사용 하기 때문에 `packages = FALSE` **spark_apply**에 대 한 호출에서를 설정 해야 합니다. 자세한 내용은 분산 R 계산에 대 한 sparklyr 설명서의 [Livy 섹션](https://spark.rstudio.com/guides/distributed-r/#livy) 을 참조 하세요. 이 설정을 사용 하면 **spark_apply**에 전달 된 r 코드에서 Spark 클러스터에 이미 설치 되어 있는 r 패키지만 사용할 수 있습니다. 다음 예제에서는이 기능을 보여 줍니다.

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [항목 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](big-data-cluster-overview.md)을 참조 하세요.
