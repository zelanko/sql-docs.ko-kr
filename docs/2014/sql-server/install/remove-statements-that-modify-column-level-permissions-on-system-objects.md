---
title: 시스템 개체에 대 한 열 수준 권한을 수정 하는 문을 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfc0bf1d77322bca3a95ec5d0ed49ab856ce9cf9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125273"
---
# <a name="remove-statements-that-modify-column-level-permissions-on-system-objects"></a>시스템 개체에 대한 열 수준 사용 권한을 수정하는 문을 제거합니다.
  업그레이드 관리자가 시스템 개체에 대한 비표준 열 수준 사용 권한을 검색했습니다. 이러한 권한 변경 내용은 업그레이드 시 유지되지 않습니다. 또한 시스템 개체에 대한 열 수준 사용 권한은 더 이상 지원되지 않습니다. 애플리케이션에서 시스템 개체에 대한 열 수준 사용 권한을 설정하는 문을 제거합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 애플리케이션에서 시스템 개체에 대한 열 수준 사용 권한을 부여, 거부 또는 취소하는 문을 제거합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
