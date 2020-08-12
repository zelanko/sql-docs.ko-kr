---
title: '`pyspark` Notebook 문제 해결'
titleSuffix: SQL Server Big Data Cluster
description: '`pyspark` Notebook 문제 해결'
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mikeray
ms.date: 06/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2de422caf8567f1473d1436a27a094fef9144085
ms.sourcegitcommit: 7397706bbbc7296946e92ca9d4de93d4a5313c66
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206047"
---
# <a name="troubleshoot-pyspark-notebook"></a>`pyspark` Notebook 문제 해결

이 문서에서는 실패한 `pyspark` Notebook 문제를 해결하는 방법을 보여 줍니다.

## <a name="architecture-of-a-pyspark-job-under-azure-data-studio"></a>Azure Data Studio에서 PySpark 작업의 아키텍처

Azure Data Studio는 `livy` SQL Server BDC의 엔드포인트와 통신합니다. 

`livy` 엔드포인트는 BDC 클러스터 내에서 `spark-submit` 명령을 실행합니다. 각 `spark-submit` 명령에는 클러스터 리소스 관리자로 YARN을 지정하는 매개 변수가 있습니다.

PySpark 세션의 문제를 효율적으로 해결하기 위해 Livy, YARN, Spark 등 각 계층 내에서 로그를 수집하고 검토합니다.

이 문제 해결 단계를 수행하려면 다음이 필요합니다.

1. `azdata`가 설치되어 있고, 클러스터에 맞게 구성되어 있습니다.
2. 실행 중인 Linux 명령 및 일부 로그 문제 해결 기술을 잘 알고 있어야 합니다.

## <a name="troubleshooting-steps"></a>문제 해결 단계

1. `pyspark`에서 스택 및 오류 메시지를 검토합니다.

   Notebook의 첫 번째 셀에서 애플리케이션 ID를 가져옵니다. 이 애플리케이션 ID를 사용하여 `livy`, YARN 및 spark 로그를 조사합니다. `SparkContext`는 이 YARN 애플리케이션 ID를 사용합니다.

   :::image type="content" source="../big-data-cluster/media/troubleshoot-pyspark-notebook/1-failed-cell.png" alt-text="실패한 셀":::

1. 로그를 가져옵니다.

   `azdata bdc debug copy-logs`를 사용하여 조사합니다.

   다음 예에서는 빅 데이터 클러스터 엔드포인트를 연결하여 로그를 복사합니다. 실행하기 전에 예에서 다음 값을 업데이트합니다.
   - `<ip_address>`: 빅 데이터 클러스터 엔드포인트
   - `<username>`: 빅 데이터 클러스터 사용자 이름
   - `<namespace>`: 클러스터의 Kubernetes 네임스페이스
   - `<folder_to_copy_logs>`: 로그를 복사해 넣을 로컬 폴더 경로

   ```console
   azdata login --auth basic --username <username> --endpoint https://<ip_address>:30080
   azdata bdc debug copy-logs -n <namespace> -d <folder_to_copy_logs>
   ```

   예제 출력

   ```output
   <user>@<server>:~$ azdata bdc debug copy-logs -n <namespace> -d copy_logs
   Collecting the logs for cluster '<namespace>'.
   Collecting logs for containers...
   Creating an archive from logs-tmp/<namespace>.
   Log files are archived in /home/<user>/copy_logs/debuglogs-<namespace>-YYYYMMDD-HHMMSS.tar.gz.
   Creating an archive from logs-tmp/dumps.
   Log files are archived in /home/<user>/copy_logs/debuglogs-<namespace>-YYYYMMDD-HHMMSS-dumps.tar.gz.
   Collecting the logs for cluster 'kube-system'.
   Collecting logs for containers...
   Creating an archive from logs-tmp/kube-system.
   Log files are archived in /home/<user>/copy_logs/debuglogs-kube-system-YYYYMMDD-HHMMSS.tar.gz.
   Creating an archive from logs-tmp/dumps.
   Log files are archived in /home/<user>/copy_logs/debuglogs-kube-system-YYYYMMDD-HHMMSS-dumps.tar.gz.
   ```

1. Livy 로그를 검토합니다. Livy 로그는 `<namespace>\sparkhead-0\hadoop-livy-sparkhistory\supervisor\log`에 있습니다.

   - PySpark Notebook 첫 번째 셀에서 YARN 애플리케이션 ID를 검색합니다.
   - `ERR` 상태를 검색합니다.
   
   `YARN ACCEPTED` 상태가 있는 Livy 로그의 예입니다. Livy가 YARN 애플리케이션을 제출했습니다.

   ```output
   HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO impl.YarnClientImpl: Submitted application application_<application_id>
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO yarn.Client: Application report for application_<application_id> (state: ACCEPTED)
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO yarn.Client: 
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      client token: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      diagnostics: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      ApplicationMaster host: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      ApplicationMaster RPC port: -1
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      queue: default
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      start time: ############
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      final status: UNDEFINED
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      tracking URL: https://sparkhead-1.fnbm.corp:8090/proxy/application_<application_id>/
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      user: <account>
   ```

1. YARN UI 검토

   Azure Data Studio 빅 데이터 클러스터 관리 대시보드에서 YARN 엔드포인트 URL을 가져오거나 `azdata bdc endpoint list –o table`을 실행합니다.

   예를 들면 다음과 같습니다.

   ```console
   azdata bdc endpoint list -o table
   ```

   반환

   ```output
   Description                                             Endpoint                                                          Name                        Protocol
   ------------------------------------------------------  ----------------------------------------------------------------  --------------------------  ----------
   Gateway to access HDFS files, Spark                     https://knox.<namespace-value>.local:30443                               gateway                     https
   Spark Jobs Management and Monitoring Dashboard          https://knox.<namespace-value>.local:30443/gateway/default/sparkhistory  spark-history               https
   Spark Diagnostics and Monitoring Dashboard              https://knox.<namespace-value>.local:30443/gateway/default/yarn          yarn-ui                     https
   Application Proxy                                       https://proxy.<namespace-value>.local:30778                              app-proxy                   https
   Management Proxy                                        https://bdcmon.<namespace-value>.local:30777                             mgmtproxy                   https
   Log Search Dashboard                                    https://bdcmon.<namespace-value>.local:30777/kibana                      logsui                      https
   Metrics Dashboard                                       https://bdcmon.<namespace-value>.local:30777/grafana                     metricsui                   https
   Cluster Management Service                              https://bdcctl.<namespace-value>.local:30080                             controller                  https
   SQL Server Master Instance Front-End                    sqlmaster.<namespace-value>.local,31433                                  sql-server-master           tds
   SQL Server Master Readable Secondary Replicas           sqlsecondary.<namespace-value>.local,31436                               sql-server-master-readonly  tds
   HDFS File System Proxy                                  https://knox.<namespace-value>.local:30443/gateway/default/webhdfs/v1    webhdfs                     https
   Proxy for running Spark statements, jobs, applications  https://knox.<namespace-value>.local:30443/gateway/default/livy/v1       livy                        https
   ```

1. 애플리케이션 ID와 개별 application_master 및 컨테이너 로그를 확인합니다.

   :::image type="content" source="media/troubleshoot-pyspark-notebook/15-hadoop-dashboard.png" alt-text="애플리케이션 ID 확인":::

1. YARN 애플리케이션 로그를 검토합니다.

   앱의 애플리케이션 로그를 가져옵니다. `kubectl`을 사용하여 `sparkhead-0` Pod에 연결합니다. 예를 들면 다음과 같습니다.
   
   ```console
   kubectl exec -it sparkhead-0 -- /bin/bash
   ```
      
   그런 다음, 올바른 `application_id`를 사용하여 해당 셸에서 다음 명령을 실행합니다.

   ```console
   yarn logs -applicationId application_<application_id>
   ```

1. 오류 또는 스택을 검색합니다.

   hdfs에 대한 사용 권한 오류의 예입니다. java 스택에서 `Caused by:`를 찾습니다.

   ```output
   YYYY-MM-DD HH:MM:SS,MMM ERROR spark.SparkContext: Error initializing SparkContext.
   org.apache.hadoop.security.AccessControlException: Permission denied: user=<account>, access=WRITE, inode="/system/spark-events":sph:<bdc-admin>:drwxr-xr-x
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:399)
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:255)
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:193)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1852)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1836)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkAncestorAccess(FSDirectory.java:1795)
        at org.apache.hadoop.hdfs.server.namenode.FSDirWriteFileOp.resolvePathForStartFile(FSDirWriteFileOp.java:324)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.startFileInt(FSNamesystem.java:2504)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.startFileChecked(FSNamesystem.java:2448)
   
   Caused by: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.security.AccessControlException): Permission denied: user=<account>, access=WRITE, inode="/system/spark-events":sph:<bdc-admin>:drwxr-xr-x
   ```

1. SPARK UI를 검토합니다.

   :::image type="content" source="media/troubleshoot-pyspark-notebook/30-spark-ui.png" alt-text="Spark UI":::

   단계 작업을 드릴다운하여 오류를 찾습니다.

## <a name="next-steps"></a>다음 단계

[SQL Server 빅 데이터 클러스터 Active Directory 통합 문제 해결](troubleshoot-active-directory.md)