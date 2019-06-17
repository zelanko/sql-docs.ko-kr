---
title: 특성 관계를 정의 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47a46bfd482463de2377470cd11186bd3bfbd5db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077059"
---
# <a name="define-attribute-relationships"></a>특성 관계 정의
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 특성은 차원의 기본 구성 요소입니다. 차원은 특성 관계를 기반으로 구성되는 특성 집합을 포함합니다.  
  
 차원에 포함된 테이블마다 테이블의 키 특성을 해당 테이블의 다른 특성과 연결하는 특성 관계가 있습니다. 이 관계는 차원을 만들 때 만들 수 있습니다.  
  
 특성 관계의 이점은 다음과 같습니다.  
  
-   차원 처리에 필요한 메모리 양이 줄어듭니다. 따라서 차원, 파티션 및 쿼리 처리가 빨라집니다.  
  
-   스토리지 액세스가 보다 빨라지고 실행 계획이 보다 최적화되므로 쿼리 성능이 향상됩니다.  
  
-   사용자 정의 계층이 관계 경로에 정의된 경우 집계 디자인 알고리즘에 따라 보다 효율적인 집계를 선택할 수 있습니다.  
  
    > [!NOTE]  
    >  중요 성과 의미를 정의 하 고 특성 관계를 구성 하는 방법에 대 한 자세한 내용은 섹션을 참조 "쿼리 성능 향상"에 [SQL Server 2005 Analysis Services 성능 가이드](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)합니다.  
  
## <a name="attribute-relationship-considerations"></a>특성 관계 고려 사항  
 기본 데이터가 특성 관계를 지원하는 경우 특성 간의 고유한 특성 관계도 정의해야 합니다. 고유한 특성 관계를 정의하려면 차원 디자이너의 **특성 관계** 탭을 사용하십시오.  
  
 나가는 관계가 있는 특성에는 관련 특성에 대한 고유 키가 있어야 합니다. 즉, 원본 특성의 멤버는 관련 특성의 멤버를 한 개만 식별해야 합니다. 예를 들어 City -> State 관계를 가정해 보겠습니다. 이 관계에서 원본 특성은 City이고 관련 특성은 State입니다. 원본 특성은 "다" 쪽 및 관련된 특성은 다 대 일 관계의 "일" 쪽입니다. 원본 특성에 대한 키는 City + State입니다. 자세한 내용은 [특성 관계 만들기, 수정 또는 삭제](attribute-relationships-create-modify-or-delete-relationship.md)를 참조하세요.  
  
 특성 관계의 속성에 대한 자세한 내용은 [특성 관계 속성 구성](attribute-relationships-configure-attribute-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  특성 관계를 잘못 정의하면 유효하지 않은 쿼리 결과를 얻을 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [에서 차원 디자이너의](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
