---
title: RStudio에서 사용 하 여 sparklyr
titleSuffix: SQL Server big data clusters
description: RStudio에서 sparklyr를 사용 하 여 빅 데이터 클러스터에 연결 합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8004146499bd8b17c7705f7558de075dfece5813
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994175"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에 사용 하 여 sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr은 Apache Spark에 대 한 R 인터페이스를 제공 합니다. Sparklyr은 Spark 사용 하 여 R 개발자를 위한 인기 있는 방법이 있습니다. 이 문서에서는 sparklyr RStudio를 사용 하 여 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 사용 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터를 배포](quickstart-big-data-cluster-deploy.md)합니다.

### <a name="install-rstudio-desktop"></a>RStudio Desktop 설치

설치 및 구성 **RStudio Desktop** 다음 단계를 사용 하 여:

1. Windows 클라이언트에서 실행 하는 경우 [다운로드 및 설치 R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4)합니다.

1. [다운로드 하 여 RStudio Desktop 설치](https://www.rstudio.com/products/rstudio/download/)합니다.

1. 설치가 완료 되 면 필요한 패키지를 설치 하려면 RStudio Desktop 내에서 다음 명령을 실행 합니다.

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>빅 데이터 클러스터에 Spark 연결

Livy 및 HDFS/Spark 게이트웨이 사용 하 여 빅 데이터 클러스터에 클라이언트에서 연결할 sparklyr을 사용할 수 있습니다. 

RStudio에서 R 스크립트를 만들고 다음 예제와 같이 Spark에 연결 합니다.

> [!TIP]
> 에 대 한 합니다 `<USERNAME>` 및 `<PASSWORD>` 사용자 이름 (예: 루트)를 사용 하는 값, 및 빅 데이터 클러스터 배포 중에 설정한 암호입니다. 에 대 한는 `<IP>` 하 고 `<PORT>` 설명서를 참조 하는 값을 [빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)합니다.

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

Spark에 연결한 후 sparklyr을 실행할 수 있습니다. 다음 예제에서는 sparklyr을 사용 하 여 iris 데이터 집합에서 쿼리를 수행 합니다.

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>분산된 된 R 계산

Sparklyr의 한 가지 기능은 수 있다는 [R 계산을 분배](https://spark.rstudio.com/guides/distributed-r/) 사용 하 여 [spark_apply](https://spark.rstudio.com/reference/spark_apply/)합니다.

Livy 연결을 사용 하는 빅 데이터 클러스터를 설정 해야 합니다 `packages = FALSE` 호출에서 **spark_apply**합니다. 자세한 내용은 참조는 [Livy 섹션](https://spark.rstudio.com/guides/distributed-r/#livy) 분산된 된 R 계산에 대 한 sparklyr 설명서의 합니다. 이 설정을 사용 하 여 사용할 수 있습니다에 전달 된 R 코드에서 Spark 클러스터에 이미 설치 된 R 패키지 **spark_apply**합니다. 다음 예제에서는이 기능을 보여 줍니다.

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터 이란](big-data-cluster-overview.md)합니다.
