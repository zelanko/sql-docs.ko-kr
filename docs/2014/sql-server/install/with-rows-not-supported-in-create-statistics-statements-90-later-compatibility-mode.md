---
title: 행은 지원 되지 않습니다 호환성 모드 90 이상에서는 CREATE STATISTICS 문에 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090968"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>호환성 모드 90 이상에서는 CREATE STATISTICS 문에 WITH ROWS를 사용할 수 없습니다.
  호환성 모드가 90 이상으로 설정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행할 때 CREATE STATISTICS 문에 WITH ROWS를 지정할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 WITH SAMPLE *number* ROWS를 지정하거나 문서화된 구문에 따라 다른 옵션을 지정하여 WITH ROWS가 포함된 CREATE STATISTICS 문을 수정합니다. 자세한 내용은 SQL Server 온라인 설명서에서 "CREATE STATISTICS(Transact-SQL)" 항목을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
