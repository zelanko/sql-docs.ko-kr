---
title: SHAPE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c928d4c96917479f8c37415d5ebe2db9b7f9eb98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938112"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;원본 데이터 쿼리&gt; -셰이프
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  여러 데이터 원본으로부터 단일 계층 구조의 테이블(중첩 테이블이 있는 테이블)로 쿼리를 결합합니다. 이 테이블은 마이닝 모델의 사례 테이블이 됩니다.  
  
 **SHAPE** 명령의 전체 구문은 MDAC ( [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 액세스 구성 요소) SDK (소프트웨어 개발 키트)에 설명 되어 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>인수  
 *마스터 쿼리*  
 부모 테이블을 반환하는 쿼리  
  
 *자식 테이블 쿼리*  
 중첩 테이블을 반환하는 쿼리  
  
 *마스터 열*  
 자식 테이블 쿼리 결과에서 자식 행을 식별하는 부모 테이블의 열  
  
 *자식 열*  
 master query 결과에서 부모 행을 식별하는 자식 테이블의 열  
  
 *열 테이블 이름*  
 중첩 테이블의 부모 테이블에서 새로 추가된 열 이름  
  
## <a name="remarks"></a>설명  
 부모 테이블 및 자식 테이블에 관련되는 열을 기준으로 쿼리를 정렬해야 합니다.  
  
## <a name="examples"></a>예  
 [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) 문 내에서 다음 예를 사용 하 여 중첩 테이블을 포함 하는 모델을 학습 시킬 수 있습니다. **SHAPE** 문 내의 두 테이블은 **ordernumber** 열을 통해 관련 됩니다.  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>참고 항목  
 [&#60;원본 데이터 쿼리&#62;](../dmx/source-data-query.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
