---
title: 읽기 전용 데이터베이스를 업그레이드할 수 없습니다. | Microsoft Docs
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
ms.openlocfilehash: ba48ed2bd80961a4949dc13f04fed0637ecc27ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054677"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>읽기 전용 데이터베이스를 업그레이드할 수 없습니다.
  업그레이드 관리자가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 일부 데이터베이스를 업그레이드할 수 없음을 감지했습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 읽기 전용 데이터베이스가 검색되었습니다. 데이터베이스를 업그레이드하려면 설치 프로그램이 데이터베이스에 쓸 수 있어야 합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 데이터베이스를 사용 하 고 있지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔터프라이즈 관리자, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 ALTER database 문을 사용 하 여 데이터베이스를 읽기/쓰기로 변경 합니다. 다음 문은 데이터베이스를 읽기/쓰기로 변경합니다.  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 ALTER DATABASE 문에 대한 자세한 내용은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 온라인 설명서에서 "ALTER DATABASE([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])" 항목을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
