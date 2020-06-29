---
title: ADOMD.NET 서버 개체 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 33a8f420f985c9e62c7d7f275e7de370a6988e8d
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469058"
---
# <a name="adomdnet-server-object-architecture"></a>ADOMD.NET 서버 개체 아키텍처
  ADOMD.NET 서버 개체는에서 Udf (사용자 정의 함수) 또는 저장 프로시저를 만드는 데 사용할 수 있는 도우미 개체입니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  `Microsoft.AnalysisServices.AdomdServer` 네임스페이스 및 이러한 개체를 사용하려면 msmgdsrv.dll에 대한 참조를 UDF 프로젝트 또는 저장 프로시저에 추가해야 합니다.  
  
 ![ADOMD.NET 서버 개체 관계 표시](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "ADOMD.NET 서버 개체 관계 표시")  
ADOMD.NET 개체 모델  
  
 ADOMD.NET 개체 계층 구조와의 상호 작용은 일반적으로 다음 표에 설명된 최상위 레이어에 있는 하나 이상의 개체에서 시작됩니다.  
  
|대상|사용 개체|  
|--------|---------------------|  
|MDX(Multidimensional Expressions) 식 평가|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll AdomdServer](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) 개체는 MDX 식을 실행 하 고 지정 된 튜플에서 해당 식을 평가 하는 방법을 제공 합니다.|  
|전체 MDX 문을 생성하지 않고 MDX 함수를 실행할 수 있는 지원 제공|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))<br /> Microsoft.analysisservices.sharepoint.integration.dll 개체는 [AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) [개체를](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) 사용 하지 않고 미리 정의 된 mdx 함수를 호출 하는 데 편리 합니다. [Microsoft.analysisservices.sharepoint.integration.dll AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) 개체에 대 한 추가 함수는 이후 릴리스에서 사용할 수 있습니다.|  
|UDF의 현재 실행 컨텍스트 표현|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) 개체는 현재 큐브 또는 마이닝 모델과 같은 정보와 다양 한 메타 데이터 컬렉션을 제공 합니다. Microsoft.analysisservices.sharepoint.integration.dll 개체의 한 가지 주요 용도는 [AdomdServer](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) [개체의](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120)) [microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms137044(v=sql.120)) 개체를 사용 하는 것입니다 .이 속성은 UDF 또는 저장 프로시저의 작성자는 이 속성을 사용하여 쿼리가 실행되는 특정 차원의 멤버를 기준으로 결정을 내릴 수 있습니다.|  
|집합 및 튜플 만들기|[Microsoft.analysisservices.sharepoint.integration.dll AdomdServer](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)), [microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll AdomdServer](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)) 는 변경할 수 없는 집합을 만드는 방법을 제공 하는 반면 [microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120)) 는 변경할 수 없는 튜플을 만드는 방법을 제공 합니다.|  
|MDX 언어의 6가지 기본 유형 간의 암시적 변환 및 캐스트 지원|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120)) 개체는 다음 형식 간의 암시적 변환과 캐스트를 제공 합니다.<br /><br /> -   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143581(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143820(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms145330(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms144530(v=sql.120))<br />-스칼라 또는 값 형식|  
  
## <a name="see-also"></a>참고 항목  
 [ADOMD.NET 서버 프로그래밍](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
