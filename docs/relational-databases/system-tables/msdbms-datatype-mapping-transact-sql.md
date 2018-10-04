---
title: MSdbms_datatype_mapping (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9131b565fe140378c65826998e338a80a5813b01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727535"
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdbms_datatype_mapping** 테이블 대상 DBMS의에서 하나 이상의 특정 데이터 형식으로 원본 데이터베이스 관리 시스템 (DBMS) 데이터 형식에서 허용 되는 데이터 형식 매핑을 포함 합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스 및 다른 유형의 데이터베이스 복제에 사용 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|고유한 각 데이터 형식 매핑을 식별합니다.|  
|**map_id**|**int**|원본 데이터 형식을 식별합니다.|  
|**dest_datatype_id**|**int**|대상 데이터 형식을 식별합니다.|  
|**dest_precision**|**bigint**|여기서 NULL 값은 전체 자릿수가 사용 되지 않음을 의미, 대상 데이터 형식의 전체 자릿수 및 값 정의 **-1** 원본 데이터 형식의 전체 자릿수가 사용 됨을 의미 합니다.|  
|**dest_scale**|**int**|여기서 NULL 값 확장은 사용 되지 않음을 의미, 대상 데이터 형식의 소수 자릿수 및 값 정의 **-1** 원본 데이터 형식의 소수 자릿수 사용 됨을 의미 합니다.|  
|**dest_length**|**bigint**|여기서 NULL 값은 길이가 사용 되지 않음을 의미, 대상 데이터 형식, 길이 및 값 정의 **-1** 원본 데이터 형식의 길이가 사용 됨을 의미 합니다.|  
|**dest_nullable**|**bit**|매핑의 대상 열이 NULL 값을 허용하는지 여부를 나타냅니다. 여기서 NULL 값은 이 정의가 필요하지 않음을 의미합니다.|  
|**dest_createparams**|**int**|각 데이터 형식에 적용할 수 있는 길이, 전체 자릿수, 소수 자릿수의 조합을 설명하는 비트맵이며 다음을 포함합니다.<br /><br /> **0x1** = 전체 자릿수입니다.<br /><br /> **0x2** = 소수 자릿수입니다.<br /><br /> **0x4** = 길이입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
