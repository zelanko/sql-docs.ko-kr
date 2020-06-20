---
title: 전체 경로를 사용 하 여 확장 저장 프로시저 DLL 이름을 등록 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- registering DLL names
- extended stored procedures [SQL Server], registering
- DLL names [SQL Server]
- full path DLL name registration [SQL Server]
ms.assetid: f648d57c-af32-4c71-9882-47b6766f3c2b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5ec4ef3fc2e0f2c4834ffa7479a00562ae15d07f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058831"
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
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
