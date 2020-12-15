---
description: sys.sysreferences(Transact-SQL)
title: sys.sys참조 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysreferences
- sys.sysreferences_TSQL
- sysreferences
- sysreferences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysreferences compatibility view
- sysreferences system table
ms.assetid: 81276f13-202e-4e74-962d-46eb98c98d2e
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2911993e51f7404b0b1b49fe8bf43af722623e28
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482854"
---
# <a name="syssysreferences-transact-sql"></a>sys.sysreferences(Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  데이터베이스 내의 참조되는 열에 대한 FOREIGN KEY 제약 조건 정의의 매핑을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 제약 조건의 ID입니다.|  
|**fkeyid**|**int**|참조하는 테이블의 ID입니다.|  
|**rkeyid**|**int**|참조되는 테이블의 ID입니다.|  
|**rkeyindid**|**smallint**|참조되는 키 열을 포함하는 참조되는 테이블에 있는 고유 인덱스의 인덱스 ID입니다.|  
|**keycnt**|**smallint**|키에 있는 열의 수입니다.|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|예약되어 있습니다.|  
|**rkeydbid**|**smallint**|예약되어 있습니다.|  
|**fkey1**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey2**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey3**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey4**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey5**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey6**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey7**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey8**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey9**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey10**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey11**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey12**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey13**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey14**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey15**|**smallint**|참조하는 열의 열 ID입니다.|  
|**fkey16**|**smallint**|참조하는 열의 열 ID입니다.|  
|**rkey1**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey2**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey3**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey4**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey5**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey6**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey7**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey8**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey9**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey10**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey11**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey12**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey13**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey14**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey15**|**smallint**|참조되는 열의 열 ID입니다.|  
|**rkey16**|**smallint**|참조되는 열의 열 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
