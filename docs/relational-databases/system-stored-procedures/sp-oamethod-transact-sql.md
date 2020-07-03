---
title: sp_OAMethod (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9dced2e79df59117a0ae17e0cee2a1429ebd1d0c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899318"
---
# <a name="sp_oamethod-transact-sql"></a>sp_OAMethod(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  OLE 개체의 메서드를 호출합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>인수  
 *objecttoken*  
 **Sp_OACreate**를 사용 하 여 이전에 만든 OLE 개체의 개체 토큰입니다.  
  
 *methodname*  
 호출할 OLE 개체의 메서드 이름입니다.  
  
 _returnvalue_  **출력**  
 OLE 개체 메서드의 반환 값입니다. 지정되는 경우 반드시 적절한 데이터 형식의 지역 변수이어야 합니다.  
  
 메서드가 단일 값을 반환 하는 경우 *returnvalue*에 대 한 지역 변수를 지정 합니다 .이 변수는 지역 변수의 메서드 반환 값을 반환 하거나, 메서드 반환 값을 클라이언트에 단일 열, 단일 행 결과 집합으로 반환 하는 *returnvalue*를 지정 하지 않습니다.  
  
 메서드 반환 값이 OLE 개체 이면 *returnvalue* 는 **int**데이터 형식의 지역 변수 여야 합니다. 개체 토큰은 지역 변수에 저장 되 고이 개체 토큰은 다른 OLE 자동화 저장 프로시저와 함께 사용 될 수 있습니다.  
  
 메서드 반환 값이 배열인 경우 *returnvalue* 가 지정 되 면 NULL로 설정 됩니다.  
  
 다음 상황에서는 오류가 발생합니다.  
  
-   *returnvalue* 가 지정 되었지만 메서드가 값을 반환 하지 않습니다.  
  
-   메서드가 두 개 이상의 차원을 가진 배열을 반환합니다.  
  
-   메서드가 배열을 출력 매개 변수로서 반환합니다.  
  
`[ _@parametername = ] parameter[ OUTPUT ]`는 메서드 매개 변수입니다. 지정 된 경우 *매개 변수* 는 적절 한 데이터 형식의 값 이어야 합니다.  
  
 출력 매개 변수의 반환 값을 가져오려면 *매개 변수* 는 적절 한 데이터 형식의 지역 변수 여야 하며 **output** 을 지정 해야 합니다. 상수 매개 변수를 지정 하거나 **output** 을 지정 하지 않은 경우 출력 매개 변수의 모든 반환 값은 무시 됩니다.  
  
 지정 된 경우 *parametername* 은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 명명 된 매개 변수의 이름 이어야 합니다. **@**_Parametername_is [!INCLUDE[tsql](../../includes/tsql-md.md)] 지역 변수가 아닙니다. At 기호 ( **@** )가 제거 되 고 *PARAMETERNAME*이 OLE 개체에 매개 변수 이름으로 전달 됩니다. 모든 명명된 매개 변수는 반드시 모든 위치 매개 변수가 지정된 후에 지정되어야 합니다.  
  
 *n*  
 여러 매개 변수를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
> [!NOTE]
>  * \@ parametername* 은 지정 된 메서드의 일부 이며 개체로 전달 되기 때문에 명명 된 매개 변수가 될 수 있습니다. 이 저장 프로시저의 다른 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드, [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)에 대 한 자세한 내용을 보려면  
  
## <a name="result-sets"></a>결과 집합  
 메서드 반환 값이 하나 또는 두 개의 차원을 가진 배열인 경우 배열은 결과 집합으로 클라이언트에 반환됩니다.  
  
-   1차원 배열은 배열 내 요소 수만큼의 열이 포함된 단일 행 결과 집합으로 클라이언트에게 반환됩니다. 즉, 배열이 (열)로 반환됩니다.  
  
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
 **Sysadmin** 고정 서버 역할의 멤버 자격 또는이 저장 프로시저에 대 한 execute 권한이 필요 합니다. `Ole Automation Procedures`OLE 자동화와 관련 된 시스템 프로시저를 사용 하려면 구성을 사용 하도록 **설정** 해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-a-method"></a>A. 메서드 호출  
 다음 예에서는 `Connect` 이전에 만든 **SQLServer** 개체의 메서드를 호출 합니다.  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>B. 속성 가져오기  
 다음 예에서는 `HostName` 이전에 만든 **SQLServer** 개체의 속성을 가져와 지역 변수에 저장 합니다.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;OLE 자동화 저장 프로시저](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
