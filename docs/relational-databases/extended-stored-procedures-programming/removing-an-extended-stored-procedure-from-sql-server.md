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
ms.openlocfilehash: ec61cf630d606977689d3fb3763cce8bd8b705c8
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095431"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>SQL Server에서 확장 저장 프로시저 제거
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 사용자 정의 확장 저장 프로시저 DLL에서 각 확장 저장 프로시저 함수를 삭제 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자가 **sp_dropextendedproc** 시스템 저장 프로시저를 실행 하 여 함수의 이름과 해당 함수가 상주 하는 DLL의 이름을 지정 해야 합니다. 예를 들어이 명령은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 xp_hello .dll 이라는 DLL에 있는 함수 **xp_hello**를 제거 합니다.  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 **sp_dropextendedproc** 는 시스템 확장 저장 프로시저를 삭제 하지 않습니다. 대신 시스템 관리자는 **공용** 역할에 대 한 확장 저장 프로시저에 대 한 EXECUTE 권한을 거부 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_dropextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
