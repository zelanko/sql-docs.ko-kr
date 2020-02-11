---
title: sys. edge_constraint_clauses (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraint_clauses
- edge_constraint_clauses
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraint_clauses catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26b347703a632a4147f8dcba369efaa272b4cef9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079349"
---
# <a name="sysedge_constraint_clauses-transact-sql"></a>sys. edge_constraint_clauses (Transact-sql)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

에 지 제약 조건에 대 한 하나의 행을 포함 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|에 지 제약 조건의 object_id입니다.|  
|**from_object_id**|**int**|FROM node 테이블의 object_id입니다.|  
|**to_object_id**|**int**|TO 노드 테이블의 object_id입니다.|  
|**clause_number**|**int**|내부적으로 생성 된 절의 정수 인덱스입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
