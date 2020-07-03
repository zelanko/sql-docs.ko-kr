---
title: sp_altermessage (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 925a08a938e56ad2834cf656e89d7a229842641d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85875189"
---
# <a name="sp_altermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에서 사용자 정의 메시지 또는 시스템 메시지의 상태를 변경합니다. 사용자 정의 메시지는 **sys. messages** 카탈로그 뷰를 사용 하 여 볼 수 있습니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>인수  
 [** @message_id =** ] *message_number*  
 메시지를 변경할 메시지의 오류 번호 **입니다.** *message_number* 는 **int** 이며 기본값은 없습니다.  
  
`[ @parameter = ] 'write\_to\_log_'`는 ** \@ parameter_value** 와 함께 사용 되어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그에 메시지를 쓸지 여부를 표시 합니다. *write_to_log* 는 **sysname** 이며 기본값은 없습니다. *write_to_log* WITH_LOG 또는 NULL로 설정 해야 합니다. *Write_to_log* 을 WITH_LOG 또는 NULL로 설정 하 고 ** \@ parameter_value** 값이 **true**이면 메시지는 Windows 응용 프로그램 로그에 기록 됩니다. *Write_to_log* 을 WITH_LOG 또는 NULL로 설정 하 고 ** \@ parameter_value** 값이 **false**이면 메시지는 항상 Windows 응용 프로그램 로그에 기록 되지는 않지만 오류 발생 방식에 따라 작성 될 수 있습니다. *Write_to_log* 지정 된 경우 ** \@ parameter_value** 에 대 한 값도 지정 해야 합니다.  
  
> [!NOTE]  
>  Windows 애플리케이션 로그에 메시지가 기록된 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 오류 로그 파일에도 기록됩니다.  
  
`[ @parameter_value = ]'value_'`는 Windows 응용 프로그램 로그에 오류가 기록 될 것임을 나타내는 ** \@ 매개 변수와** 함께 사용 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] . *값* 은 **varchar (5)** 이며 기본값은 없습니다. **True**이면 오류가 항상 Windows 응용 프로그램 로그에 기록 됩니다. **False**이면 오류가 항상 Windows 응용 프로그램 로그에 기록 되지는 않지만 오류 발생 방식에 따라 기록 될 수 있습니다. *Value* 를 지정 하면 ** \@ 매개 변수에** 대 한 *write_to_log* 도 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 WITH_LOG 옵션을 사용 하는 **sp_altermessage** 의 효과는 **sp_altermessage** 기존 메시지의 로깅 동작을 변경 한다는 점을 제외 하 고 RAISERROR with LOG 매개 변수의 효과와 비슷합니다. 메시지가 WITH_LOG로 변경된 경우 사용자가 오류를 발생시킨 방법과 상관 없이 항상 Windows 애플리케이션 로그에 기록됩니다. RAISERROR가 WITH_LOG 옵션 없이 실행된 경우에도 Windows 애플리케이션 로그에 오류가 기록됩니다.  
  
 **Sp_altermessage**를 사용 하 여 시스템 메시지를 수정할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Serveradmin** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 기존 메시지 `55001`을 Windows 애플리케이션 로그에 기록합니다.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
