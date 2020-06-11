---
title: 다음 기능은 Excel 서비스에서 지원 되지 않으며 표시 되지 않거나 부분적 으로만 표시 될 수 있습니다. 주석, 셰이프 또는 기타 개체 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
author: minewiskan
ms.author: owend
ms.openlocfilehash: cd5f3da5eb53683e0c02655ad49bb36431d7e0b7
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547606"
---
# <a name="the-following-features-are-not-supported-by-excel-services-and-may-not-display-or-may-display-only-partially-comments-shapes-or-other-objects"></a>다음 기능은 브라우저에서 지원되지 않으며 표시되지 않거나 부분적으로만 표시될 수 있습니다. 메모, 도형 또는 기타 개체
  이 오류는 PowerPivot 필드 목록에서 PowerPivot 통합 문서에 슬라이서를 추가할 때 발생합니다.  
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|적용 대상|SharePoint용 PowerPivot|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|Excel Web Access가 PowerPivot 필드 목록에서 통합 문서에 추가된 슬라이서의 위치 지정 및 서식을 제어하는 데 사용되는 도형 개체를 렌더링할 수 없습니다.|  
|메시지 텍스트|다음 기능은 브라우저에서 지원되지 않으며 표시되지 않거나 부분적으로만 표시될 수 있습니다.<br /><br /> 메모, 도형 또는 기타 개체<br /><br /> 외부 데이터 쿼리와 같은 일부 기능은 Microsoft Excel 클라이언트 버전에서만 새로 고칠 수 있는 캐시된 데이터를 표시합니다.|  
  
## <a name="explanation"></a>설명  
 브라우저에서 PowerPivot 통합 문서를 열고 **지원 되지 않는 기능, 지원 되지 않는 기능**에 대 한 **세부 정보** 단추를 클릭 하면 Excel 웹 액세스에이 오류가 표시 됩니다.  
  
 이 오류가 발생하는 원인은 PowerPivot 통합 문서에 포함된 슬라이서의 레이아웃을 Excel의 숨겨진 도형 개체가 제어하기 때문입니다. 도형 개체는 가로 및 세로 배치 시 슬라이서의 위치 지정 및 서식을 제어합니다.  
  
 Excel 서비스에서는 도형 개체를 렌더링할 수 없지만 개체가 숨겨져 있으므로 이는 문제가 되지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류는 무시해도 됩니다. **확인** 을 클릭하여 오류 메시지를 닫고 통합 문서 및 슬라이서를 계속 사용해도 아무런 문제가 없습니다.  
  
  
