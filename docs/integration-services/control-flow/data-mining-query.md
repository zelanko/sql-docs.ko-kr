---
title: "데이터 마이닝 쿼리 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8809f1e5f91ad5746b66d4640747b1ec0a923f0f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="data-mining-query"></a>데이터 마이닝 쿼리
  디자인 창에는 데이터 마이닝 예측 쿼리를 작성할 때 사용할 수 있는 데이터 마이닝 예측 쿼리 작성기가 포함되어 있습니다. 입력 테이블을 기반으로 하는 예측 쿼리를 디자인하거나 단일 예측 쿼리를 디자인할 수 있습니다. 쿼리를 실행하고 결과를 보려면 결과 뷰로 전환합니다. 쿼리 뷰에서는 예측 쿼리 작성기로 만든 DMX(Data Mining Extensions) 쿼리를 표시합니다.  
  
## <a name="options"></a>옵션  
 뷰 전환 단추  
 디자인 창과 쿼리 창 사이를 전환하려면 아이콘을 클릭합니다. 기본적으로 디자인 창이 열립니다.  
  
 디자인 창으로 전환 하려면는 ![디자인 아이콘](../../integration-services/control-flow/media/ssis-designicon.gif "디자인 아이콘") 아이콘입니다.  
  
 쿼리 창으로 전환 하려면는 ![SQL 아이콘](../../integration-services/control-flow/media/ssis-queryicon.gif "SQL 아이콘") 아이콘입니다.  
  
 **마이닝 모델**  
 예측의 기반으로 하려고 선택한 마이닝 모델을 표시합니다.  
  
 **모델 선택**  
 **마이닝 모델 선택** 대화 상자를 엽니다.  
  
 **입력 열**  
 예측 생성에 사용되는 선택한 입력 열을 표시합니다.  
  
 **원본**  
 열에 사용할 필드를 포함하는 원본을 드롭다운 목록에서 선택합니다. **마이닝 모델** 테이블에서 선택한 마이닝 모델, **입력 테이블 선택** 테이블에서 선택한 입력 테이블, 예측 함수 또는 사용자 지정 식을 사용할 수 있습니다.  
  
 마이닝 모델과 입력 열이 포함된 테이블에서 셀로 열을 끌 수 있습니다.  
  
 **필드**  
 원본 테이블에서 파생된 열 목록에서 열을 선택합니다. **원본** 에서 **예측 함수**를 선택한 경우 이 셀에는 선택한 마이닝 모델에 대해 사용할 수 있는 예측 함수의 드롭다운 목록이 포함됩니다.  
  
 **별칭**  
 서버에서 반환한 열의 이름입니다.  
  
 **표시**  
 열을 반환하거나 WHERE 절에서만 열을 사용하려면 선택합니다.  
  
 **그룹**  
 **및/또는** 열과 함께 사용하여 식을 그룹화할 수 있습니다. 예를 들어 (expr1 OR expr2) AND expr3과 같습니다.  
  
 **및/또는**  
 논리적 쿼리를 만드는 데 사용합니다. 예를 들어 (expr1 OR expr2) AND expr3과 같습니다.  
  
 **조건/인수**  
 열에 적용되는 조건 또는 사용자 식을 지정합니다. 마이닝 모델과 입력 열이 포함된 테이블에서 셀로 열을 끌 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 쿼리 도구](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  

