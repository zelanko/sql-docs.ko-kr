---
title: sys. numbered_procedure_parameters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d3216f6719371b4e62e25a06a6341ad030620d20
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883800"
---
# <a name="sysnumbered_procedure_parameters-transact-sql"></a>sys.numbered_procedure_parameters(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  번호를 매긴 프로시저의 각 매개 변수당 한 개의 행을 포함합니다. 번호가 매겨진 저장 프로시저를 만들면 기본 프로시저의 번호는 1이며 이어지는 프로시저의 번호는 2, 3... 등이 됩니다. **numbered_procedure_parameters** 은 2 이상 번호가 매겨진 모든 후속 프로시저에 대 한 매개 변수 정의를 포함 합니다. 이 뷰에는 기본 저장 프로시저(번호 = 1)에 대한 매개 변수는 표시하지 않습니다. 기본 저장 프로시저는 번호를 매기지 않은 저장 프로시저와 비슷하므로 따라서 해당 매개 변수는 [sys. parameters (transact-sql)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)로 표시 됩니다.  
  
> [!IMPORTANT]  
>  번호를 매긴 프로시저는 더 이상 사용되지 않으므로 사용하지 않는 것이 좋습니다. 이 카탈로그 뷰를 사용하는 쿼리가 컴파일되면 DEPRECATION_ANNOUNCEMENT 이벤트가 발생합니다.  
  
> [!NOTE]  
>  번호를 매긴 프로시저에는 XML 및 CLR 매개 변수를 사용할 수 없습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 매개 변수가 속한 개체의 ID입니다.|  
|**procedure_number**|**smallint**|개체 내에서 이 프로시저의 번호이며 2 이상입니다.|  
|**name**|**sysname**|매개 변수의 이름입니다. **Procedure_number**내에서 고유 합니다.|  
|**parameter_id**|**int**|매개 변수의 ID입니다. **Procedure_number**내에서 고유 합니다.|  
|**system_type_id**|**tinyint**|매개 변수 시스템 형식의 ID입니다.|  
|**user_type_id**|**int**|사용자가 정의한 매개 변수 유형의 ID입니다.|  
|**max_length**|**smallint**|매개 변수의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 varchar(max), nvarchar(max) 또는 varbinary(max)입니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반일 경우 매개 변수의 전체 자릿수이고 그렇지 않으면 0입니다.|  
|**scale**|**tinyint**|숫자 기반일 경우 매개 변수의 소수 자릿수이고 그렇지 않으면 0입니다.|  
|**is_output**|**bit**|1 = 매개 변수가 출력 또는 반환 값입니다. 그렇지 않으면 0입니다.|  
|**is_cursor_ref**|**bit**|1 = 매개 변수가 커서 참조 매개 변수입니다.|  
  
> [!NOTE]  
>  번호를 매긴 프로시저에는 XML 및 CLR 매개 변수를 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
