---
title: 저장 프로시저 DLL 언로드 확장 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 148a94bc0413a7fa2a7320599a612b0dcb09d5a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207959"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>확장 저장 프로시저 DLL 언로드
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL의 함수 중 하나를 호출 하는 즉시 확장된 저장된 프로시저 DLL을 로드 합니다. 서버가 종료되거나 시스템 관리자가 DBCC 문을 사용하여 언로드할 때까지 DLL은 로드된 상태로 유지됩니다. 예를 들어이 명령은 언로드합니다 합니다 **xp_hello.dll**, 시스템 관리자 서버를 종료 하지 않고 디렉터리에이 파일의 최신 버전을 복사할 수 있습니다.  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>관련 항목  
 [DBCC dllname &#40;무료&#41; &#40;TRANSACT-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
