---
title: sp_changesubscriptiondtsinfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords:
- sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
author: stevestein
ms.author: sstein
ms.openlocfilehash: a091df0cbbeb2883ff9905d7c5b3718d50efa86b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762549"
---
# <a name="spchangesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  구독의 DTS(데이터 변환 서비스) 패키지 속성을 변경합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changesubscriptiondtsinfo [ [ @job_id = ] job_id ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`밀어넣기 구독에 대 한 배포 에이전트의 작업 ID입니다. *job_id* 는 **varbinary (16)** 이며 기본값은 없습니다. 배포 작업 ID를 찾으려면 **sp_helpsubscription** 또는 **sp_helppullsubscription**를 실행 합니다.  
  
`[ @dts_package_name = ] 'dts_package_name'`DTS 패키지의 이름을 지정 합니다. *dts_package_name* 는 **sysname**이며 기본값은 NULL입니다. 예를 들어 **DTSPub_Package**라는 패키지를 지정 하려면를 지정 `@dts_package_name = N'DTSPub_Package'`합니다.  
  
`[ @dts_package_password = ] 'dts_package_password'`패키지에 대 한 암호를 지정 합니다. *dts_package_password* 는 **sysname** 이며 기본값은 암호 속성이 변경 되지 않은 상태로 유지 되도록 지정 하는 NULL입니다.  
  
> [!NOTE]  
>  DTS 패키지에는 암호가 있어야 합니다.  
  
`[ @dts_package_location = ] 'dts_package_location'`패키지 위치를 지정 합니다. *dts_package_location* 은 **nvarchar (12)** 이며 기본값은 패키지 위치를 변경 되지 않은 상태로 유지 하도록 지정 하는 NULL입니다. 패키지의 위치를 **배포자** 또는 **구독자로**변경할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changesubscriptiondtsinfo** 는 밀어넣기 구독에만 사용 되는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할의 멤버 또는 구독의 작성자만 **sp_changesubscriptiondtsinfo**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
