---
title: sysmail_help_account_sp (거래 -SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: stevestein
ms.author: sstein
ms.openlocfilehash: ccb5cfd245148c97288a34b1857955f48f3efc73
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528417"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  암호를 제외하고 데이터베이스 메일 계정에 대한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @account_id = ] account_id`정보를 나열할 계정의 계정 ID입니다. *account_id* **INT이며**기본값은 NULL입니다.  
  
`[ @account_name = ] 'account_name'`정보를 나열할 계정의 이름입니다. *account_name* **sysname이며**기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0(성공)** 또는 **1(실패)**  
  
## <a name="result-sets"></a>결과 집합  
 아래에 나열된 열을 포함한 결과 집합을 반환합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|**account_id**|**int**|계정의 ID입니다.|  
|**name**|**sysname**|계정 이름입니다.|  
|**설명**|**nvarchar(256)**|계정에 대한 설명입니다.|  
|**email_address**|**nvarchar(128)**|메시지를 보내는 전자 메일 주소입니다.|  
|**display_name**|**nvarchar(128)**|계정의 표시 이름입니다.|  
|**replyto_address**|**nvarchar(128)**|이 계정에서 보낸 메시지에 회신하는 주소입니다.|  
|**Servertype**|**sysname**|계정에 대한 전자 메일 서버의 유형입니다.|  
|**Servername**|**sysname**|계정에 대한 전자 메일 서버의 이름입니다.|  
|**포트**|**int**|사용되는 전자 메일 서버의 포트 번호입니다.|  
|**사용자**|**nvarchar(128)**|전자 메일 서버에서 인증을 사용하는 경우 전자 메일 서버 로그인에 사용할 사용자 이름입니다. **사용자 이름이** NULL이면 Database Mail은 이 계정에 대한 인증을 사용하지 않습니다.|  
|**use_default_credentials**|**bit**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 자격 증명을 사용하여 메일을 SMTP 서버로 보낼지 여부를 지정합니다. **use_default_credentials** 비트이며 기본값은 없습니다. 이 매개 변수가 1이면 데이터베이스 메일에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스의 자격 증명을 사용합니다. 이 매개 변수가 0이면 ** \@** Database Mail은 SMTP 서버에서 인증을 위해 사용자 이름과 ** \@암호를** 사용합니다. ** \@사용자 이름과** ** \@암호가** NULL인 경우 Database Mail은 익명 인증을 사용합니다. 이 매개 변수를 지정하기 전에 해당 SMTP 관리자에게 문의하십시오.|  
|**enable_ssl**|**bit**|데이터베이스 메일이 이전에 SSL(보안 소켓 계층)이라고 하는 TLS(전송 계층 보안)를 사용하여 통신을 암호화하는지 여부를 지정합니다. SMTP 서버에 TLS가 필요한 경우 이 옵션을 사용합니다. **enable_ssl** 비트이며 기본값은 없습니다. 1은 데이터베이스 메일이 TLS를 사용하여 통신을 암호화함을 나타냅니다. 0은 데이터베이스 메일이 TLS 암호화 없이 메일을 전송함을 나타냅니다.|  
  
## <a name="remarks"></a>설명  
 *account_id* 또는 *account_name* 제공되지 않는 경우 **sysmail_help_account** Microsoft SQL Server 인스턴스의 모든 Database Mail 계정에 대한 정보를 나열합니다.  
  
 저장 프로시저 **sysmail_help_account_sp** **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유합니다. 현재 데이터베이스가 **msdb가**아닌 경우 프로시저는 세 부분으로 구성된 이름으로 실행되어야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대한 사용 권한을 시스템 **관리자** 고정 서버 역할의 구성원으로 기본설정합니다.  
  
## <a name="examples"></a>예  
 **1. 모든 계정에 대한 정보 나열**  
  
 다음 예에서는 인스턴스의 모든 계정에 대한 계정 정보를 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **2. 특정 계정에 대한 정보 나열**  
  
 다음 예에서는 `AdventureWorks Administrator`라는 계정에 대해 계정 정보를 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 저장 프로시저 &#40;거래-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
