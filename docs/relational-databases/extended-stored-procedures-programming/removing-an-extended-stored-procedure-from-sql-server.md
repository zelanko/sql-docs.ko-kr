---
title: 제거 하는 확장 저장 프로시저에서 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7ad2af2bf3d6aa641ac1e8563b01bc51103dccdd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>SQL Server에서 확장 저장 프로시저 제거
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 사용자 정의 확장된 저장된 프로시저 DLL에서에서 각 확장된 저장된 프로시저 함수를 삭제 하려면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자를 실행 해야는 **sp_dropextendedproc** 시스템 저장 프로시저의 이름을 지정 하는 함수 및 해당 함수가 있는 DLL의 이름입니다. 이 명령은 함수를 제거 하는 예를 들어 **xp_hello**에서 xp_hello.dll 이라는 DLL에 있는, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** 시스템 확장 저장된 프로시저를 삭제 하지 않습니다. 시스템 관리자에 확장된 저장된 프로시저에 대 한 EXECUTE 권한이 거부 해야 대신는 **공용** 역할입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_dropextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
