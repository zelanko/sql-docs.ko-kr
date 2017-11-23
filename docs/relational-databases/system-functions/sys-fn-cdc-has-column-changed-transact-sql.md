---
title: sys.fn_cdc_has_column_changed (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_has_column_changed_TSQL
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed_TSQL
- fn_cdc_has_column_changed
dev_langs: TSQL
helpviewer_keywords:
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed
ms.assetid: 2b9e6278-050d-4ffc-8d1a-09606180facc
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 605d44ed6af4de9abb5e7950954c6e2ade6c60d4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysfncdchascolumnchanged-transact-sql"></a>sys.fn_cdc_has_column_changed(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 업데이트 마스크가 관련 변경 행에서 지정된 열이 업데이트되었음을 나타내는지 여부를 식별합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_cdc_has_column_changed ( 'capture_instance','column_name' , update_mask )  
```  
  
## <a name="arguments"></a>인수  
 **'** *capture_instance* **'**  
 캡처 인스턴스의 이름입니다. *capture_instance* 은 **sysname**합니다.  
  
 **'** *column_name* **'**  
 보고할 지정된 캡처 인스턴스의 캡처된 열입니다. *column_name* 은 **sysname**합니다.  
  
 *update_mask*  
 관련 변경 행에서 업데이트된 열을 식별하는 마스크입니다. *update_mask* 은 **varbinary(128)**합니다.  
  
## <a name="return-type"></a>반환 형식  
 **bit**  
  
## <a name="remarks"></a>주의  
 이 함수를 사용하여 변경 데이터에 대한 쿼리에 반환된 업데이트 마스크에서 정보를 추출할 수 있습니다. 관련 변경 행에서 특정 열이 수정되었는지 여부를 확인할 때 업데이트 마스크의 후처리에 가장 유용합니다. 자세한 내용은 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)를 참조하세요.  
  
 이 정보는 변경 데이터 쿼리의 일부로 반환 됩니다 하는 경우 함수를 사용 하는 것이 좋습니다 [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) 및 [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) 이 함수 대신 합니다. 원하는 열 서수가 한 번만 계산되도록 하려면 변경 데이터를 쿼리하기 전에 fn_cdc_get_column_ordinal 함수를 사용합니다. 반환된 각 행의 업데이트 마스크에서 정보를 추출하려면 이 쿼리 내에서 fn_cdc_is_bit_set을 사용합니다.  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다. 다른 모든 사용자의 경우 원본 테이블에서 캡처된 모든 열에 대한 SELECT 권한이 필요하며 캡처 인스턴스에 대한 제어 역할이 정의된 경우 해당 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [cdc. &#60; capture_instance& &#62; _CT &#40; Transact SQL &#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)   
 [cdc.captured_columns &#40; Transact SQL &#41;](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
  
  
