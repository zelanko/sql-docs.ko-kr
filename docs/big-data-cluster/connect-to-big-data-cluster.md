---
title: 마스터에 연결 하 고 HDFS
titleSuffix: SQL Server big data clusters
description: SQL Server 마스터 인스턴스와 SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 위한 HDFS/Spark 게이트웨이 연결 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 245e88034194a01908b69d545deb9fa717c19a4a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782975"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Azure Data Studio에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 연결 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- 배포 된 [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)합니다.
- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **kubectl**

## <a id="master"></a> 클러스터에 연결

Azure Data Studio를 사용 하 여 빅 데이터 클러스터에 연결 하려면 클러스터의 마스터 SQL Server 인스턴스에 새 연결을 설정 합니다. 다음 단계를 사용 하 여 Azure Data Studio 마스터 인스턴스에 연결 하는 방법에 설명 합니다.

1. 명령줄에서 다음 명령 사용 하 여 마스터 인스턴스 IP를 찾습니다.

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 빅 데이터 클러스터 이름 기본값으로 **mssql 클러스터** 배포 구성 파일의 이름을 사용자 지정 하지 않으면. 자세한 내용은 [빅 데이터 클러스터에 대 한 배포 설정을 구성](deployment-custom-configuration.md#clustername)합니다.

1. Azure Data Studio 눌러 **F1** > **새 연결**합니다.

1. **연결 유형**를 선택 **Microsoft SQL Server**합니다.

1. SQL Server 마스터 인스턴스의 IP 주소를 입력 **서버 이름** (예: **\<IP 주소\>31433,** ).

1. SQL 로그인을 입력 **사용자 이름** 하 고 **암호**합니다.

   > [!TIP]
   > 기본적으로 사용자 이름이 **SA** 템플릿이며, 변경 하지 않는 한 암호를 **MSSQL_SA_PASSWORD** 배포 중에 사용 되는 환경 변수입니다.

1. 대상 변경 **데이터베이스 이름** 관계형 데이터베이스 중 하나에 있습니다.

   ![마스터 인스턴스에 연결](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 키를 눌러 **Connect**, 및 **Server 대시보드** 표시 되어야 합니다.

Azure Data Studio 2019 년 2 월 릴리스의 SQL Server 마스터 인스턴스에 연결할 있습니다 HDFS/Spark 게이트웨이와 상호 작용할 수 있습니다. 즉, HDFS 및 다음 섹션에서 설명 하는 Spark에 대 한 별도 연결을 사용할 필요가 없습니다.

- 개체 탐색기는 이제 새 포함 **Data Services** 노드를 마우스 오른쪽 단추 클릭 새 노트북을 만들거나 spark 작업을 제출 하는 빅 데이터 클러스터 작업을 지원 합니다. 
- 합니다 **Data Services** 포함는 **HDFS** HDFS 탐색 및 Notebook에서 외부 테이블 만들기 또는 분석 등의 작업 수행에 대 한 폴더입니다.
- **서버 대시보드** 에 연결에 대 한 탭에도 포함 되어 있습니다 **SQL Server 빅 데이터 클러스터** 하 고 **SQL Server 2019 (미리 보기)** 확장이 설치 되는 경우.

   ![Azure Data Studio 데이터 서비스 노드](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란](big-data-cluster-overview.md)합니다.