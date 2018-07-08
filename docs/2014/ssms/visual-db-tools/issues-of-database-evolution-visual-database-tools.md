---
title: 데이터베이스의 단계적 개발 문제(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dcfafbe237f58d6e53cdc64642f5090b9139731e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161584"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>데이터베이스의 단계적 개발 문제(Visual Database Tools)
  배포된 데이터베이스의 구조를 변경하는 경우 변경 내용이 기존 데이터 및 데이터베이스 구조와 호환되도록 각별히 주의해야 합니다. 다음과 같이 수정한 경우 특별한 단계를 수행해야 할 수도 있습니다.  
  
-   **제약 조건 추가** 제약 조건을 추가하는 경우 데이터베이스에 제약 조건을 만족하지 않는 데이터가 이미 있을 수 있습니다. 새 제약 조건을 저장하려고 하면 [저장 후 알림 대화 상자&#40;Visual Database Tools&#41;](visual-database-tools.md)가 표시되어 데이터베이스 서버에서 제약 조건을 만들 수 없음을 알려 줍니다. 데이터베이스에서 새 제약 조건을 강제로 허용하도록 하려면 **만들 때 기존 데이터 검사** 확인란을 선택 취소하면 됩니다.  
  
-   **관계 추가** 관계를 추가하는 경우 기본 키 테이블에 해당 행이 없는 외래 키 테이블 행이 이미 데이터베이스에 있을 수 있습니다. 즉, 기존 데이터가 참조 무결성을 충족하지 않을 수 있습니다. 새 관계를 저장하려고 하면 [저장 후 알림 대화 상자&#40;Visual Database Tools&#41;](visual-database-tools.md)가 표시되어 데이터베이스 서버에서 수정된 외래 키 테이블을 저장할 수 없음을 알려 줍니다. 데이터베이스에 수정 내용을 강제로 적용하려면 **만들 때 기존 데이터 검사** 확인란을 선택 취소하면 됩니다.  
  
-   **인덱싱된 뷰에 적용되는 테이블 수정** Microsoft SQL Server 인덱싱된 뷰에 적용되는 테이블을 수정하면 해당 뷰의 인덱스가 손실됩니다. 인덱스 다시 만들기에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
-   **개체 삭제** 열, 테이블 또는 뷰와 같은 개체를 삭제하는 경우 데이터베이스의 다른 개체가 이러한 삭제 대상 개체를 참조하고 있지 않은지 먼저 확인해야 합니다.  
  
 데이터베이스 디자인을 변경하는 방법에 관계 없이 변경 기록을 유지해야 합니다. 프로덕션 데이터베이스의 모든 수정 내용에 대한 SQL 스크립트를 유지하는 것도 변경 기록을 유지하는 한 방법입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Unique 제약 조건 및 Check 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [다중 사용자 환경&#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
