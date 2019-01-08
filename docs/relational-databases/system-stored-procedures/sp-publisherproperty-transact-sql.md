---
title: sp_publisherproperty (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49be961d1bc34bcc06b046e95b73d0b5c8ed33ac
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204402"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  표시 하거나 변경에 대 한 게시자 속성 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. 이 저장 프로시저는 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>인수  
 [**@publisher** =] **'***게시자***'**  
 유형이 다른 게시자의 이름입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [**@propertyname** =] **'***propertyname***'**  
 설정할 속성 이름입니다. *propertyname* 됩니다 **sysname**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**xactsetbatching**|후속 작업에 대해 게시자에서 트랜잭션을 일관성 있는 트랜잭션 세트(Xactset)로 그룹화할지 여부입니다. 값이 **활성화** Xactset를 만들 수 있음을, 기본값을 의미 합니다. 값이 **비활성화** 기존 Xactset 없습니다 새 Xactset로 처리 하는 방법을 만들어집니다.|  
|**xactsetjob**|Xactset를 만드는 데 Xactset 작업을 사용할지 여부입니다. 값이 **활성화** Xactset를 만들기 위해 게시자에서 Xactset 작업을 정기적으로 실행 됨을 의미 합니다. 값이 **비활성화** Xactset만 만들어졌는지 로그 판독기 에이전트에서 변경 내용에 대 한 게시자를 폴링할 때를 의미 합니다.|  
|**xactsetjobinterval**|Xactset 작업 실행 간격(분)입니다.|  
  
 때 *propertyname* 를 생략 하면 설정할 수 있는 모든 속성이 반환 됩니다.  
  
 [**@propertyvalue** =] **'***propertyvalue***'**  
 속성 설정의 새 값입니다. *propertyvalue* 됩니다 **sysname**, 기본값은 NULL입니다. 때 *propertyvalue* 를 생략 하면 반환 된 속성에 대 한 현재 설정입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|설정할 수 있는 다음 게시 속성을 반환합니다.<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**propertyvalue**|**sysname**|속성에 대 한 현재 설정 된 **propertyname** 열입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_publisherproperty** 에 대 한 트랜잭션 복제는 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
 개체만 *게시자* 를 지정 하면 결과 집합에 설정할 수 있는 모든 속성에 대 한 현재 설정을 포함 합니다.  
  
 때 *propertyname* 를 지정 하면 결과 집합의 명명된 된 속성만 표시 됩니다.  
  
 모든 매개 변수를 지정하면 속성이 변경되고 결과 집합이 반환되지 않습니다.  
  
 변경 하는 경우는 **xactsetjobinterval** 실행 중인 작업에 대 한 속성을 적용 하려면 새 간격에 대 한 작업을 다시 시작 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할의 배포자에서 실행할 수 있습니다 **sp_publisherproperty**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Oracle 게시자에 대한 트랜잭션 집합 작업 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
