---
title: sp_batch_params (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 135937bbdac930d3ee90259c7e5b0f4faaab098f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85874141"
---
# <a name="sp_batch_params-transact-sql"></a>sp_batch_params(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  일괄 처리에 포함 된 매개 변수에 대 한 정보를 포함 하는 행 집합을 반환 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . **sp_batch_params** 지정 된 일괄 처리만 구문 분석 하 고 포함 된 매개 변수 값에 대 한 정보를 반환 합니다. 일괄 처리를 실행하거나 실행 환경을 수정하지는 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @tsqlbatch = ] 'tsqlbatch'`[!INCLUDE[tsql](../../includes/tsql-md.md)]원하는 매개 변수 정보에 대 한 문 또는 일괄 처리를 포함 하는 유니코드 문자열입니다. *tsqlbatch* 는 **nvarchar (max)** 또는 **nvarchar (max)** 로 암시적으로 변환 될 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 일괄 처리에서 찾은 매개 변수의 이름입니다.|  
|**COLUMN_TYPE**|**smallint**|이 필드는 다음 값 중 하나를 반환합니다.<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> 이 열은 항상 0입니다.|  
|**DATA_TYPE**|**smallint**|매개 변수의 데이터 형식(ODBC 데이터 형식에 대한 정수 코드)입니다. 이 데이터 형식을 ISO 형식에 매핑할 수 없는 경우 값은 NULL입니다. Native data 형식 이름은 **TYPE_NAME** 열에 반환 됩니다. 이 값은 항상 NULL입니다.|  
|**TYPE_NAME**|**sysname**|원본으로 사용하는 DBMS에 의해 제시된 데이터 형식의 문자열 표시입니다. 이 값은 NULL입니다.|  
|**소수**|**int**|유효 자릿수입니다. **전체 자릿수** 열의 반환 값은 밑수 10에 있습니다.|  
|**LENGTH**|**int**|데이터의 전송 크기입니다. 이 값은 NULL입니다.|  
|**배율을**|**smallint**|소수점 오른쪽 자릿수입니다. 이 값은 NULL입니다.|  
|**기 수**|**smallint**|숫자 유형에 대한 기준입니다. 이 값은 NULL입니다.|  
|**않는**|**smallint**|Null 허용 여부를 지정합니다.<br /><br /> 1 = Null 값을 허용하는 매개 변수 데이터 형식을 만들 수 있습니다.<br /><br /> 0 = Null 값이 허용되지 않습니다.<br /><br /> 이 값은 NULL입니다.|  
|**SQL_DATA_TYPE**|**smallint**|설명자의 TYPE 필드에 표시된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식의 값입니다. 이 열은 **datetime** 및 ISO **interval** 데이터 형식을 제외 하 고는 **DATA_TYPE** 열과 동일 합니다. 이 열은 항상 값을 반환합니다. 이 값은 NULL입니다.|  
|**SQL_DATETIME_SUB**|**smallint**|**SQL_DATA_TYPE** 값이 SQL_DATETIME 또는 SQL_INTERVAL 경우 **datetime** 또는 ISO **interval** 하위 코드입니다. **datetime**과 ISO **interval**이 아닌 데이터 형식의 경우 이 열은 NULL입니다. 이 값은 NULL입니다.|  
|**CHAR_OCTET_LENGTH**|**int**|**문자** 또는 **이진** 데이터 형식 매개 변수의 최대 길이 (바이트)입니다. 다른 모든 데이터 형식의 경우에는 이 열이 NULL을 반환합니다. 이 값은 항상 NULL입니다.|  
|**ORDINAL_POSITION**|**int**|일괄 처리에 있는 매개 변수의 서수 위치입니다. 매개 변수 이름이 여러 번 반복되는 경우 이 열에는 처음 나타나는 위치의 서수가 포함됩니다. 첫 번째 매개 변수의 서수 위치는 1입니다. 이 열은 항상 값을 반환합니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Sp_batch_params** 를 실행할 수 있는 권한은 **public**에 부여 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sp_batch_params`로 전달되는 쿼리를 보여 줍니다. 결과 집합에는 포함된 매개 변수 값의 목록이 나열됩니다.  
  
```  
DECLARE @SQLString nvarchar(500);  
/* Build the SQL string */  
SET @SQLString =  
     N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
     WHERE BusinessEntityID = @BusinessEntityID';  
EXECUTE sp_batch_params @SQLString;  
```  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [저장 프로시저 실행 방법 항목 ODBC&#41;&#40;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [저장 프로시저&#40;OLE DB&#41; 실행](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
