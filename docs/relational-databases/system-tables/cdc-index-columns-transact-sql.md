---
title: cdc.index_columns (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d47de7882a6eeeca72ad0da8521ab298c7ea8364
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704889"
---
# <a name="cdcindexcolumns-transact-sql"></a>cdc.index_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  변경 테이블과 관련된 각 인덱스 열에 대해 하나의 행을 반환합니다. 인덱스 열은 변경 데이터 캡처에서 원본 테이블의 행을 고유하게 식별하는 데 사용됩니다. 기본적으로 원본 테이블의 기본 키 열이 포함되지만 원본 테이블에서 변경 데이터 캡처가 사용되는 경우 원본 테이블에 고유한 인덱스가 지정되어 있으면 해당 인덱스의 열이 대신 사용됩니다. 순 변경 추적이 설정된 경우에는 원본 테이블에 기본 키 또는 고유 인덱스가 있어야 합니다. 자세한 내용은 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)합니다.  
  
 시스템 테이블은 직접 쿼리하지 않는 것이 좋습니다. 대신 실행 합니다 [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) 저장 프로시저입니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|변경 테이블의 ID입니다.|  
|**column_name**|**sysname**|인덱스 열의 이름입니다.|  
|**index_ordinal**|**tinyint**|인덱스 내에 있는 열의 서수(1부터 시작)입니다.|  
|**column_id**|**int**|원본 테이블에 있는 열의 ID입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [cdc.change_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
