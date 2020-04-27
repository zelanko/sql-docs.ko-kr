---
title: 데이터베이스 속성(쿼리 저장소 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 51116c993cf795e6390ac463f67f75e2ddff3e0e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917214"
---
# <a name="database-properties-query-store-page"></a>데이터베이스 속성(쿼리 저장소 페이지)
  이 페이지는 주 데이터베이스에서 액세스하며 데이터베이스 쿼리 저장소의 속성을 구성하고 수정하는 데 사용합니다. [ALTER DATABASE SET 옵션](/sql/t-sql/statements/alter-database-transact-sql-set-options)을 사용하여 이러한 옵션을 구성할 수도 있습니다. 쿼리 저장소에 대한 자세한 내용은 [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md)을 참조하세요.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="options"></a>옵션  
 사용  
 쿼리 저장소를 사용하거나 사용하지 않도록 설정합니다.  
  
 작업 모드  
 유효한 값은 READ_ONLY 및 READ_WRITE입니다. READ_WRITE 모드에서 쿼리 저장소는  쿼리 계획 및 런타임 실행 통계 정보를 수집하고 유지합니다. READ_ONLY 모드에서는 쿼리 저장소에서 정보를 읽을 수 있지만 새 정보는 추가되지 않습니다. 쿼리 저장소의 최대 할당 공간이 모두 사용되면 쿼리 저장소는 작업 모드를 READ_ONLY로 변경합니다.  
  
 작업 모드(실제)  
 쿼리 저장소의 작업 모드를 가져옵니다.  
  
 작업 모드(요청)  
 쿼리 저장소의 원하는 작업 모드를 가져오거나 설정합니다.  
  
 데이터 플러시 간격(분)  
 쿼리 저장소에 기록된 데이터가 디스크에 유지되는 빈도를 결정합니다. 성능 최적화를 위해 쿼리 저장소에서 수집한 데이터는 디스크에 비동기적으로 기록됩니다. 이 비동기 전송이 발생되는 빈도가 구성됩니다.  
  
 통계 수집 간격  
 통계 수집 간격 값을 가져오거나 설정합니다.  
  
 최대 크기(MB)  
 쿼리 저장소에 할당된 총 공간을 가져오거나 설정합니다.  
  
 오래된 쿼리 임계값(일)  
 오래된 쿼리 임계값을 가져오거나 설정합니다. STALE_QUERY_THRESHOLD_DAYS 인수를 구성하여 쿼리 저장소에 데이터를 보존할 일수를 지정합니다.  
  
 쿼리 데이터 삭제  
 쿼리 저장소의 내용을 제거합니다.  
  
 원형 차트  
 왼쪽 차트에는 디스크의 총 데이터베이스 파일 사용 및 쿼리 저장소 데이터로 채워진 파일 부분이 표시됩니다.  
  
 오른쪽 차트에는 현재 사용된 쿼리 저장소 할당량 부분이 표시됩니다. 왼쪽 차트에는 할당량이 표시되지 않습니다. 할당량이 데이터베이스의 현재 크기를 초과할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 쿼리 저장소 기능을 통해 DBA는 쿼리 계획 선택 및 성능에 대한 정보를 얻을 수 있습니다. 쿼리 계획 변경으로 인해 발생하는 성능 차이를 신속하게 찾을 수 있도록 하여 성능 문제 해결을 간소화합니다. 이 기능은 쿼리, 계획 및 런타임 통계의 기록을 자동으로 캡처하고 검토할 수 있도록 이 기록을 유지합니다. 데이터를 기간별로 구분하여 데이터베이스 사용 패턴을 파악하고 서버에서 쿼리 계획 변경이 발생한 시기를 이해할 수 있게 해줍니다. 쿼리 저장소는 이 쿼리 저장소 데이터베이스 속성 페이지를 사용하거나 [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) 옵션을 사용하여 구성할 수 있습니다. 쿼리 저장소는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 대화 상자를 사용하여 정보를 표시합니다. 쿼리 저장소에 대한 자세한 내용은 [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 쿼리 저장소](/sql/relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/query-store-catalog-views-transact-sql)  
  
  
