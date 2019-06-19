---
title: TYPEPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TYPEPROPERTY
- TYPEPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], data types
- data types [SQL Server], status information
- TYPEPROPERTY function
ms.assetid: bc311c80-bac5-46ab-a5c8-68b1c6bbf24a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 796de66b6fdce95be5fe235219208a504cc8095e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65946831"
---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터 형식에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>인수  
 *type*  
 데이터 형식의 이름입니다.  
  
 *property*  
 데이터 형식에 대해 반환할 정보의 유형입니다. *property*는 다음 값 중 하나일 수 있습니다.  
  
|속성|설명|반환 값|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|데이터 형식이 Null 값을 허용합니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 데이터 형식을 찾지 못함.|  
|**OwnerId**|형식의 소유자입니다.<br /><br /> 참고: 스키마 소유자가 형식 소유자일 필요는 없습니다.|Null이 아닌 경우 = 형식 소유자의 데이터베이스 사용자 ID입니다.<br /><br /> NULL = 지원되지 않는 형식이거나 형식 ID가 유효하지 않습니다.|  
|**정밀도**|데이터 형식의 전체 자릿수입니다.|자릿수 또는 문자 수입니다.<br /><br /> -1 = **xml** 또는 큰 값 데이터 형식<br /><br /> NULL = 데이터 형식을 찾지 못함.|  
|**소수 자릿수**|데이터 형식의 소수 자릿수입니다.|데이터 형식의 소수 자릿수입니다.<br /><br /> NULL = 데이터 형식이 **numeric**이 아니거나 데이터 형식을 찾지 못함.|  
|**UsesAnsiTrim**|데이터 형식을 만들 때 ANSI 패딩 설정을 ON으로 설정했습니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 데이터 형식을 찾을 수 없거나 이진 또는 문자열 데이터 형식이 아님.|  
  
## <a name="return-types"></a>반환 형식  
 **ssNoversion**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 사용 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 TYPEPROPERTY와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-identifying-the-owner-of-a-data-type"></a>1\. 데이터 형식의 소유자 확인  
 다음 예에서는 데이터 형식의 소유자를 반환합니다.  
  
```  
SELECT TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId') AS owner_id, name, system_type_id, user_type_id, schema_id  
FROM sys.types;  
```  
  
### <a name="b-returning-the-precision-of-the-tinyint-data-type"></a>2\. tinyint 데이터 형식의 전체 자릿수 반환  
 다음 예제에서는 `tinyint` 데이터 형식의 자릿수 또는 전체 자릿수를 반환합니다.  
  
```  
SELECT TYPEPROPERTY( 'tinyint', 'PRECISION');  
```  
  
## <a name="see-also"></a>참고 항목  
 [TYPE_ID&#40;Transact-SQL&#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  

