---
title: SHAPE (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHAPE
dev_langs:
- DMX
helpviewer_keywords:
- SHAPE statement
- multiple data sources
ms.assetid: b9526ec2-40bc-4bf5-b4e5-774f71075065
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dcd4940769fc52852b1d48feb453f1393c754084
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt---shape"></a>&lt;원본 데이터 쿼리와&gt; -셰이프
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  여러 데이터 원본으로부터 단일 계층 구조의 테이블(중첩 테이블이 있는 테이블)로 쿼리를 결합합니다. 이 테이블은 마이닝 모델의 사례 테이블이 됩니다.  
  
 전체 구문을 **셰이프** 명령에 설명 되어는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 데이터 Access Components (MDAC) 소프트웨어 개발 키트 (SDK).  
  
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
  
 *테이블 열 이름*  
 중첩 테이블의 부모 테이블에서 새로 추가된 열 이름  
  
## <a name="remarks"></a>주의  
 부모 테이블 및 자식 테이블에 관련되는 열을 기준으로 쿼리를 정렬해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 내에서 사용할 수 있습니다는 [INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md) 중첩된 테이블이 포함 된 모델을 학습 하는 문입니다. 내의 두 테이블에서 **셰이프** 문을 통해 관련 된 **OrderNumber** 열.  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>관련 항목:  
 [&#60; 원본 데이터 쿼리와 &#62;](../dmx/source-data-query.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

