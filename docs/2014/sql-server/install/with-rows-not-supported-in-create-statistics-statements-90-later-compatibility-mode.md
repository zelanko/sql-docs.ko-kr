---
title: 행에서 지원 되지 않습니다는 호환성 모드 90 이상에서는 CREATE STATISTICS 문에 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9d509352d99cab9359e7ea222f5fb2d5d7e28075
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172082"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>호환성 모드 90 이상에서는 CREATE STATISTICS 문에 WITH ROWS를 사용할 수 없습니다.
  호환성 모드가 90 이상으로 설정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행할 때 CREATE STATISTICS 문에 WITH ROWS를 지정할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 WITH SAMPLE *number* ROWS를 지정하거나 문서화된 구문에 따라 다른 옵션을 지정하여 WITH ROWS가 포함된 CREATE STATISTICS 문을 수정합니다. 자세한 내용은 SQL Server 온라인 설명서에서 "CREATE STATISTICS(Transact-SQL)" 항목을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
