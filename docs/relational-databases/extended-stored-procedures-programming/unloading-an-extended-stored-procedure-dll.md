---
description: 확장 저장 프로시저 DLL 언로드
title: 확장 저장 프로시저 DLL 언로드 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
ms.openlocfilehash: f409b15fe8212ca3d5ce25334a0241eb38feea9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88408789"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>확장 저장 프로시저 DLL 언로드
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dll의 함수 중 하나가 호출 되는 즉시 확장 저장 프로시저 DLL을 로드 합니다. 서버가 종료되거나 시스템 관리자가 DBCC 문을 사용하여 언로드할 때까지 DLL은 로드된 상태로 유지됩니다. 예를 들어이 명령은 **xp_hello.dll**를 언로드하고, 시스템 관리자가 서버를 종료 하지 않고이 파일의 최신 버전을 디렉터리에 복사할 수 있도록 합니다.  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>참고 항목  
 [DBCC dllname &#40;FREE&#41; &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
