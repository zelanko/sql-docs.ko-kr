---
title: HDFS 사용 권한 복원
titleSuffix: SQL Server Big Data Cluster
description: TRestore HDFS 관리자 권한.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6d09921074ca2f2e386535baff5060620a7a3c8
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669378"
---
# <a name="restore-hdfs-permissions"></a>HDFS 사용 권한 복원

HDFS ACL(액세스 제어 목록)을 수정하면 HDFS의 `/system` 및 `/tmp` 폴더에 영향을 줄 수 있습니다. 가장 가능성이 높은 ACL 수정의 원인은 사용자가 폴더 ACL을 수동으로 조작하는 것입니다. /system 폴더 및 /tmp/logs 폴더에서 직접 권한을 수정할 수 없습니다.

## <a name="symptom"></a>증상

Spark 작업이 ADS를 통해 제출되며 SparkContext 초기화 오류 및 AccessControlException과 함께 실패합니다.

```
583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=<UserAccount>, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

Yarn UI가 애플리케이션 ID를 중단됨 상태로 표시합니다.

도메인 사용자로 폴더에 쓰려고 하는 경우에도 작업이 실패합니다. 다음 예제를 사용하여 테스트할 수 있습니다.

```bash
kinit <UserAccount>
hdfs dfs -touch /system/spark-events/test
hdfs dfs -rm /system/spark-events/test
```

## <a name="cause"></a>원인

BDC 사용자 도메인 보안 그룹에 대한 HDFS ACL이 수정되었습니다. /system 및/tmp 폴더에 대한 ACL이 수정되었을 수 있습니다. 이러한 폴더는 수정할 수 없습니다.

Livy 로그의 영향을 확인합니다.

```
INFO utils.LineBufferedStream: YYYY-MM-DD-HH:MM:SS,858 INFO yarn.Client: Application report for application_1580771254352_0041 (state: ACCEPTED)
...
WARN rsc.RSCClient: Client RPC channel closed unexpectedly.
INFO interactive.InteractiveSession: Failed to ping RSC driver for session <ID>. Killing application
```

YARN UI가 애플리케이션 ID를 중단됨 상태의 애플리케이션으로 표시합니다.

RPC 연결 닫기의 근본 원인을 확인하려면 애플리케이션에 해당하는 앱의 YARN 애플리케이션 로그를 확인합니다. 위의 예제에서는 `application_1580771254352_0041`입니다. `kubectl`을 사용하여 sparkhead-0 Pod에 연결하고 다음 명령을 실행합니다.

다음 명령은 애플리케이션의 YARN 로그를 쿼리합니다.

```bash
yarn logs -applicationId application_1580771254352_0041
```

아래 결과에서는 사용자의 권한이 거부되었습니다. 

```
YYYY-MM-DD-HH:MM:SS,583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=user1, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

BDC 사용자가 HDFS 루트 폴더에 재귀적으로 추가된 것이 원인일 수 있습니다. 이는 기본 권한에 영향을 미칠 수 있습니다.

## <a name="resolution"></a>해결 방법

다음 스크립트를 사용하여 권한을 복원합니다. 관리자 권한으로 `kinit`를 사용합니다.

```bash
hdfs dfs -chmod 733 /system/spark-events
hdfs dfs -setfacl --set default:user:sph:rwx,default:other::--- /system/spark-events
hdfs dfs -setfacl --set default:user:app-setup:r-x,default:other::--- /system/appdeploy
hadoop fs -chmod 733 /tmp/logs
hdfs dfs -setfacl --set default:user:yarn:rwx,default:other::--- /tmp/logs
```
