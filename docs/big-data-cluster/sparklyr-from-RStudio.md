---
title: RStudio에서 사용 하 여 sparklyr
titleSuffix: SQL Server 2019 big data clusters
description: RStudio에서 sparklyr를 사용 하 여 빅 데이터 클러스터에 연결 합니다.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 83980f9d08a3894b0fbf7871cf899483e06702c4
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018359"
---
# <a name="use-sparklyr-in-sql-server-2019-big-data-cluster"></a>SQL Server 2019 빅 데이터 클러스터에서 사용 하 여 Sparklyr

Sparklyr은 Apache Spark에 대 한 R 인터페이스를 제공 합니다. Sparklyr는 Spark 사용 하 여 R 개발자를 위한 기본 방법입니다. 이 문서에서는 sparklyr RStudio를 사용 하 여 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 사용 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터를 배포](quickstart-big-data-cluster-deploy.md)합니다.
- [RStudio 설치](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>SS19 빅 데이터 클러스터에 spark 연결

RStudio는 RScript 만들고 다음과 같이 Spark를 연결 합니다. Spark의 빅 데이터 클러스터에 접근할 수 있는 Livy를 통해 연결 합니다 [HDFS/Spark 게이트웨이](connect-to-big-data-cluster.md#hdfs)합니다. 인증용 사용자 이름 및 배포 하는 동안 설정 된 암호를 사용 합니다.

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "***root***", password = "****")

httr::set_config(httr::config(ssl_verifypeer = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>Sparklyr 쿼리 실행

Spark에 연결한 후 sparklyr을 실행할 수 있습니다. 다음 예제에서는 sparklyr을 사용 하 여 iris 데이터 집합에서 쿼리를 수행 합니다.

``` r
copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.