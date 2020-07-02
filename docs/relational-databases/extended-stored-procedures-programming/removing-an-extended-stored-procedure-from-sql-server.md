---
title: 확장 저장 프로시저 제거
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ec666e49ccc6da12e14f7f1c85ce6eda4b6a4d0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723415"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>SQL Server에서 확장 저장 프로시저 제거
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 사용자 정의 확장 저장 프로시저 DLL에서 각 확장 저장 프로시저 함수를 삭제 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자가 함수 이름 및 해당 함수가 상주 하는 DLL의 이름을 지정 하 여 **sp_dropextendedproc** 시스템 저장 프로시저를 실행 해야 합니다. 예를 들어이 명령은 xp_hello.dll 이라는 DLL에 있는 **xp_hello**함수를 제거 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 부터 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **sp_dropextendedproc** 는 시스템 확장 저장 프로시저를 삭제 하지 않습니다. 대신 시스템 관리자는 **공용** 역할에 대 한 확장 저장 프로시저에 대 한 EXECUTE 권한을 거부 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_dropextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
