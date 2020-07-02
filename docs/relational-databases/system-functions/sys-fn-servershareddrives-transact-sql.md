---
title: sys. fn_servershareddrives (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_servershareddrives
- fn_servershareddrives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_servershareddrives function
- shared drives [SQL Server]
- names [SQL Server], shared drives
- sys.fn_serversharedrives function
ms.assetid: ff01eff7-8cb6-460c-ba7a-6a52bda6d471
author: rothja
ms.author: jroth
ms.openlocfilehash: ce7301325f8cf6ec782b9c9850399617171146f7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85652006"
---
# <a name="sysfn_servershareddrives-transact-sql"></a>sys.fn_servershareddrives(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  클러스터형 서버가 사용하는 공유 드라이브의 이름을 반환합니다.  
  
> [!IMPORTANT]  
>  이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 기능은 이전 버전과의 호환성을 위해 제공됩니다. 대신 [dm_io_cluster_valid_path_names &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) 를 사용 하는 것이 좋습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_servershareddrives()  
```  
  
## <a name="tables-returned"></a>반환된 테이블  
 현재 서버가 클러스터형 서버인 경우 **fn_servershareddrives** 는 공유 드라이브의 드라이브 이름을 반환 합니다.  
  
 현재 서버 인스턴스가 클러스터형 서버가 아닌 경우 **fn_servershareddrives** 는 빈 행 집합을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 `fn_servershareddrives`는 이 클러스터형 서버가 사용하는 공유 드라이브의 목록을 반환합니다. 이러한 공유 드라이브는 리소스와 동일한 클러스터 그룹에 속합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스도 이 드라이브에 종속됩니다.  
  
 이 함수는 사용자가 사용할 수 있는 드라이브를 식별하는 데 유용합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 VIEW SERVER STATE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `fn_servershareddrives`를 사용하여 클러스터형 서버 인스턴스에서 쿼리합니다.  
  
```  
SELECT * FROM fn_servershareddrives();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 DriveName  
  
 -------\-  
  
 분  
  
 n  
  
## <a name="see-also"></a>참고 항목  
 [dm_io_cluster_valid_path_names &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [dm_io_cluster_shared_drives &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [fn_virtualservernodes &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)  
  
  
