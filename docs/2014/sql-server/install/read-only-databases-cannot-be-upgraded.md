---
title: 읽기 전용 데이터베이스를 업그레이드할 수 없습니다 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 414b26cf860ab32bb11beaa1ccbef3316c68f557
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093366"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>읽기 전용 데이터베이스를 업그레이드할 수 없습니다.
  업그레이드 관리자가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 일부 데이터베이스를 업그레이드할 수 없음을 감지했습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 읽기 전용 데이터베이스가 검색되었습니다. 데이터베이스를 업그레이드하려면 설치 프로그램이 데이터베이스에 쓸 수 있어야 합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 아무도 데이터베이스를 사용 하 고, 사용 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔터프라이즈 관리자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 또는 읽기 / 쓰기 데이터베이스를 변경 하려면 ALTER DATABASE 문을 합니다. 다음 문은 데이터베이스를 읽기/쓰기로 변경합니다.  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 ALTER DATABASE 문에 대한 자세한 내용은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 온라인 설명서에서 "ALTER DATABASE([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])" 항목을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
