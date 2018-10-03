---
title: SQL Server에 설치 하는 저장된 프로시저 확장 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f8f8616fe8b5a6c06a8492fc713e4e93004d0dad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057273"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>SQL Server에 설치된 확장 저장 프로시저 쿼리
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 된 사용자 및 표시할 수는 현재 정의 된 확장 저장된 프로시저를 실행 하 여 각 DLL의 이름을 속한 합니다 **sp_helpextendedproc** 시스템 프로시저입니다. 다음 예는 DLL을 반환 하는 예를 들어 **xp_hello** 속합니다.  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 하는 경우 **sp_helpextendedproc** 확장된 저장된 프로시저, 모든 확장된 저장된 프로시저 및 해당 Dll이 표시 됩니다 지정 하지 않고 실행 됩니다.  
  
> [!IMPORTANT]  
>  로그인한 사용자가 소유하거나 권한이 있는 확장 저장 프로시저에 대해서만 정보가 반환됩니다. 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner**를 **db_securityadmin**, 및 **db_ddladmin** 고정된 데이터베이스 역할 모든 확장된 저장된 프로시저에 대 한 정보를 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
