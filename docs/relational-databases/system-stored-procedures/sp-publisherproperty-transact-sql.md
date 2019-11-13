---
title: sp_publisherproperty (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 0d3ba6552861f162a8ba0755dc37e30bc965e2a4
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962386"
---
# <a name="sp_publisherproperty-transact-sql"></a>sp_publisherproperty(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 대 한 게시자 속성을 표시 하거나 변경 합니다. 이 저장 프로시저는 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`은 유형이 다른 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @propertyname = ] 'propertyname'`는 설정 되는 속성의 이름입니다. *propertyname* 은 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**xactsetbatching**|후속 작업에 대해 게시자에서 트랜잭션을 일관성 있는 트랜잭션 세트(Xactset)로 그룹화할지 여부입니다. **Enabled** 값은 xactset (기본값)를 만들 수 있음을 의미 합니다. **Disabled** 값은 새 xactset 생성 되지 않은 경우에도 기존 xactset 처리 됨을 의미 합니다.|  
|**xactsetjob**|Xactset를 만드는 데 Xactset 작업을 사용할지 여부입니다. **Enabled** 값은 Xactset 작업이 정기적으로 실행 되어 게시자에서 xactset를 만듭니다. **Disabled** 값은 변경 내용에 대해 게시자를 폴링할 때 로그 판독기 에이전트 xactset만 생성 됨을 의미 합니다.|  
|**xactsetjobinterval**|Xactset 작업 실행 간격(분)입니다.|  
  
 *Propertyname* 을 생략 하면 설정 가능한 모든 속성이 반환 됩니다.  
  
 `[ @propertyvalue = ] 'propertyvalue'`  
 속성 설정의 새 값입니다. *propertyvalue* 는 **sysname**이며 기본값은 NULL입니다. *Propertyvalue* 를 생략 하면 속성에 대 한 현재 설정이 반환 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|설정할 수 있는 다음 게시 속성을 반환합니다.<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**propertyvalue**|**sysname**|는 **propertyname** 열의 속성에 대 한 현재 설정입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_publisherproperty** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시자에 대 한 트랜잭션 복제에 사용 됩니다.  
  
 *게시자* 만 지정 하는 경우 결과 집합에는 설정할 수 있는 모든 속성에 대 한 현재 설정이 포함 됩니다.  
  
 *Propertyname* 을 지정 하면 결과 집합에 명명 된 속성만 표시 됩니다.  
  
 모든 매개 변수를 지정하면 속성이 변경되고 결과 집합이 반환되지 않습니다.  
  
 실행 중인 작업의 **xactsetjobinterval** 속성을 변경 하는 경우 작업을 다시 시작 해야 새 간격이 적용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_publisherproperty**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자에 대한 트랜잭션 집합 작업 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
