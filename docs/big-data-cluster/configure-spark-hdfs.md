---
title: Apache Spark 및 Apache Hadoop
titleSuffix: Configure Apache Spark and Apache Hadoop in Big Data Clusters
description: SQL Server 빅 데이터 클러스터는 Spark 및 HDFS 솔루션을 허용합니다. 구성 방법에 대해 알아보세요.
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1e5d0941256fbb1e167f65489e250eed9c9b895a
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257223"
---
# <a name="configure-apache-spark-and-apache-hadoop-in-big-data-clusters"></a>빅 데이터 클러스터에서 Apache Spark 및 Apache Hadoop 구성

빅 데이터 클러스터에서 Apache Spark 및 Apache Hadoop을 구성하려면 배포 시 클러스터 프로필을 수정해야 합니다.

빅 데이터 클러스터에는 다음과 같은 네 가지 구성 범주가 있습니다. 

- `sql` 
- `hdfs` 
- `spark` 
- `gateway` 

`sql`, `hdfs`, `spark`, `sql`은 서비스입니다. 각 서비스는 동일한 이름의 구성 범주에 매핑됩니다. 모든 게이트웨이 구성은 범주 `gateway`로 이동합니다. 

예를 들어 서비스 `hdfs`의 모든 구성은 범주 `hdfs`에 속합니다. 모든 Hadoop(core-site), HDFS 및 Zookeeper 구성은 `hdfs` 범주에 속합니다. 모든 Livy, Spark, Yarn, Hive, 메타스토어 구성은 `spark` 범주에 속합니다. 

[지원되는 구성](reference-config-spark-hadoop.md#supported-configurations)에는 SQL Server 빅 데이터 클러스터를 배포할 때 구성할 수 있는 Apache Spark 및 Hadoop 속성이 나열되어 있습니다.

다음 섹션에는 클러스터에서 수정할 수 **없는** 속성이 나열되어 있습니다.

- [지원되지 않는 `spark` 구성](reference-config-spark-hadoop.md#unsupported-spark-configurations)
- [지원되지 않는 `hdfs` 구성](reference-config-spark-hadoop.md#unsupported-hdfs-configurations)
- [지원되지 않는 `gateway` 구성](reference-config-spark-hadoop.md#unsupported-gateway-configurations)


## <a name="configurations-via-cluster-profile"></a>클러스터 프로필을 통한 구성

클러스터 프로필에는 리소스와 서비스가 있습니다. 배포 시 다음과 같은 두 가지 방법 중 하나로 구성을 지정할 수 있습니다. 

* 첫째, 리소스 수준에서 다음을 수행합니다. 

   다음 예제는 프로필에 대한 패치 파일입니다. 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.zookeeper.spec.settings", 
         "value": { 
           "hdfs": { 
             "zoo-cfg.syncLimit": "6" 
           } 
         } 
   }
   ```

   또는 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.gateway.spec.settings", 
         "value": { 
           "gateway": { 
             "gateway-site.gateway.httpclient.socketTimeout": "95s" 
           } 
         } 
   } 
   ```

* 둘째, 서비스 수준에서 다음을 수행합니다. 서비스에 여러 리소스를 할당하고 서비스에 대한 구성을 지정합니다.

다음은 HDFS 블록 크기를 설정하기 위한 프로필 패치 파일의 예입니다. 

   ```json
   { 
         "op": "add", 
         "path": "spec.services.hdfs.settings", 
         "value": { 
           "hdfs-site.dfs.block.size": "268435456" 
        } 
   } 
   ```

서비스 `hdfs`는 다음과 같이 정의됩니다.

```json
{ 
  "spec": { 
   "services": { 
     "hdfs": { 
        "resources": [ 
          "nmnode-0", 
          "zookeeper", 
          "storage-0", 
          "sparkhead" 
        ], 
        "settings":{ 
          "hdfs-site.dfs.block.size": "268435456" 
        } 
      } 
    } 
  } 
} 
```
 
> [!NOTE]
> 리소스 수준 구성은 서비스 수준 구성을 재정의합니다. 하나의 리소스를 여러 서비스에 할당할 수 있습니다.

## <a name="enable-spark-in-the-storage-pool"></a>스토리지 풀에서 Spark 사용
지원되는 Apache 구성 외에도 Spark 작업을 스토리지 풀에서 실행할 수 있는지 여부를 구성하는 기능이 제공됩니다. 이 부울 값 `includeSpark`는 `spec.resources.storage-0.spec.settings.spark`의 `bdc.json` 구성 파일에 있습니다.

bdc.json의 예제 스토리지 풀 정의는 다음과 같습니다.
```json
...
"storage-0": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Storage",
                    "replicas": 2,
                    "settings": {
                        "spark": {
                            "includeSpark": "true"
                        }
                    }
                }
            }
```


## <a name="limitations"></a>제한 사항

구성은 범주 수준에서만 지정할 수 있습니다. 동일한 하위 범주를 사용하여 여러 구성을 지정하기 위해 클러스터 프로필에서 공통 접두사를 추출할 수 없습니다. 

```json
{ 
      "op": "add", 
      "path": "spec.services.hdfs.settings.core-site.hadoop", 
      "value": { 
        “proxyuser.xyz.users”: “*”, 
        “proxyuser.abc.users”: “*” 
     } 
} 
```

## <a name="next-steps"></a>다음 단계

- [Apache Spark 및 Apache Hadoop(HDFS) 구성 속성](reference-config-spark-hadoop.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 참조](../azdata/reference/reference-azdata.md)
- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)