---
title: "SQL Server에 설치 하는 저장된 프로시저에 확장 쿼리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d17f27bf2d9822886c022103fae5834d8b4fddc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>SQL Server에 설치된 확장 저장 프로시저 쿼리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 합니다.  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행 하 여 속한 각 DLL의 이름 및 인증 된 사용자를 표시할 수는 현재 정의 된 확장 저장된 프로시저는 **sp_helpextendedproc** 시스템 프로시저입니다. 다음 예제에서는 DLL을 반환 하는 예를 들어 **xp_hello** 속한:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 경우 **sp_helpextendedproc** 확장된 저장된 프로시저, 모든 확장된 저장된 프로시저 및 해당 Dll 표시 되는 지정 하지 않고 실행 됩니다.  
  
> [!IMPORTANT]  
>  로그인한 사용자가 소유하거나 권한이 있는 확장 저장 프로시저에 대해서만 정보가 반환됩니다. 구성원만는 **sysadmin** 고정된 서버 역할 및 **db_owner**, **db_securityadmin**, 및 **db_ddladmin** 고정된 데이터베이스 역할 모든 확장된 저장된 프로시저에 대 한 정보를 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_helpextendedproc &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
