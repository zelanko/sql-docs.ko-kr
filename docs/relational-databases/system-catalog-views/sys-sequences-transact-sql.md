---
title: sys.debug (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sequences_TSQL
- sys.sequences
- sequences
- sequences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sys. sequences catalog view
- sys.sequences catalog view
ms.assetid: 0e1b0e32-1cce-40f7-83c8-860ec660138a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4a6588e142fb17f0b90dfb302dda242255513ed3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717568"
---
# <a name="syssequences-transact-sql"></a>sys.sequences(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  데이터베이스의 각 시퀀스 개체에 대한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||는 [sys. 개체](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)의 모든 열을 상속 합니다.|  
|**start_value**|**NULL이 아님 sql_variant**|시퀀스 개체의 시작 값입니다. ALTER SEQUENCE를 사용하여 시퀀스 개체가 다시 시작될 경우 이 값에서 다시 시작됩니다. 시퀀스 개체를 순환 하는 경우 **start_value**가 아닌 **minimum_value** 또는 **maximum_value**으로 진행 됩니다.|  
|**increment**|**NULL이 아님 sql_variant**|각각의 생성되는 값 다음에 시퀀스 개체를 늘리는 데 사용되는 값입니다.|  
|**minimum_value**|**NULL sql_variant**|시퀀스 개체가 생성할 수 있는 최소값입니다. 이 값에 도달하면 시퀀스 개체가 값을 더 생성하려고 할 때 오류를 반환하거나 CYCLE 옵션이 지정되는 경우 다시 시작됩니다. MINVALUE가 지정 되지 않은 경우이 열은 시퀀스 생성기의 데이터 형식에서 지 원하는 최소값을 반환 합니다.|  
|**maximum_value**|**NULL sql_variant**|시퀀스 개체가 생성할 수 있는 최대값입니다. 이 값에 도달하면 시퀀스 개체가 값을 더 생성하려고 할 때 오류 반환을 시작하거나 CYCLE 옵션이 지정되는 경우 다시 시작됩니다. MAXVALUE가 지정되지 않은 경우 이 열은 시퀀스 개체의 데이터 형식이 지원하는 최대값을 반환합니다.|  
|**is_cycling**|**비트 NOT NULL**|시퀀스 개체에 대해 NO CYCLE이 지정된 경우 0을 반환하고 CYCLE이 지정된 경우 1을 반환합니다.|  
|**is_cached**|**비트 NOT NULL**|시퀀스 개체에 대해 NO CACHE가 지정된 경우 0을 반환하고 CACHE가 지정된 경우 1을 반환합니다.|  
|**cache_size**|**int NULL**|시퀀스 개체에 대해 지정된 캐시 크기를 반환합니다. NO CACHE 옵션을 사용하여 시퀀스가 만들어지거나 캐시 크기를 지정하지 않고 CACHE가 지정된 경우 이 열은 NULL을 포함합니다. 캐시 크기로 지정된 값이 시퀀스 개체가 반환할 수 있는 값의 최대 개수보다 클 경우 가져올 수 없는 캐시 크기가 계속 표시됩니다.|  
|**system_type_id**|**tinyint NOT NULL**|시퀀스 개체의 데이터 형식에 대 한 시스템 유형의 ID입니다.|  
|**user_type_id**|**int NOT NULL**|사용자가 정의한 시퀀스 개체에 대한 데이터 형식의 ID입니다.|  
|**전체 자릿수**|**tinyint NOT NULL**|데이터 형식의 최대 전체 자릿수입니다.|  
|**scale**|**tinyint NOT NULL**|형식의 최대 소수 자릿수입니다. 소수 자릿수는 전체 자릿수와 함께 반환되어 사용자에게 전체 메타데이터를 제공합니다. 정수 형식만 허용되기 때문에 시퀀스 개체의 소수 자릿수는 항상 0입니다.|  
|**current_value**|**NULL이 아님 sql_variant**|강제된 마지막 값입니다. 즉, NEXT VALUE FOR 함수를 가장 최근에 실행 하 여 반환 된 값 또는 **sp_sequence_get_range** 프로시저 실행의 마지막 값이 반환 됩니다. 시퀀스가 사용되지 않은 경우 START WITH 값을 반환합니다.|  
|**is_exhausted**|**비트 NOT NULL**|0은 시퀀스에서 값을 더 생성할 수 있다는 의미이며, 1은 시퀀스 개체가 MAXVALUE 매개 변수에 도달했고 시퀀스가 CYCLE로 설정되지 않았다는 의미입니다. ALTER SEQUENCE를 사용하여 시퀀스가 다시 시작될 때까지 NEXT VALUE FOR 함수가 오류를 반환합니다.|  
|**last_used_value**|**NULL sql_variant**|[Next Value For](../../t-sql/functions/next-value-for-transact-sql.md) 함수에 의해 생성 된 마지막 값을 반환 합니다. SQL Server 2017 이상에 적용 됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 사용자가 소유하고 있거나 일부 사용 권한이 부여된 보안 개체의 경우에만 카탈로그 뷰의 메타데이터를 볼 수 있도록 제한됩니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [Transact-sql&#41;시퀀스 &#40;만들기](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-sql&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-sql&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [&#40;Transact-sql&#41;의 다음 값](../../t-sql/functions/next-value-for-transact-sql.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
