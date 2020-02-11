---
title: 데이터 로드
description: Integration Services, bcp 유틸리티, dwloader 또는 SQL INSERT 문을 사용 하 여 SQL Server 병렬 데이터 웨어하우스 (PDW)에 데이터를 로드 하거나 삽입할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401044"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>병렬 데이터 웨어하우스로 데이터 로드
Integration Services, [Bcp 유틸리티](../tools/bcp-utility.md), **Dwloader** 명령줄 로더 또는 SQL insert 문을 사용 하 여 SQL Server 병렬 데이터 웨어하우스 (PDW)에 데이터를 로드 하거나 삽입할 수 있습니다.  

## <a name="loading-environment"></a>환경 로드 중  
데이터를 로드 하려면 로드 서버가 하나 이상 필요 합니다. 자신의 기존 ETL 또는 다른 서버를 사용 하거나 새 서버를 구입할 수 있습니다. 자세한 내용은 [로드 서버 가져오기 및 구성](acquire-and-configure-loading-server.md)을 참조 하세요. 이러한 지침에는 로딩을 위한 적절 한 솔루션을 계획 하는 데 도움이 되는 [로드 서버 용량 계획 워크시트가](loading-server-capacity-planning-worksheet.md) 포함 되어 있습니다.  
  
## <a name="load-with-dwloader"></a>Dwloader를 사용 하 여 로드  
[Dwloader 명령줄 로더](dwloader.md) 를 사용 하는 것은 데이터를 PDW로 로드 하는 가장 빠른 방법입니다.  
  
![프로세스 로드](media/loading-process.png "프로세스 로드")  
  
dwloader는 제어 노드를 통해 데이터를 전달 하지 않고 계산 노드에 직접 데이터를 로드 합니다. 데이터를 로드 하기 위해 dwloader는 먼저 제어 노드와 통신 하 여 계산 노드에 대 한 연락처 정보를 가져옵니다. dwloader는 각 계산 노드를 사용 하 여 통신 채널을 설정 하 고 라운드 로빈 방식으로 계산 노드에 256KB 데이터 청크를 보냅니다.  
  
각 계산 노드에서 DMS (데이터 이동 서비스)는 데이터 청크를 받아 처리 합니다. 데이터를 처리 하려면 각 행을 SQL Server 네이티브 형식으로 변환 하 고 배포 해시를 계산 하 여 각 행이 속한 계산 노드를 확인 합니다.  
  
행을 처리 한 후 DMS는 무작위 이동을 사용 하 여 각 행을 올바른 계산 노드와 SQL Server 인스턴스로 전송 합니다. 행을 받는 SQL Server는 dwloader에서 설정 된 **-b** 일괄 처리 크기 매개 변수에 따라 일괄 처리 한 다음 일괄 처리를 대량 로드 합니다.  

## <a name="load-with-prepared-statements"></a>준비 된 문을 사용 하 여 로드

준비 된 문을 사용 하 여 분산 및 복제 된 테이블로 데이터를 로드할 수 있습니다. 입력 데이터가 대상 데이터 형식과 일치 하지 않는 경우 암시적 변환이 수행 됩니다. PDW 준비 문에 의해 지원 되는 암시적 변환은 SQL Server에서 지 원하는 변환의 하위 집합입니다. 즉, 변환의 하위 집합만 지원 되지만, 지원 되는 변환 SQL Server 암시적 변환과 일치 합니다. 로드 될 대상 테이블이 분산 테이블 또는 복제 된 테이블로 정의 되는지에 관계 없이, 필요한 경우 대상 테이블에 있는 모든 열에 암시적 변환이 적용 됩니다. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>관련 작업  
  
|Task|Description|  
|--------|---------------|  
|준비 데이터베이스를 만듭니다.|[준비 데이터베이스 만들기](staging-database.md)|  
|Integration Services를 사용 하 여 로드 합니다.|[Integration Services를 사용하여 로드](load-with-ssis.md)|  
|Dwloader의 형식 변환을 이해 합니다.|[dwloader의 데이터 형식 변환 규칙](dwloader-data-type-conversion-rules.md)|  
|Dwloader를 사용 하 여 데이터를 로드 합니다.|[dwloader 명령줄 로더](dwloader.md)|  
|INSERT의 형식 변환을 이해 합니다.|[INSERT를 사용하여 데이터 로드](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
