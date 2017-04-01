---
title: "clr enabled 서버 구성 옵션 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "어셈블리 [CLR 통합], 확인을 실행할 수 있음"
  - "clr enabled 옵션"
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# clr enabled 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  clr enabled 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 어셈블리를 실행할 수 있는지 여부를 지정합니다. clr enabled 옵션은 다음 값을 제공합니다. 
  
|값|설명|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 실행할 수 없습니다.|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 실행할 수 없습니다.|  
  
WOW64에만 해당합니다. 설정 변경 내용을 적용하려면 WOW64 서버를 다시 시작합니다. 다른 서버 유형의 경우에는 서버를 다시 시작하지 않아도 됩니다.  

RECONFIGURE를 실행하고 clr enabled 옵션을 1에서 0으로 변경하면 사용자 어셈블리가 포함된 모든 응용 프로그램 도메인이 즉시 언로드됩니다.  
  
>  **경량 풀링에서는 CLR(공용 언어 런타임) 실행이 지원되지 않습니다.** "clr enabled"와 "lightweight pooling" 옵션 중 하나를 해제하세요. CLR에 의존하며 파이버 모드에서 제대로 작동하지 않는 기능에는 **hierarchy** 데이터 형식, 복제, 정책 기반 관리 등이 있습니다.  
  
## 예제  
 다음 예에서는 먼저 clr enabled 옵션의 현재 설정을 표시한 다음 옵션 값을 1로 설정하여 옵션을 사용하도록 설정합니다. 옵션을 해제하려면 값을 0으로 설정합니다.  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## 참고 항목  
 [경량 풀링 서버 구성 옵션](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [경량 풀링 서버 구성 옵션](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  