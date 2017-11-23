---
title: sysmail_help_configure_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d799b3d4d319bfda84014e8b520008acdb2c6a30
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailhelpconfiguresp-transact-sql"></a>sysmail_help_configure_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일의 구성 설정을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@parameter_name**  =] **'***p a r a***'**  
 검색할 구성 설정의 이름입니다. 을 지정 구성 설정의 값에 반환 되는  **@parameter_value**  출력 매개 변수입니다. No  **@parameter_name**  지정,이 저장된 프로시저 결과 인스턴스에서 데이터베이스 메일 구성 설정의 모든 포함 된 집합을 반환 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 No  **@parameter_name**  지정 되 면 다음과 같은 열이 있는 결과 집합을 반환 합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|**paramname**|**nvarchar(256)**|구성 매개 변수의 이름입니다.|  
|**paramvalue**|**nvarchar(256)**|구성 매개 변수의 값입니다.|  
|**설명**|**nvarchar(256)**|구성 매개 변수에 대한 설명입니다.|  
  
## <a name="remarks"></a>주의  
 저장된 프로시저 **sysmail_help_configure_sp** 인스턴스에 대 한 현재 데이터베이스 메일 구성 설정을 나열 합니다.  
  
 때는  **@parameter_name**  지정 된 출력 매개 변수 없음 ´ ë ç 하지만  **@parameter_value** ,이 저장된 프로시저는 출력이 없습니다.  
  
 저장된 프로시저 **sysmail_help_configure_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 호출 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 데이터베이스 메일 구성 설정 목록을 보여 줍니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
