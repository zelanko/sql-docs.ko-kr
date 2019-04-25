---
title: 필터 연산자(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 27914c8b-8951-4b7d-914d-1cbf528dd248
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 36e7784eb1725505a00225d237d5016945f5f7c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62516880"
---
# <a name="filter-operators-master-data-services"></a>필터 연산자(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  멤버 목록을 필터링할 때 다음과 같은 연산자를 사용할 수 있습니다.  
  
> [!NOTE]  
>  여러 조건을 기준으로 필터링하는 경우 모든 조건이 true여야 결과가 반환됩니다. 예를 들면 SquareFeet = 2000 **AND** Division <> 123 같은 경우입니다.  
  
## <a name="filter-operators"></a>필터 연산자  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**같음**|지정된 조건과 정확히 같은 특성 값을 반환합니다. 예를 들어 **Mountain-100**을 필터링하려면 **Mountain-100**을 입력해야 합니다.|  
|**같지 않음**|지정된 조건과 같지 않은 특성 값을 반환합니다. 필터 조건은 결과에서 생략할 특성 값과 정확히 같아야 합니다. 예를 들어 **Mountain-100**과 일치하는 결과를 생략하려면 **Mountain-100**을 입력해야 합니다.<br /><br /> <br /><br /> 참고: "Is not equal" 절을 사용하여 특성에 필터 조건을 적용하면 특성이 NULL인 멤버가 필터 조건을 전달하고 SET ANSI_NULLS가 데이터베이스 문자열에서 ON으로 설정된 경우 결과가 반환됩니다. 이 동작을 중지하려면 데이터베이스 설정에서 SET ANSI_NULLS를 OFF로 설정합니다. SET ANSI_NULLS가 OFF로 설정된 경우 데이터 값이 Null이면 Null 값에 대한 모든 데이터 비교가 TRUE로 평가되고 멤버가 "Is not equal" 절을 전달하지 않는 결과가 발생합니다. 자세한 내용은 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.|  
|**유사함**|Transact-SQL에서 LIKE 연산자를 사용하여 결과를 필터링합니다. 자세한 내용은 SQL Server 온라인 설명서에서 [LIKE&#40;Transact-SQL&#41;](../t-sql/language-elements/like-transact-sql.md)를 참조하세요.|  
|**유사하지 않음**|Transact-SQL에서 NOT 연산자를 사용하여 결과를 필터링합니다. 자세한 내용은 SQL Server 온라인 설명서에서 [NOT&#40;Transact-SQL&#41;](../t-sql/language-elements/not-transact-sql.md)을 참조하세요.|  
|**보다 큼**|지정된 조건보다 큰 특성 값을 반환합니다. 예를 들어 **F**보다 큰 문자로 시작하는 특성 값을 반환하려면 **F**를 입력합니다.|  
|**보다 작음**|지정된 조건보다 작은 특성 값을 반환합니다. 예를 들어 **F**보다 작은 문자로 시작하는 특성 값을 반환하려면 **F**를 입력합니다.|  
|**크거나 같음**|지정된 조건보다 크거나 같은 특성 값을 반환합니다. 예를 들어 **3** 이상의 숫자로 시작하는 특성 값을 반환하려면 **3**을 입력합니다.|  
|**작거나 같음**|지정된 조건보다 작거나 같은 특성 값을 반환합니다. 예를 들어 **3** 이하의 숫자로 시작하는 특성 값을 반환하려면 **3**을 입력합니다.|  
|**일치**|유사 항목 조회 인덱스를 사용하여 결과를 필터링합니다.<br /><br /> **유사성 수준** 필드를 사용하여 특성 값이 지정된 필터 조건과 어느 정도 일치해야 하는지 지정할 수 있습니다(기본값 30%).<br /><br /> **알고리즘** 목록 상자에서 다음 중 하나를 선택합니다.<br /><br /> **Levenshtein**: 편집 횟수를 기반으로 하는 거리 (예를 들어, 추가 또는 삭제)을 다른 문자열는 합니다. 기본값입니다. 추가 매개 변수는 필요하지 않습니다.<br /><br /> **Jaccard**: 여러 문자열을 비교할 때 가장 잘 작동 하는 인덱스입니다. 이 검색에서는 제약 편차의 추가 매개 변수가 지원됩니다(아래 참조).<br /><br /> **Jaro-Winkler**: 중복 된 사용자 이름을 찾는 가장 많이 사용 되는 거리입니다. 이 방법은 다른 방법보다 많은 결과를 반환합니다. 제약 편차는 지원하지 않습니다.<br /><br /> **최장 공통 하위 시퀀스**: 패턴의 문자가 구분되어 있을 수 있더라도 순서대로 표시되는 하위 시퀀스에 따라 작동합니다(예: "MSR"은 "MaSteR"의 하위 시퀀스임). 이 검색에서는 제약 편차의 추가 매개 변수가 지원됩니다(아래 참조).<br /><br /> <br /><br /> 참고: **Jaccard** 또는 **최장 공통 하위 시퀀스** 알고리즘의 경우 **제약 편차**를 추가합니다. 0과 1 사이의 소수 백분율로 제공되는 길이 임계값입니다(기본값 .62). 임계값이 낮으면 반환 가능한 일치 항목 수가 늘어납니다.|  
|**일치하지 않음**|유사 항목 조회 인덱스를 사용하여 결과를 필터링합니다. **유사성 수준** 필드를 사용하여 특성 값이 지정된 필터 조건과 어느 정도 일치하지 않아야 하는지 지정할 수 있습니다.|  
|**패턴 포함**|.NET Framework 정규식을 사용하여 지정된 패턴에 대한 결과를 필터링합니다. 정규식에 대한 자세한 내용은 MSDN Library의 [정규식 언어 요소](https://go.microsoft.com/fwlink/?LinkId=164401) 를 참조하십시오.|  
|**패턴을 포함하지 않음**|.NET Framework 정규식을 사용하여 지정된 패턴과 일치하지 않는 결과를 필터링합니다. 정규식에 대한 자세한 내용은 MSDN Library의 [정규식 언어 요소](https://go.microsoft.com/fwlink/?LinkId=164401) 를 참조하십시오.|  
|**NULL**|Null인 특성 값을 반환합니다. **NULL** 연산자를 선택한 경우에는 **조건** 필드가 비활성화됩니다.|  
|**NULL이 아님**|Null이 아닌 특성 값을 반환합니다. **NULL이 아님** 연산자를 선택한 경우에는 **조건** 필드가 비활성화됩니다.|  
  
  
