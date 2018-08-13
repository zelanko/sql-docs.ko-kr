---
title: sys.fn_virtualservernodes (Transact SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bc722b0b2b240ee72f2899cbebc7076549b4df0b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542053"
---
# <a name="sysfnvirtualservernodes-transact-sql"></a>sys.fn_virtualservernodes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 실행할 수 있는 장애 조치(Failover) 클러스터형 인스턴스 노드의 목록을 반환합니다. 이 정보는 장애 조치 클러스터링 환경에서 유용하게 사용됩니다.  
  
> [!IMPORTANT]  
>  이렇게 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 시스템 기능은 이전 버전과 호환성을 위해 포함 됩니다. 사용 하는 것이 좋습니다 [sys.dm_os_cluster_nodes &#40;Transact SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md) 대신.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>반환된 테이블  
 현재 서버가 클러스터 된 서버인 경우 **fn_virtualservernodes** 이 장애 조치 클러스터 인스턴스 노드의 목록을 반환 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 정의 되어 있습니다.  
  
 현재 서버 인스턴스가 클러스터 된 서버의 경우 **fn_virtualservernodes** 는 빈 행 집합을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대해 VIEW SERVER STATE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `fn_virtualservernodes`를 사용하여 클러스터형 서버 인스턴스에서 쿼리합니다.  
  
```  
SELECT * FROM fn_virtualservernodes();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 NodeName  
  
 -------\-  
  
 SS3-CLUSN1  
  
 SS3-CLUSN2  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_os_cluster_nodes &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;Transact SQL&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  
