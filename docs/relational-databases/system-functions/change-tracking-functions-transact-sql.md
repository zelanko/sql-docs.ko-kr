---
title: 변경 내용 추적 함수 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], change tracking
- change tracking [SQL Server], functions
ms.assetid: 04eb53c4-8b69-414e-9696-185d227fea35
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2397ed5b466715a023ba63e34c6832dbf59ea017
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844037"
---
# <a name="change-tracking-functions-transact-sql"></a>변경 내용 추적 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  변경 내용 추적은 추적된 테이블에 적용되는 삽입, 업데이트 및 삭제 작업을 기록하고, 쉽게 사용할 수 있는 관계형 형식으로 변경의 세부 내용을 제공합니다. 다음 함수는 변경에 대한 정보를 반환합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|[CHANGETABLE (CHANGES)](../../relational-databases/system-functions/changetable-transact-sql.md)|지정된 버전 이후에 발생한 모든 변경 내용에 대한 추적 정보를 테이블에 반환합니다.|  
|[CHANGETABLE (버전)](../../relational-databases/system-functions/changetable-transact-sql.md)|지정된 행에 대한 최신 변경 내용 추적 정보를 반환합니다.|  
|[CHANGE_TRACKING_MIN_VALID_VERSION()](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)|변경 내용 추적 정보가 지정된 된 테이블에서 사용 하는 경우 가져오는 데 사용할 유효한 최소 버전을 반환 합니다 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) 함수입니다.|  
|[CHANGE_TRACKING_CURRENT_VERSION](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)|마지막으로 커밋된 트랜잭션과 연관된 버전을 가져옵니다. 이 버전을 사용하여 다음 번에 CHANGETABLE을 사용하여 변경 내용을 열거할 수 있습니다.|  
|[CHANGE_TRACKING_IS_COLUMN_IN_MASK](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)|CHANGETABLE(CHANGES …) 함수에서 반환된 SYS_CHANGE_COLUMNS 값을 해석합니다.|  
|[WITH CHANGE_TRACKING_CONTEXT](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md)|응용 프로그램이 데이터를 변경할 경우 주관자 ID와 같은 변경 컨텍스트의 사양을 설정합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
