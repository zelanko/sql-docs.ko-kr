---
title: SELECT FROM &lt;구조&gt;합니다. 경우 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 65ab4d5ebf1fbe64d3e85854df186d9ebe098e84
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600063"
---
# <a name="select-from-ltstructuregtcases"></a>SELECT FROM &lt;구조&gt;합니다. 경우
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  마이닝 구조를 만드는 데 사용된 사례를 반환합니다.  
  
 구조에 드릴스루가 사용되도록 설정되지 않은 경우에는 문이 실패합니다. 또한 사용자에게 마이닝 구조에 대한 드릴스루 권한이 없는 경우에도 문은 실패합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 기본적으로 새 마이닝 구조에 드릴스루를 사용 합니다. 특정 구조에 드릴스루를 사용할 수 있는지 여부를 확인 하려면 확인 여부를 값을 **CacheMode** 속성이 **KeepTrainingCases**합니다.  
  
 경우 값 **CacheMode** 으로 변경 됩니다 **ClearAfterProcessing**, 구조 사례는 캐시에서 지워지고 드릴스루를 사용할 수 없습니다.  
  
> [!NOTE]  
>  DMX(Data Mining Extensions)를 사용하여 마이닝 구조에 대해 드릴스루를 사용하거나 사용하지 않도록 설정할 수는 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 선택 사항입니다. 반환할 행의 수를 지정하는 정수입니다.  
  
 *식 목록*  
 쉼표로 구분된 식 목록입니다.  
  
 식은 열 식별자, 사용자 정의 함수 및 VBA 함수를 포함할 수 있습니다.  
  
 *구조*  
 구조의 이름입니다.  
  
 *조건 식*  
 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 선택 사항입니다. 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>Remarks  
 모델과 구조 모두에 드릴스루가 사용되도록 설정되어 있으면 마이닝 구조 및 모델에 대해 드릴스루 권한을 가지는 역할의 모든 멤버는 다음 구문을 사용하여 모델에 포함되지 않은 구조 열을 반환할 수 있습니다.  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 따라서 중요 한 데이터 나 개인 정보를 보호 하려면 구성 않아야 개인 정보를 마스킹 권한을 부여 하 여 데이터 원본 뷰 **AllowDrillthrough** 마이닝 구조 또는 마이닝 모델에 대 한 권한이 경우에만 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 마이닝 구조를 기반으로 하는 타겟 메일링 기반한는 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터베이스와 연결 된 마이닝 모델입니다. 자세한 내용은 [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다.  
  
### <a name="example-1-drill-through-to-structure-cases"></a>예제 1: 구조 사례로 드릴스루  
 다음 예에서는 마이닝 구조인 대상 메일에서 가장 오래된 500명의 고객 목록을 반환합니다. 이 쿼리는 마이닝 모델에 있는 모든 열을 반환하지만 자전거를 구입한 고객의 행으로 행을 제한하고 이러한 행을 고객의 나이별로 정렬합니다. 식 목록을 편집하여 필요한 열만 반환할 수도 있습니다.  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>예제 2: 테스트 또는 학습 사례로 드릴스루  
 다음 예에서는 테스트용으로 예약된 대상 메일에 대한 구조 사례 목록을 반환합니다. 마이닝 구조에 홀드아웃 테스트 집합이 포함되지 않은 경우에는 기본적으로 모든 사례가 학습 사례로 취급되고 이 쿼리는 0개의 사례를 반환합니다.  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 학습 사례를 반환하려면 `IsTrainingCase()` 함수를 대체합니다.  
  
## <a name="see-also"></a>관련 항목  
 [선택 &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
