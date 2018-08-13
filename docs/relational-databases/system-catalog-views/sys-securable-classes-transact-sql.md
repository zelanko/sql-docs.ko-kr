---
title: sys.securable_classes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- securable_classes_TSQL
- securable_classes
- sys.securable_classes_TSQL
- sys.securable_classes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.securable_classes catalog view
ms.assetid: ae2bf589-17be-4cad-b5d5-05a34173b32d
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 44a9a7268c58ee87c21ae399021e7f0530d9e0c2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551943"
---
# <a name="syssecurableclasses-transact-sql"></a>sys.securable_classes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  보안 개체 클래스 목록을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**class_desc**|**sysname**|클래스의 이름입니다.|  
|**class**|**int**|클래스의 숫자 지정입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이 인스턴스에서 지원하는 보안 개체 클래스를 반환합니다.  
  
```sql  
SELECT * FROM sys.securable_classes ORDER BY class;  
```  
  
## <a name="see-also"></a>관련 항목  
 [보안 개체](../../relational-databases/security/securables.md)  
  
  
