---
title: 트리거 중첩이 OFF 일 때도 중첩 AFTER 트리거가 발생 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, nested
- nested triggers option
- triggers [SQL Server], nested
ms.assetid: 94d72960-676e-40d9-81bc-08bffe778110
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0675c412d753a1ce60fa41c7ced40528b3c58f75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093827"
---
# <a name="nested-after-trigger-fires-even-when-trigger-nesting-is-off"></a>트리거 중첩이 OFF일 때도 중첩 AFTER 트리거가 발생합니다.
  업그레이드 관리자가 하나 이상의 테이블에 정의되어 있는 INSTEAD OF 트리거 내부에서 중첩 AFTER 트리거를 검색했습니다. 
  `nested triggers` 서버 구성 옵션이 0으로 설정되어 있는 경우에도 중첩된 AFTER 트리거가 발생할 수 있습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 INSTEAD OF 트리거 내부에 중첩된 첫 번째 AFTER 트리거는 `nested triggers` 서버 구성 옵션이 0으로 설정되어 있는 경우에도 실행됩니다. 그러나 이 설정에서는 이후의 AFTER 트리거는 발생하지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 중첩 트리거에 대한 애플리케이션을 검토하여 `nested triggers` 서버 구성 옵션이 0으로 설정된 경우 이 새 동작과 관련된 비즈니스 규칙을 애플리케이션이 여전히 준수하는지 확인한 다음 적절하게 수정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
