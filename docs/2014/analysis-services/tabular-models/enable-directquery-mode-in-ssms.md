---
title: 메모리 내 또는 테이블 형식 모델 데이터베이스에 대 한 DirectQuery 액세스 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c91dd8529fa6ddfb111ebb87cb84d87a55d3a709
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184575"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>테이블 형식 모델 데이터베이스에 대해 메모리 내 또는 DirectQuery 액세스 구성
  이 항목에서는 직접 쿼리 모드에서 모델을 사용할 수 있도록 이미 배포된 테이블 형식 모델의 연결 속성을 변경하는 방법에 대해 설명합니다.  
  
 이러한 속성 및 가장 일반적인 시나리오에 대 한 구성에 대 한 자세한 내용은 참조 [DirectQuery 배포 시나리오 &#40;SSAS 테이블 형식&#41;](../directquery-deployment-scenarios-ssas-tabular.md)합니다.  
  
## <a name="requirements"></a>요구 사항  
 테이블 형식 모델에서 직접 쿼리 모드를 사용하도록 설정하는 작업은 다단계 프로세스입니다. 다음을 수행해야 합니다.  
  
1.  모델에 직접 쿼리 모드에서 유효성 검사 오류를 일으킬 수 있는 기능이 없는지 확인  
  
2.  직접 쿼리를 지원하도록 모델의 저장소 모드 변경  
  
3.  하이브리드 또는 순수 직접 쿼리 모드에서 쿼리를 지원하는 모드로 모델 배포  
  
4.  직접 쿼리 모드를 지원하도록 배포된 데이터베이스의 연결 문자열 편집  
  
 이 항목에서는 모델을 만들고 유효성을 검사했으며 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]와 같은 클라이언트에서 직접 쿼리 액세스를 사용하도록 설정하기만 하면 되는 것으로 간주합니다.  
  
## <a name="procedure"></a>절차  
  
#### <a name="change-the-connection-string-properties-of-the-model"></a>모델의 연결 문자열 속성 변경  
  
1.  SQL Server Management Studio에서 모델을 배포한 인스턴스를 엽니다.  
  
2.  개체 탐색기에서 모델 데이터베이스 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  **DirectQueryMode**속성을 찾습니다. 관계형 데이터 원본을 사용하려면 이 속성을 다음 값 중 하나로 설정해야 합니다.  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  