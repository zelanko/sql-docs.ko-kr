---
description: sp_OAGetProperty(Transact-SQL)
title: sp_OAGetProperty (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6fb1683c5c873bf561c012e00907cbe90e1c1fbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493169"
---
# <a name="sp_oagetproperty-transact-sql"></a>sp_OAGetProperty(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  OLE 개체의 속성 값을 구합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>인수  
 *objecttoken*  
 **Sp_OACreate**를 사용 하 여 이전에 만든 OLE 개체의 개체 토큰입니다.  
  
 *propertyname*  
 반환할 OLE 개체의 속성 이름입니다.  
  
 *propertyvalue* **출력**  
 반환된 속성 값입니다. 지정되는 경우 반드시 적절한 데이터 형식의 지역 변수이어야 합니다.  
  
 속성이 OLE 개체를 반환 하는 경우 *propertyvalue* 는 **int**데이터 형식의 지역 변수 여야 합니다. 개체 토큰은 지역 변수에 저장 되 고이 개체 토큰은 다른 OLE 자동화 저장 프로시저와 함께 사용 될 수 있습니다.  
  
 속성이 단일 값을 반환 하는 경우 *propertyvalue*의 지역 변수를 지정 합니다 .이 변수는 지역 변수에서 속성 값을 반환 합니다. 또는 속성 값을 단일 열, 단일 행 결과 집합으로 클라이언트에 반환 하는 *propertyvalue*를 지정 하지 마십시오.  
  
 속성이 배열을 반환 하는 경우 *propertyvalue* 를 지정 하면 NULL로 설정 됩니다.  
  
 *Propertyvalue* 를 지정 했지만 속성에서 값을 반환 하지 않는 경우 오류가 발생 합니다. 속성이 두 개 이상의 차원을 가진 배열을 반환하는 경우 오류가 발생합니다.  
  
 *index*  
 인덱스 매개 변수입니다. 지정 된 경우 *인덱스* 는 적절 한 데이터 형식의 값 이어야 합니다.  
  
 일부 속성에는 매개 변수가 있습니다. 이러한 속성을 인덱싱된 속성이라 하고 매개 변수를 인덱스 매개 변수라고 합니다. 하나의 속성이 여러 개의 인덱스 매개 변수를 가질 수 있습니다.  
  
> [!NOTE]  
>  이 저장 프로시저의 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)를 참조 하세요.  
  
## <a name="result-sets"></a>결과 집합  
 속성이 한 개 또는 두 개의 차원을 가진 배열을 반환하면 배열은 결과 집합으로 클라이언트에게 반환됩니다.  
  
-   1차원 배열은 배열 내 요소 수만큼의 열이 포함된 단일 행 결과 집합으로 클라이언트에게 반환됩니다. 즉, 배열이 열로 반환됩니다.  
  
-   2차원 배열은 배열의 첫 번째 차원에 있는 요소 수만큼의 열과 두 번째 차원에 있는 요소 수만큼의 행이 포함된 결과 집합으로 클라이언트에게 반환됩니다. 즉, 배열이 (열, 행)으로 반환됩니다.  
  
 속성 반환 값 또는 메서드 반환 값이 배열인 경우 **sp_OAGetProperty** 또는 **sp_OAMethod** 결과 집합을 클라이언트에 반환 합니다. (메서드 출력 매개 변수는 배열이 될 수 없습니다) 이러한 프로시저는 배열의 모든 데이터 값을 검색하여 결과 집합의 각 열에 알맞은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 데이터 길이를 결정합니다. 특정 열에 대해서는 이러한 프로시저에서 해당 열의 모든 데이터 값을 나타내기 위해 필요한 데이터 형식과 길이를 사용합니다.  
  
 하나의 열에 있는 모든 데이터 값이 같은 데이터 형식을 공유하는 경우에는 해당 데이터 형식이 전체 열에 대해 사용됩니다. 한 열의 데이터 값들이 여러 다른 데이터 형식을 가질 경우 전체 열의 데이터 형식이 다음 표를 기준으로 선택됩니다.  
  
||int|float|money|Datetime|varchar|nvarchar|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>설명  
 **Sp_OAMethod** 를 사용 하 여 속성 값을 가져올 수도 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버 자격 또는이 저장 프로시저에 대 한 execute 권한이 필요 합니다. `Ole Automation Procedures` OLE 자동화와 관련 된 시스템 프로시저를 사용 하려면 구성을 사용 하도록 **설정** 해야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-a-local-variable"></a>A. 지역 변수 사용  
 다음 예에서는 `HostName` 이전에 만든 **SQLServer** 개체의 속성을 가져와 지역 변수에 저장 합니다.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. 결과 집합 사용  
 다음 예에서는 `HostName` 이전에 만든 **SQLServer** 개체의 속성을 가져와서이를 결과 집합으로 클라이언트에 반환 합니다.  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;OLE 자동화 저장 프로시저 ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
