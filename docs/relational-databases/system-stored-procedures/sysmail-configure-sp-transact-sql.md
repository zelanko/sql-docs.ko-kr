---
title: sysmail_configure_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe47df497b61d35c66bfebfb3ba5a75fad0e183
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588557"
---
# <a name="sysmailconfiguresp-transact-sql"></a>sysmail_configure_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일의 구성 설정을 변경합니다. 지정 된 구성 설정을 **sysmail_configure_sp** 전체에 적용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>인수  
 [**@parameter_name** =] **'**_parameter_name_**'**  
 변경할 매개 변수의 이름입니다.  
  
 [**@parameter_value** =] **'**_parameter_value_**'**  
 매개 변수의 새 값입니다.  
  
 [**@description** =] **'**_설명을_**'**  
 매개 변수에 대한 설명입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 메일은 다음과 같은 매개 변수를 사용합니다.  
  
||||  
|-|-|-|  
|매개 변수 이름|Description|기본값|  
|*AccountRetryAttempts*|외부 메일 프로세스에서 지정된 프로필의 각 계정을 사용하여 전자 메일 메시지를 보내려고 시도하는 횟수입니다.|**1**|  
|*AccountRetryDelay*|외부 메일 프로세스가 메시지 보내기를 시도하는 사이에 대기하는 시간(초)입니다.|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|외부 메일 프로세스가 활성 상태로 유지되는 최소 시간(초)입니다. 데이터베이스 메일에서 많은 메시지를 보내려면 이 값을 늘려 데이터베이스 메일을 활성 상태로 유지하고 자주 시작하고 중지하는 오버헤드를 방지합니다.|**600**|  
|*DefaultAttachmentEncoding*|전자 메일 첨부 파일의 기본 인코딩입니다.|MIME|  
|*MaxFileSize*|첨부 파일의 최대 크기(바이트)입니다.|**1000000**|  
|*ProhibitedExtensions*|전자 메일 메시지에 대한 첨부 파일로 보낼 수 없는 쉼표로 구분된 확장명 목록입니다.|**exe,dll,vbs,js**|  
|*LoggingLevel*|데이터베이스 메일 로그에 기록할 메시지를 지정합니다. 다음 숫자 값 중 하나입니다.<br /><br /> 1 - 표준 모드입니다. 오류만 기록합니다.<br /><br /> 2 - 확장 모드입니다. 오류, 경고 및 정보 메시지를 기록합니다.<br /><br /> 3 - 세부 정보 표시 모드입니다. 오류, 경고, 정보 메시지, 성공 메시지 및 추가 내부 메시지를 기록합니다. 이 모드는 문제 해결을 위해 사용합니다.|**2**|  
  
 저장된 프로시저 **sysmail_configure_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 각 계정을 10 번씩 다시 시도 하도록 데이터베이스 메일 설정**  
  
 다음 예에서는 계정에 연결할 수 없는 것으로 간주하기 전에 각 계정을 10번씩 다시 시도하도록 데이터베이스 메일을 설정합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B. 최대 첨부 파일 크기를 2mb로 설정**  
  
 다음 예에서는 최대 첨부 파일 크기를 2MB로 설정합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
