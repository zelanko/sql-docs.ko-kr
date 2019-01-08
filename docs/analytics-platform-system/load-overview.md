---
title: Parallel Data Warehouse로 데이터 로드 | Microsoft Docs
description: 로드 하거나 Integration Services, bcp 유틸리티, dwloader, 또는 SQL INSERT 문을 사용 하 여 데이터를 SQL Server 병렬 데이터 웨어하우스 (PDW)를 삽입 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f4551f77b1348ece34dc87dc8abeb91e27290d00
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502141"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Parallel Data Warehouse로 데이터 로드
로드 하거나 Integration Services를 사용 하 여 데이터를 SQL Server 병렬 데이터 웨어하우스 (PDW)를 삽입할 수 있습니다 [bcp 유틸리티](../tools/bcp-utility.md)하십시오 **dwloader** 명령줄 로더 또는 SQL INSERT 문을 합니다.  

## <a name="loading-environment"></a>환경을 로딩  
데이터를 로드 하려면 하나 이상의 서버를 로드 해야 합니다. 사용자 고유의 기존 ETL 또는 다른 서버를 사용 하거나 새 서버를 구입할 수 있습니다. 자세한 내용은 [로드 서버 획득 및 구성](acquire-and-configure-loading-server.md)합니다. 이러한 지침에 포함 되어는 [서버 용량 계획 워크시트 로드](loading-server-capacity-planning-worksheet.md) 로드에 적합 한 솔루션을 계획할 수 있습니다.  
  
## <a name="load-with-dwloader"></a>Dwloader를 사용 하 여 로드  
사용 하 여 [dwloader 명령줄 로더](dwloader.md) PDW 데이터를 로드 하는 가장 빠른 방법은 합니다.  
  
![로드 프로세스](media/loading-process.png "로드 프로세스")  
  
dwloader는 컨트롤 노드를 통해 데이터를 전달 하지 않고 계산 노드로 직접 데이터를 로드 합니다. 데이터를 로드 하려면 dwloader 먼저 계산 노드에 대 한 연락처 정보를 가져올 컨트롤 노드를 사용 하 여 통신 합니다. dwloader 각 계산 노드를 사용 하 여 통신 채널을 설정 하 고 라운드 로빈 방식으로 계산 노드를 데이터의 크기는 256kb 청크를 전송 합니다.  
  
각 Compute 노드에 데이터 이동 서비스 (DMS) 수신 하 고 데이터의 청크를 처리 합니다. 데이터 처리를 SQL Server 네이티브 형식으로 각 행을 변환 하 고 각 행이 속해 있는 계산 노드를 확인 하려면 배포 해시 계산에 포함 되어 있습니다.  
  
DMS는 행을 처리 한 후 올바른 계산 노드와 SQL Server 인스턴스의 각 행을 전송할 순서 섞기 이동을 사용 합니다. SQL Server 행을 받으면 해당 일괄 처리에 따라 하는 **-b** dwloader, 배치 크기 매개 변수 설정 하 고 대량 로드 일괄 처리 합니다.  

## <a name="load-with-prepared-statements"></a>준비 된 문을 사용 하 여 로드

분산 되 고 복제 된 테이블로 데이터를 로드 하려면 준비 된 문을 사용할 수 있습니다. 입력된 데이터를 대상 데이터 형식에 맞지 않습니다, 경우에 암시적 변환이 수행 됩니다. 준비 된 문의 PDW에서 지원 되는 암시적 변환 이며 SQL Server에서 지 원하는 변환의 하위 집합 즉, 변환의 하위 집합만 지원 되지만 지원 되는 변환에는 암시적으로 SQL Server와 일치 합니다. 분산 또는 복제 된 테이블로 로드할 대상 테이블을 정의 하는지 여부에 관계 없이 암시적 변환은 필요한 경우 대상 테이블에 있는 모든 열에 적용 됩니다. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크|Description|  
|--------|---------------|  
|준비 데이터베이스를 만듭니다.|[준비 데이터베이스 만들기](staging-database.md)|  
|Integration Services를 사용 하 여 로드 합니다.|[Integration Services를 사용하여 로드](load-with-ssis.md)|  
|Dwloader의 형식 변환 이해 합니다.|[dwloader의 데이터 형식 변환 규칙](dwloader-data-type-conversion-rules.md)|  
|Dwloader 사용 하 여 데이터를 로드 합니다.|[dwloader 명령줄 로더](dwloader.md)|  
|삽입에 대 한 형식 변환 이해 합니다.|[INSERT를 사용하여 데이터 로드](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
