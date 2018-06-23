---
title: 등록의 전체 경로 사용 하 여 확장 저장된 프로시저 DLL 이름을 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- registering DLL names
- extended stored procedures [SQL Server], registering
- DLL names [SQL Server]
- full path DLL name registration [SQL Server]
ms.assetid: f648d57c-af32-4c71-9882-47b6766f3c2b
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5735e7cc66f269a03ba37fc33dd59e1bdc46c7d1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088770"
---
# <a name="use-the-full-path-to-register-extended-stored-procedure-dll-names"></a>전체 경로를 사용하여 확장 저장 프로시저 DLL 이름을 등록합니다.
  DLL 이름에 대한 전체 경로 없이 이전에 등록된 확장 저장 프로시저는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 작동하지 않을 수 있습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드한 후 DLL 이름에 대한 전체 경로 없이 이전에 등록된 확장 저장 프로시저는 작동하지 않을 수 있습니다. 이는 업그레이드 중에 이전 BINN 디렉터리가 새 경로에 추가되지 않기 때문입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 확장 저장 프로시저를 찾지 못할 수도 있습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드하기 전에 전체 경로 이름으로 등록되지 않은 각 확장 저장 프로시저에 대해 다음 단계를 수행합니다.  
  
1.  sp_dropextendedproc을 실행하여 확장 저장 프로시저를 제거합니다.  
  
2.  sp_addextendedproc을 실행하여 전체 경로 이름으로 확장 저장 프로시저를 등록합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
