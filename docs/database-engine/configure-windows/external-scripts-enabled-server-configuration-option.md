---
title: "external scripts enabled 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
f1_keywords: 
  - "external scripts enabled"
  - "external_scripts_enabled_TSQL"
helpviewer_keywords: 
  - "external scripts enabled 옵션"
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# external scripts enabled 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  **external scripts enabled** 옵션을 사용하면 특정 원격 언어 확장을 사용하여 스크립트를 실행하도록 설정할 수 있습니다. 이 속성은 기본적으로 해제됩니다. **고급 분석 서비스** 가 설치되어 있으면 설치 프로그램에서 필요에 따라 이 속성을 true로 설정할 수 있습니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 **sp_execute_external_script** 프로시저를 사용하여 외부 스크립트를 실행하려면 외부 스크립트 사용 옵션을 사용하도록 설정해야 합니다. **sp_execute_external_script**를 사용하여 R 등의 지원되는 언어로 작성된 스크립트를 실행합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]와 함께 설치되는 서버 구성 요소와, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 고성능 환경에 데이터 기술자를 연결해 주는 워크스테이션 도구 및 연결 라이브러리 집합으로 구성됩니다.  R 스크립트를 실행할 수 있도록 설정하려면 **설치 중에** 고급 분석 확장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치합니다. 자세한 내용은 [Installing Previous Versions of SQL Server R Services](../Topic/Installing%20Previous%20Versions%20of%20SQL%20Server%20R%20Services.md)을(를) 참조하십시오.  
  
 외부 스크립트를 사용하도록 설정하려면 다음 스크립트를 실행합니다.  
  
```  
sp_configure 'external scripts enabled', 1;  
RECONFIGURE;  
```  
  
 이 변경 내용을 적용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## 참고 항목  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  