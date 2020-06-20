---
title: 호환성 모드 90 이상에서는 CREATE STATISTICS 문에 WITH ROWS를 사용할 수 없습니다. Microsoft Docs
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
ms.openlocfilehash: d28a05e7cd025e213e2cebdce9d582a9df446fea
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065051"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>호환성 모드 90 이상에서는 CREATE STATISTICS 문에 WITH ROWS를 사용할 수 없습니다.
  호환성 모드가 90 이상으로 설정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행할 때 CREATE STATISTICS 문에 WITH ROWS를 지정할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 WITH SAMPLE *number* ROWS를 지정하거나 문서화된 구문에 따라 다른 옵션을 지정하여 WITH ROWS가 포함된 CREATE STATISTICS 문을 수정합니다. 자세한 내용은 SQL Server 온라인 설명서에서 "CREATE STATISTICS(Transact-SQL)" 항목을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
