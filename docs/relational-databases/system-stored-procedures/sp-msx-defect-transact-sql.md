---
title: sp_msx_defect (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a9d60318c9e737dd01d80d6ab00b089d98a1fb0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spmsxdefect-transact-sql"></a>sp_msx_defect(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  다중 서버 작업에서 현재 서버를 제거합니다.  
  
> [!CAUTION]  
>  **sp_msx_defect** 는 레지스트리를 편집 합니다. 레지스트리를 잘못 변경하면 시스템에 심각한 구성 문제를 일으키기 때문에 레지스트리를 수동으로 편집하는 것은 좋지 않습니다. 숙련된 사용자만 레지스트리 편집기 프로그램을 사용하여 레지스트리를 편집해야 합니다. 자세한 내용은 Microsoft Windows 설명서를 참조하십시오.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>인수  
 [  **@forced_defection =**] *forced_defection*  
 강제 제거 마스터 SQLServerAgent 손실 된 경우에 영구적으로 복구할 수 없을 정도로 손상으로 인해 발생 여부를 지정 **msdb** 데이터베이스나 아니요 **msdb** 데이터베이스 백업 합니다. *forced_defection*은 **비트**, 기본값은 **0**를 강제로 제거할 발생 않아야 함을 나타냅니다. 값이 **1** 하면 강제 제거 합니다.  
  
 실행 하 여 제거를 강제로 후 **sp_msx_defect**의 멤버는 **sysadmin** 마스터 SQLServerAgent에서 고정된 서버 역할 제거를 완료 하려면 다음 명령을 실행 해야 합니다.  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 때 **sp_msx_defect** 제대로 완료 되 면 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_msx_enlist &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
