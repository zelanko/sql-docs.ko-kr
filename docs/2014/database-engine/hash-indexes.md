---
title: 해시 인덱스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 263fdcd4b09c4acc6c2bba4d67629f867d64c6b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779495"
---
# <a name="hash-indexes"></a>해시 인덱스
  인덱스는 메모리 최적화 테이블의 진입점으로 사용됩니다. 테이블의 행을 읽으려면 메모리에 있는 데이터를 찾을 인덱스가 필요합니다.  
  
 해시 인덱스는 나란히 있는 버킷의 컬렉션으로 구성됩니다. 해시 함수는 인덱스 키를 해시 인덱스의 해당 버킷으로 매핑합니다. 다음 그림에서는 해시 인덱스에 있는 세 개의 서로 다른 버킷에 매핑되는 세 개의 인덱스 키를 보여 줍니다. 이해를 돕기 위해 해시 함수 이름은 f(x)입니다.  
  
 ![인덱스 키가 여러 버킷에 매핑되었습니다.](../../2014/database-engine/media/hekaton-tables-2.gif "인덱스 키가 여러 버킷에 매핑되었습니다.")  
  
 해시 인덱스에 사용되는 해시 함수의 특징은 다음과 같습니다.  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 모든 해시 인덱스에 사용되는 하나의 해시 함수가 있습니다.  
  
-   해시 함수는 결정적입니다. 동일한 인덱스 키가 항상 해시 인덱스의 동일한 버킷에 매핑됩니다.  
  
-   여러 인덱스 키를 동일한 해시 버킷에 매핑할 수 있습니다.  
  
-   해시 함수는 균형을 이룹니다. 즉, 해시 버킷에 대한 인덱스 키 값의 분포는 일반적으로 포아송 분포를 따릅니다.  
  
     포아송 분포는 균등한 분포가 아닙니다. 인덱스 키 값은 해시 버킷에 균등하게 분포되지 않습니다. 예를 들어 *n* 개의 해시 버킷에 대한 *n* 개의 고유 인덱스 키의 포아송 분포는 버킷을 대략적으로 삼등분합니다. 삼등분된 버킷 부분에는 공백, 하나의 인덱스 키, 두 개의 인덱스 키가 각각 포함됩니다. 소수의 버킷에 세 개 이상의 키가 포함됩니다.  
  
 두 개의 인덱스 키가 동일한 해시 버킷에 매핑되면 해시 충돌이 발생합니다. 대부분의 해시 충돌은 읽기 작업의 성능에 영향을 줍니다.  
  
 메모리 내 해시 인덱스 구조는 메모리 포인터의 배열로 구성됩니다. 각 버킷은 이 배열의 오프셋에 매핑됩니다. 배열의 각 버킷은 해당 해시 버킷의 첫 번째 행을 가리킵니다. 버킷의 각 행은 그 다음 행을 가리키기 때문에 다음 그림과 같이 각 해시 버킷에 대한 행 체인이 만들어집니다.  
  
 ![메모리 내 해시 인덱스 구조](../../2014/database-engine/media/hekaton-tables-3.gif "메모리 내 해시 인덱스 구조")  
  
 이 그림에는 행이 포함된 세 개의 버킷이 있습니다. 맨 위에서 두 번째 버킷에는 세 개의 빨간색 행이 포함됩니다. 네 번째 버킷에는 하나의 파란색 행이 포함됩니다. 맨 아래 버킷에는 두 개의 녹색 행이 포함됩니다. 이러한 행은 동일한 행의 서로 다른 버전일 수 있습니다.  
  
 메모리 최적화 테이블의 인덱스에 대한 자세한 내용은 [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블의 인덱스](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
