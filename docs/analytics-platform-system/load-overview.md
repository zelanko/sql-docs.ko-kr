---
title: 로드
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 로드 하거나 Integration Services, bcp 유틸리티, dwloader, 또는 SQL INSERT 문을 사용 하 여 데이터를 SQL Server 병렬 데이터 웨어하우스 (PDW)를 삽입할 수 있습니다.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c7292108-4a48-409e-b0f4-e4ba84dce26f
caps.latest.revision: 22
ms.openlocfilehash: 77bb7e3ba6a3377fe63decf06a872872eaa4ee61
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="load-sql-server-pdw"></a>부하 (SQL Server PDW)
로드 하거나 Integration Services를 사용 하 여 데이터를 SQL Server 병렬 데이터 웨어하우스 (PDW)을 삽입 하려면 [bcp 유틸리티](../tools/bcp-utility.md), **dwloader** 명령줄 로더 또는 SQL INSERT 문을 합니다.  

## <a name="loading-environment"></a>환경에 로드  
데이터를 로드 하려면 하나 이상의 서버를 로드 해야 합니다. 사용자 고유의 기존 ETL 또는 다른 서버를 사용할 수 있습니다 또는 새 서버를 구매할 수 있습니다. 자세한 내용은 참조 [를 획득 하 고 로드 하는 서버를 구성](acquire-and-configure-loading-server.md)합니다. 이러한 지침에는 한 [서버 용량 계획 워크시트 로드](loading-server-capacity-planning-worksheet.md) 로드에 대 한 적합 한 솔루션을 계획할 수 있도록 합니다.  
  
## <a name="load-with-dwloader"></a>Dwloader 함께 로드  
사용 하는 [dwloader 명령줄 로더](dwloader.md) 는 가장 빠른 방법은 PDW에 데이터를 로드 합니다.  
  
![로드 프로세스](media/loading-process.png "로드 프로세스")  
  
dwloader 제어 노드를 통해 데이터를 전달 하지 않고 계산 노드에 직접 데이터를 로드 합니다. 데이터를 로드 하려면 dwloader 먼저 계산 노드에 대 한 연락처 정보를 얻으려면는 제어 노드에와 통신 합니다. dwloader 각 계산 노드가 함께 통신 채널을 설정 하 고에 라운드 로빈 방식으로 계산 노드 256KB 데이터 청크를 보냅니다.  
  
각 계산 노드의 데이터 이동 서비스 (DMS) 받아 데이터의 청크를 처리 합니다. 데이터 처리 각 행을 SQL Server 네이티브 형식으로 변환 하 고 각 행이 속한 계산 노드를 확인 하려면 배포 해시 계산에 포함 됩니다.  
  
행을 처리 한 후 DMS 순서 섞기 이동을 사용 하 여 올바른 계산 노드 및 SQL Server의 인스턴스를 각 행을 전송 하도록 합니다. SQL Server가 행에 해당 일괄 처리에 따라 이러한는 **– b** dwloader에 배치 크기 매개 변수 설정 하 고 대량 일괄 처리를 로드 합니다.  

## <a name="load-with-prepared-statements"></a>준비 된 문과 함께 로드

데이터 분산 되 고 복제 된 테이블에 로드 하는 준비 된 문을 사용할 수 있습니다. 입력된 데이터는 대상 데이터 형식과 일치 하지 않습니다, 암시적 변환이 수행 됩니다. 암시적 변환 준비 된 문의 PDW에서 지원 되는 SQL Server에서 지 원하는 변환의 하위 집합입니다. 즉, 변환의 하위 집합만 사용할 수 있지만 지원 되는 변환은 암시적 변환은 SQL Server와 일치 합니다. 분산 또는 복제 된 테이블로 로드할 대상 테이블은 정의 여부에 관계 없이 암시적으로 변환할이 필요한 경우 대상 테이블에 있는 모든 열에 적용 됩니다. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크|Description|  
|--------|---------------|  
|준비 데이터베이스를 만듭니다.|[준비 데이터베이스 만들기](staging-database.md)|  
|Integration Services와 함께 로드 합니다.|[Integration Services를 사용하여 로드](load-with-ssis.md)|  
|Dwloader에 대 한 형식 변환 이해 합니다.|[dwloader의 데이터 형식 변환 규칙](dwloader-data-type-conversion-rules.md)|  
|Dwloader 사용 하 여 데이터를 로드 합니다.|[dwloader 명령줄 로더](dwloader.md)|  
|삽입에 대 한 형식 변환 이해 합니다.|[INSERT를 사용하여 데이터 로드](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
