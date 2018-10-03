---
title: sysmail_help_configure_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1ef80206f9ff82cf1ab2917e90f61432be15c190
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838431"
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
 [**@parameter_name** = ] **'***parameter_name***'**  
 검색할 구성 설정의 이름입니다. 구성 설정의 값을 지정 하면 반환은 **@parameter_value** 출력 매개 변수입니다. 없는 경우 **@parameter_name** 을 지정 하면이 저장된 프로시저 결과 모든 인스턴스에서 데이터베이스 메일 구성 설정이 포함 된 집합을 반환 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없는 경우 **@parameter_name** 을 지정한 경우 결과 다음 열을 사용 하 여 집합을 반환 합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|**paramname**|**nvarchar(256)**|구성 매개 변수의 이름입니다.|  
|**paramvalue**|**nvarchar(256)**|구성 매개 변수의 값입니다.|  
|**description**|**nvarchar(256)**|구성 매개 변수에 대한 설명입니다.|  
  
## <a name="remarks"></a>Remarks  
 저장된 프로시저 **sysmail_help_configure_sp** 인스턴스에 대 한 현재 데이터베이스 메일 구성 설정을 나열 합니다.  
  
 때를 **@parameter_name** 지정 된 출력 매개 변수가 제공 됩니다 있지만 **@parameter_value**,이 저장된 프로시저는 출력이 없습니다.  
  
 저장된 프로시저 **sysmail_help_configure_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 호출 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
