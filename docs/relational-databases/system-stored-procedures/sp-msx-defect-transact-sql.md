---
title: sp_msx_defect (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 102698d7efffa753510f3e3b9af6fe40e35408fc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715165"
---
# <a name="sp_msx_defect-transact-sql"></a>sp_msx_defect(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  다중 서버 작업에서 현재 서버를 제거합니다.  
  
> [!CAUTION]  
>  **sp_msx_defect** 레지스트리를 편집 합니다. 레지스트리를 잘못 변경하면 시스템에 심각한 구성 문제를 일으키기 때문에 레지스트리를 수동으로 편집하는 것은 좋지 않습니다. 숙련된 사용자만 레지스트리 편집기 프로그램을 사용하여 레지스트리를 편집해야 합니다. 자세한 내용은 Microsoft Windows 설명서를 참조하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>인수  
`[ @forced_defection = ] forced_defection`무효로 손상 된 **msdb** 데이터베이스로 인해 마스터 SQLServerAgent가 영구적으로 손실 되거나 **msdb** 데이터베이스 백업이 없는 경우 강제로 제거할지 여부를 지정 합니다. *forced_defection*은 **bit**이며 기본값은 **0**으로 강제 제거를 수행 하지 않음을 나타냅니다. 값 **1** 은 강제로 제거 합니다.  
  
 **Sp_msx_defect**를 실행 하 여 강제로 제거 하 고 나 서 마스터 SQLServerAgent에서 **sysadmin** 고정 서버 역할의 멤버는 다음 명령을 실행 하 여 제거를 완료 해야 합니다.  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **Sp_msx_defect** 정상적으로 완료 되 면 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_msx_enlist &#40;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
