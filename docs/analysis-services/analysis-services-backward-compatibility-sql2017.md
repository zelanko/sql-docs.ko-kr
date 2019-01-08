---
title: SQL Server 2017 Analysis Services 이전 버전과 호환성 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29fb46b02e887ceebde293383fda99cbd3ed42be
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072430"
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Analysis Services 이전 버전과 호환성 (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

기능 가용성 및 현재 릴리스 및 이전 버전 간의 동작 변경 내용을 설명합니다.

## <a name="deprecated-features"></a>사용되지 않는 기능
A *사용 되지 않는 기능* 향후 릴리스에서 제품에서 중단 될 예정 이지만 여전히 지원 되 고 이전 버전과 호환성을 유지 하기 위해 현재 릴리스에서 포함 합니다. 신규 및 기존 프로젝트에서 사용 되지 않는 기능을 사용 하 여 향후 릴리스와도 호환을 유지 관리를 중단 하는 것이 좋습니다.

다음 기능은이 릴리스에서 사용 되지 않습니다.
  
|||  
|-|-|  
|**모드/범주**|**기능**|
|다차원|데이터 마이닝|
|다차원|원격으로 연결된 측정값 그룹|
|테이블 형식|모델 1100 및 1103 호환성 수준|
|테이블 형식|테이블 형식 개체 모델 속성: Column.TableDetailPosition, Column.IsDefaultLabel, Column.IsDefaultImage|
|Tools|추적 캡처용 SQL Server Profiler<br /><br /> SQL Server Management Studio에 포함된 확장 이벤트 프로파일러를 대신 사용할 수 있습니다.  <br /> [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)을 참조하세요.|  
|Tools|추적 재생용 Server Profiler <br />대체 기능 대체 기능은 없습니다.|  
|추적 관리 개체 및 추적 API|Analysis Services 추적 및 재생 개체용 API를 포함하는 Microsoft.AnalysisServices.Trace 개체. 다음과 같은 여러 부분을 대신 사용할 수 있습니다.<br /><br /> 추적 구성: Microsoft.SqlServer.Management.XEvent<br />추적 읽기: Microsoft.SqlServer.XEvent.Linq<br />추적 재생: 없음|  


## <a name="discontinued-features"></a>지원 되지 않는 기능
A *기능을 지원 되지 않는* 이전 릴리스에서 사용 되지 않았습니다. 계속 현재 릴리스에서 포함 될 수 있지만 더 이상 지원 되지. 지원 되지 않는 기능을 제거할 수 있습니다 완전히 이후에서 릴리스 또는 업데이트 합니다.

다음 이전 릴리스에서 사용 되지 않는 기능과이 릴리스에서 더 이상 지원 되지.
  
|||  
|-|-|  
|**모드/범주**|**기능**|  
|테이블 형식|VertipaqPagingPolicy 메모리 속성 값 (2) 메모리를 사용 하 여 디스크에 페이징 사용 매핑된 파일입니다.|
|다차원|원격 파티션|  
|다차원|원격으로 연결된 측정값 그룹|  
|다차원|차원 쓰기(writeback)|  
|다차원|연결된 차원|


## <a name="breaking-changes"></a>주요 변경 내용
A *주요 변경 내용* 기능, 데이터 모델, 응용 프로그램 코드 또는 스크립트가 더 이상 작동 현재 릴리스로 업그레이드 한 후에 발생 합니다.

이 릴리스에 주요 변경 내용이 없습니다.

## <a name="behavior-changes"></a>동작 변경 내용
A *동작 변경* 이전 릴리스에서 비교해 서 현재 릴리스의 동일한 기능을 작동 하는 방법에 영향을 줍니다. 중요 한 동작이 변경 내용만 설명 되어 있습니다. 변경 내용을 사용자 인터페이스에 포함 되지 않습니다.

MDSCHEMA_MEASUREGROUP_DIMENSIONS 및 DISCOVER_CALC_DEPENDENCY, 변경 내용에 자세히 설명 합니다 [Analysis Services 용 SQL Server 2017 CTP 2.1의 새로운 기능](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/) 알림.


## <a name="see-also"></a>참고자료
[Analysis Services 이전 버전과 호환성 (SQL Server 2016)](analysis-services-backward-compatibility.md)
