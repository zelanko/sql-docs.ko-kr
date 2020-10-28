---
title: SQL Server 빅 데이터 클러스터 HDFS 암호화 영역 사용 가이드
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 BDC의 SQL Server HDFS 암호화 영역 기능을 사용하는 방법을 보여 줍니다.
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 904b07913a63e226e5e45876f2fc520226411223
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199589"
---
# <a name="sql-server-big-data-clusters-hdfs-encryption-zones-usage-guide"></a>SQL Server 빅 데이터 클러스터 HDFS 암호화 영역 사용 가이드

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 가이드에서는 SQL Server 빅 데이터 클러스터의 미사용 데이터 암호화 기능을 통해 암호화 영역을 사용하여 HDFS 폴더를 암호화하는 방법을 보여 줍니다.

사용할 준비가 된 기본 암호화 영역이 이미 __```/securelake```__ 에 탑재되어 있습니다. 이 암호화 영역은 __securelakekey__ 라는 시스템 생성 256비트 키를 사용하여 생성되었습니다. 이 키를 추가 암호화 영역을 만드는 데 사용할 수 있습니다.

## <a name="prerequisites"></a><a id="prereqs"></a> 필수 조건

- Active Directory 통합이 포함된 [SQL Server 빅 데이터 클러스터 CU8+](release-notes-big-data-cluster.md).
- 관리자 권한이 있는 사용자.

## <a name="login-into-the-name-node"></a>이름 노드에 대한 로그인.

[Active Directory 연결 지침](active-directory-connect.md)을 사용하여 클러스터 로그인을 수행합니다. 이름 노드(nmnode-0-0)에 로그인하여 키 및 암호화 영역 명령을 실행합니다.

   ```console
   kubectl exec -it -c hadoop -n <cluster_namespace> nmnode-0-0 -- /bin/bash
   ```

## <a name="create-an-encryption-zone-using-the-provided-system-managed-key"></a>제공된 시스템 관리형 키를 사용하여 암호화 영역 만들기

1. HDFS 폴더 만들기

   ```console
   hdfs dfs -mkdir -p /user/zone/folder
   ```

1. __securelakekey__ 키를 사용하여 폴더를 암호화하는 암호화 영역 만들기 명령을 실행합니다.

   ```console
   hdfs crypto -createZone -keyName securelakekey -path /user/zone/folder
   ```

## <a name="create-a-custom-new-key-and-encryption-zone"></a>사용자 지정 새 키 및 암호화 영역 만들기

1. 다음 패턴을 사용하여 256비트 키를 생성합니다.

   ```console
   kinit hdfs
   hadoop key create mydatalakekey -size 256
   ```

1. 사용자 키를 사용하여 새 HDFS 경로를 만들고 암호화합니다.

   ```console
   hdfs dfs -mkdir -p /user/mydatalake
   hdfs crypto -createZone -keyName mydatalakekey -path /user/mydatalake
   ```
