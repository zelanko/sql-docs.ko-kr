---
title: sp_enumcustomresolvers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4f0b23d39e365a27cc2734e7e051e431055a21f2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032446"
---
# <a name="spenumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포자에 등록된 모든 사용 가능한 비즈니스 논리 처리기와 사용자 지정 해결 프로그램 목록을 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>인수  
 [  **@distributor =**] **'***배포자***'**  
 사용자 지정 해결 프로그램이 있는 배포자의 이름입니다. *배포자* 됩니다 **sysname**, 기본값은 NULL입니다. *이 매개 변수는 사용 되지 않으며 이후 릴리스에서 제거 됩니다.*  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar(255)**|비즈니스 논리 처리기 또는 충돌 해결 프로그램의 이름입니다.|  
|**resolver_clsid**|**nvarchar(50)**|COM 기반 해결 프로그램의 CLSID(클래스 ID)입니다. 이 열은 비즈니스 논리 처리기에 대해 CLSID 값 0을 반환합니다.|  
|**is_dotnet_assembly**|**bit**|비즈니스 논리 처리기에 대한 등록인지 여부를 나타냅니다.<br /><br /> **0** = COM 기반 충돌 해결 프로그램<br /><br /> **1** = 비즈니스 논리 처리기|  
|**dotnet_assembly_name**|**nvarchar(255)**|비즈니스 논리 처리기를 구현하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 어셈블리의 이름입니다.|  
|**dotnet_class_name**|**nvarchar(255)**|비즈니스 논리 처리기를 구현하도록 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>을 재정의하는 클래스의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_enumcustomresolvers** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_enumcustomresolvers**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
