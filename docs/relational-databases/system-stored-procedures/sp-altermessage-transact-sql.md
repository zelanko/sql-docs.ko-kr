---
title: sp_altermessage (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c254a5ac8837b8e631e2ef688c35bf217a35da7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에서 사용자 정의 메시지 또는 시스템 메시지의 상태를 변경합니다. 사용 하 여 사용자 정의 메시지를 볼 수 있습니다는 **sys.messages** 카탈로그 뷰에 있습니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>인수  
 [**@message_id =** ] *message_number*  
 변경할 메시지의 오류 번호는 **sys.messages**합니다. *message_number* 은 **int** 기본값은 없습니다.  
  
 [ **@parameter =** ] **'***write_to_log*'  
 와 함께 사용 되 **@parameter_value** 메시지에 쓸 임을 나타내기 위해는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그입니다. *write_to_log* 은 **sysname** 기본값은 없습니다. *write_to_log* WITH_LOG 또는 NULL로 설정 해야 합니다. 경우 *write_to_log* WITH_LOG 또는 NULL와에 대 한 값으로 설정 된 **@parameter_value** 은 **true**, Windows 응용 프로그램 로그에 메시지가 기록 됩니다. 경우 *write_to_log* WITH_LOG 또는 NULL 값을로 설정 되어 **@parameter_value** 은 **false**, 메시지는 항상 Windows 응용 프로그램 로그에 기록 되지는 않지만 수 있습니다 오류 발생 방식에 따라 기록 합니다. 경우 *write_to_log* 지정 된 값에 대 한 **@parameter_value** 도 지정 해야 합니다.  
  
> [!NOTE]  
>  Windows 응용 프로그램 로그에 메시지가 기록된 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 오류 로그 파일에도 기록됩니다.  
  
 [ **@parameter_value =** ]**'***value*'  
 와 함께 사용 되 **@parameter** 에 쓰려고 오류 임을 나타내기 위해는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그입니다. *값* 은 **varchar(5)**, 기본값은 없습니다. 경우 **true**, 오류가 항상 Windows 응용 프로그램 로그에 기록 됩니다. 경우 **false**, 오류가 항상 Windows 응용 프로그램 로그에 기록 되지는 않지만 오류 발생 방식에 따라 기록 될 수 있습니다. 경우 *값* 지정 된 *write_to_log* 에 대 한 **@parameter** 도 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 효과 **sp_altermessage** 는 WITH_LOG with 옵션은 RAISERROR WITH LOG 매개 변수를 제외 하 고 유사 하지만 **sp_altermessage** 기존 메시지의 로깅 동작을 변경 합니다. 메시지가 WITH_LOG로 변경된 경우 사용자가 오류를 발생시킨 방법과 상관 없이 항상 Windows 응용 프로그램 로그에 기록됩니다. RAISERROR가 WITH_LOG 옵션 없이 실행된 경우에도 Windows 응용 프로그램 로그에 오류가 기록됩니다.  
  
 시스템 메시지를 사용 하 여 수정할 수 있는 **sp_altermessage**합니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **serveradmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 기존 메시지 `55001`을 Windows 응용 프로그램 로그에 기록합니다.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
