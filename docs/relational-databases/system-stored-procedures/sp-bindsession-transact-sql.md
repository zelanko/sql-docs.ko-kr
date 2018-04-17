---
title: sp_bindsession (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7d47d969caa2e4f93482f4f457971d32c179264
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  바인딩 또는의 동일한 인스턴스에 있는 다른 세션에 대 한 세션을 바인딩 해제 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다. 세션을 바인딩하면 두 개 이상의 세션이 같은 트랜잭션에 참가할 수 있으며 ROLLBACK TRANSACTION 또는 COMMIT TRANSACTION이 실행될 때까지 잠금을 공유할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 MARS(Multiple Active Results Sets) 또는 분산 트랜잭션을 사용하십시오. 자세한 내용은 참조 [Multiple Active Result Sets를 사용 하 여 & #40; MARS & #41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>인수  
 **'** *bind_token* **'**  
 트랜잭션을 식별 하는 토큰 처음에 확보를 사용 하 여 **sp_getbindtoken** 또는 개방형 데이터 서비스인 **srv_getbindtoken** 함수입니다. *bind_token*은 **varchar (255)**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 바인딩된 두 세션은 트랜잭션과 잠금만 공유합니다. 각 세션은 고유한 격리 수준을 유지하며 한 세션에서 새 격리 수준을 설정해도 다른 세션의 격리 수준에는 영향을 주지 않습니다. 각 세션은 보안 계정으로 계속 식별할 수 있으며 해당 계정이 권한을 부여 받은 데이터베이스 리소스에만 액세스할 수 있습니다.  
  
 **sp_bindsession** 두 개 이상의 기존 클라이언트 세션을 바인딩하는 바인드 토큰을 사용 합니다. 이들 클라이언트 세션은 바인딩 토큰을 확보한 같은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 있어야 합니다. 세션은 명령을 실행하는 클라이언트입니다. 바인딩된 데이터베이스 세션은 트랜잭션 및 잠금 공간을 공유합니다.  
  
 한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 확보한 바인딩 토큰은 DTC 트랜잭션을 포함해서 다른 인스턴스에 연결된 클라이언트 세션에 사용할 수 없습니다. 바인딩 토큰은 각 인스턴스 내에 로컬로만 유효하며 여러 인스턴스에 걸쳐 공유할 수 없습니다. 다른 인스턴스에서 클라이언트 세션을 바인딩하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 실행 하 여 다른 바인딩 토큰을 가져와야 합니다 **sp_getbindtoken**합니다.  
  
 **sp_bindsession** 활성화 되지 않은 토큰을 사용 하는 경우 오류가 발생 하면서 실패 합니다.  
  
 사용 하 여 세션에서 바인딩을 해제할 **sp_bindsession** 지정 하지 않고 *bind_token* 에 NULL을 전달 하 여 *bind_token*합니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 바인딩 토큰을 현재 세션에 바인딩합니다.  
  
> [!NOTE]  
>  이 예제에 표시 된 바인드 토큰을 실행 하 여 가져온 **sp_getbindtoken** 실행 하기 전에 **sp_bindsession**합니다.  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_getbindtoken& #40; Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;확장 저장 프로시저 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
