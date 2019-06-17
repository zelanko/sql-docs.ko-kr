---
title: SQL Server에서 프로시저 확장 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: bcb58ac180861641803147d1dfea621bd52df9a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512028"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>SQL Server에서 확장 저장 프로시저 제거
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 사용자 정의 확장된 저장된 프로시저 DLL에서에서 각 확장된 저장된 프로시저 함수를 삭제 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자를 실행 해야 합니다 **sp_dropextendedproc** 시스템 저장 프로시저의 이름을 지정 하는 함수 및 해당 함수가 있는 DLL의 이름입니다. 이 명령은 함수를 제거 하는 예를 들어 **xp_hello**에서 xp_hello.dll 이라는 DLL에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]하십시오 **sp_dropextendedproc** 시스템 확장 저장된 프로시저를 삭제 하지 않습니다. 시스템 관리자에 확장된 저장된 프로시저에 EXECUTE 권한을 거부 해야 대신 합니다 **공용** 역할입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_dropextendedproc&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
