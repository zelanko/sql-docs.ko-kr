---
title: SESSIONPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSIONPROPERTY
- SESSIONPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, SESSIONPROPERTY function
- SESSIONPROPERTY function
- sessions [SQL Server], SET options settings
ms.assetid: 1f3730b4-1495-4d3a-af43-e57952812df9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ba08b2273102d43eed26d7b383a285d6568a63d2
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65942888"
---
# <a name="sessionproperty-transact-sql"></a>SESSIONPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  세션의 SET 옵션 설정을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SESSIONPROPERTY (option)  
```  
  
## <a name="arguments"></a>인수  
 *옵션*  
 이 세션에 대한 현재 옵션 설정입니다. *옵션*은 다음 값 중 하나일 수 있습니다.  
  
|옵션|설명|  
|------------|-----------------|  
|ANSI_NULLS|null 값에 같음(=) 및 같지 않음(<>)의 ISO 동작을 적용할 수 있는지 여부를 지정합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_PADDING|열에서 열에 정의된 크기보다 더 작은 값을 저장하는 방식과 문자 및 이진 데이터에 후행 공백이 있는 값을 저장하는 방식을 제어합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_WARNINGS|0으로 나누기 및 산술 오버플로 등과 같은 특정 상황에 대해 ISO 표준 동작의 오류 메시지나 경고 발생이 적용되는지 여부를 지정합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ARITHABORT|쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생할 때 쿼리를 종료할 것인지 여부를 결정합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|CONCAT_NULL_YIELDS_ NULL|연결된 결과를 null 값으로 다룰 것인지 또는 빈 문자열 값으로 다룰 것인지를 제어합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|NUMERIC_ROUNDABORT|식에서 반올림하여 전체 자릿수 손실이 생길 때 오류 메시지 및 경고의 생성 여부를 지정합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|QUOTED_IDENTIFIER|식별자와 리터럴 문자열을 구분하는 따옴표의 사용 방법에 대한 ISO 규칙을 따를 것인지 여부를 지정합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|\<다른 문자열>|NULL = 입력이 잘못되었습니다.|  
  
## <a name="return-types"></a>반환 형식  
 **sql_variant**  
  
## <a name="remarks"></a>Remarks  
 SET 옵션은 서버 수준, 데이터베이스 수준 및 사용자 지정 옵션을 결합하여 구성됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `CONCAT_NULL_YIELDS_NULL` 옵션의 설정 상태를 반환하는 방법을 보여 줍니다.  
  
```  
SELECT   SESSIONPROPERTY ('CONCAT_NULL_YIELDS_NULL')  
```  
  
## <a name="see-also"></a>참고 항목  
 [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
