---
title: "메모리 액세스에 최적화된 테이블에서 IDENTITY 구현 | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4ff2fc2a470d0382dfe92a91b996b178ee938337
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>메모리 액세스에 최적화된 테이블에서 IDENTITY 구현
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

IDENTITY는 초기값과 증분값이 모두 1(기본값)인 메모리 최적화 테이블에서 지원됩니다. x != 1 또는 y != 1인 IDENTITY(x, y) 정의를 사용하는 ID 열은 메모리 최적화 테이블에서 지원되지 않습니다.   
    
IDENTITY 초기값을 늘리려면 세션 옵션 `SET IDENTITY_INSERT table_name ON`을 사용하여 ID 열에 대한 명시적 값이 있는 새 행을 삽입합니다. 행을 삽입하면 IDENTITY 초기값이 명시적으로 삽입된 값에 1을 더한 값으로 변경됩니다. 예를 들어 초기값을 1000으로 늘리려면 ID 열에 값이 999인 행을 삽입합니다. 이렇게 하면 생성되는 ID 값이 1000부터 시작됩니다.     
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
