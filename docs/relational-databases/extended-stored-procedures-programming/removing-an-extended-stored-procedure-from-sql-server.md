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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74095431"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>SQL Server에서 확장 저장 프로시저 제거
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 하세요.  
  
 사용자 정의 확장 저장 프로시저 DLL에서 각 확장 저장 프로시저 함수를 삭제 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자가 함수 이름 및 해당 함수가 상주 하는 DLL의 이름을 지정 하 여 **sp_dropextendedproc** 시스템 저장 프로시저를 실행 해야 합니다. 예를 들어 다음 명령은 **xp_hello**에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]xp_hello .dll 이라는 dll에 있는 함수를 제거 합니다.  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 부터 sp_dropextendedproc [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]는 **** 시스템 확장 저장 프로시저를 삭제 하지 않습니다. 대신 시스템 관리자는 **공용** 역할에 대 한 확장 저장 프로시저에 대 한 EXECUTE 권한을 거부 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_dropextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
