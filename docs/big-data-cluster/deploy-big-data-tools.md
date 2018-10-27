---
title: Azure Data Studio를 사용 하 여 빅 데이터 클러스터를 SQL Server에 연결 | Microsoft Docs
description: Azure Data Studio를 사용 하 여 SQL Server 2019 빅 데이터 클러스터에 연결 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 18df937cfed15d7302a58267eb392a1933d73052
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643791"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Azure Data Studio를 사용 하 여 SQL Server 빅 데이터 클러스터에 연결

이 문서에서는 Azure Data Studio, SQL Server 2019 확장 (미리 보기)를 설치한 다음 빅 데이터 클러스터에 연결 하는 방법을 설명 합니다. 새 SQL Server 2019 확장에 대 한 미리 보기가 지원 됩니다 [SQL Server 2019 빅 데이터 클러스터](big-data-cluster-overview.md), 통합 된 [노트 환경과](notebooks-guidance.md), 및는 PolyBase [Create External Table 마법사](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-azure-data-studio"></a>Azure Data Studio를 설치 합니다.

Azure Data Studio를 설치 하려면 [Azure Data Studio의 최신 버전 다운로드 및 설치](../azure-data-studio/download.md)합니다.

## <a name="install-the-sql-server-2019-extension-preview"></a>SQL Server 2019 확장 (미리 보기) 설치

확장을 설치 하려면 [SQL Server 2019 확장 (미리 보기) 설치](../azure-data-studio/sql-server-2019-extension.md)합니다.

## <a name="connect-to-the-cluster"></a>클러스터에 연결

SQL Server에 연결할 수 있는 빅 데이터 클러스터에 연결할 때 [마스터 인스턴스](concept-master-instance.md) 또는 HDFS/Spark 게이트웨이. 다음 섹션에서는 각각에 연결 하는 방법을 보여 줍니다.

## <a id="master"></a> 마스터 인스턴스

1. Azure Data Studio 눌러 **F1** > **새 연결**합니다.

1. **연결 유형**를 선택 **Microsoft SQL Server**합니다.

1. SQL Server 마스터 인스턴스의 IP 주소를 입력 **서버 이름** (예:  **\<IP 주소\>31433,**).

1. SQL 로그인을 입력 **사용자 이름** 하 고 **암호**합니다.

1. 변경 된 **데이터베이스 이름** 에 **high_value_data** 데이터베이스.

   ![마스터 인스턴스에 연결](./media/deploy-big-data-tools/connect-to-cluster.png)

1. 키를 눌러 **Connect**, 및 **Server 대시보드** 표시 되어야 합니다.

## <a id="hdfs"></a> HDFS/Spark 게이트웨이

1. Azure Data Studio 눌러 **F1** > **새 연결**합니다.

1. **연결 유형**를 선택 **SQL Server 빅 데이터 클러스터**합니다.

1. 빅 데이터 클러스터의 IP 주소를 입력 **서버 이름**합니다.

1. 입력 `root` 에 대 한는 **사용자** 지정 합니다 **암호** 빅 데이터 클러스터에 있습니다.

   ![HDFS/Spark 게이트웨이에 연결](./media/deploy-big-data-tools/connect-to-cluster-hdfs-spark.png)

1. 키를 눌러 **Connect**, 및 **Server 대시보드** 표시 되어야 합니다.

## <a name="next-steps"></a>다음 단계

Azure Data Studio notebook을 실행 하려면 참조 [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.
