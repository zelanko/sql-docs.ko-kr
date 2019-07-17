---
title: sp_altermessage (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0722bbc713804af6b2b97b5651df5b564d17a136
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117801"
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에서 사용자 정의 메시지 또는 시스템 메시지의 상태를 변경합니다. 사용 하 여 사용자 정의 메시지를 볼 수 있습니다 합니다 **sys.messages** 카탈로그 뷰에 있습니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>인수  
 [ **@message_id =** ] *message_number*  
 변경할 메시지의 오류 번호 **sys.messages**합니다. *message_number* 됩니다 **int** 이며 기본값은 없습니다.  
  
`[ @parameter = ] 'write\_to\_log_'` 와 함께 사용 됩니다 **@parameter_value** 메시지를 쓸 수 임을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그입니다. *write_to_log* 됩니다 **sysname** 이며 기본값은 없습니다. *write_to_log* WITH_LOG 또는 NULL로 설정 해야 합니다. 하는 경우 *write_to_log* WITH_LOG 또는 NULL이 고 값으로 설정 됩니다 **@parameter_value** 됩니다 **true**, Windows 응용 프로그램 로그에 메시지가 기록 됩니다. 하는 경우 *write_to_log* WITH_LOG 또는 NULL 값을 설정할지 **@parameter_value** 됩니다 **false**, 메시지는 항상 Windows 응용 프로그램 로그에 기록 되지는 않지만 될 수 있습니다 오류 발생 방식에 따라 기록 합니다. 하는 경우 *write_to_log* 지정 된 값 **@parameter_value** 도 지정 해야 합니다.  
  
> [!NOTE]  
>  Windows 응용 프로그램 로그에 메시지가 기록된 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 오류 로그 파일에도 기록됩니다.  
  
`[ @parameter_value = ]'value_'` 와 함께 사용 됩니다 **@parameter** 쓸 오류 임을 나타내려면는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그입니다. *값* 됩니다 **varchar(5)** , 기본값은 없습니다. 하는 경우 **true**, 오류가 항상 Windows 응용 프로그램 로그에 기록 됩니다. 하는 경우 **false**, 오류는 항상 Windows 응용 프로그램 로그에 기록 되지는 않지만 오류 발생 방식에 따라 기록 될 수 있습니다. 하는 경우 *값* 를 지정 하면 *write_to_log* 에 대 한 **@parameter** 도 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 미치는 **sp_altermessage** WITH_LOG를 사용 하 여 옵션은 RAISERROR WITH LOG 매개 변수는 점을 제외 하면 비슷합니다 **sp_altermessage** 기존 메시지의 로깅 동작을 변경 합니다. 메시지가 WITH_LOG로 변경된 경우 사용자가 오류를 발생시킨 방법과 상관 없이 항상 Windows 응용 프로그램 로그에 기록됩니다. RAISERROR가 WITH_LOG 옵션 없이 실행된 경우에도 Windows 응용 프로그램 로그에 오류가 기록됩니다.  
  
 시스템 메시지를 사용 하 여 수정할 수 있습니다 **sp_altermessage**합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **serveradmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 기존 메시지 `55001`을 Windows 응용 프로그램 로그에 기록합니다.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
