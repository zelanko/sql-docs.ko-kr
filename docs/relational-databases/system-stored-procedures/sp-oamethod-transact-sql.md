---
title: sp_OAMethod (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: c7dbc0d6ccf753f8f11baee2f5c1c479895d0687
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107923"
---
# <a name="spoamethod-transact-sql"></a>sp_OAMethod(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE 개체의 메서드를 호출합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>인수  
 *objecttoken*  
 사용 하 여 이전에 만든 OLE 개체의 개체 토큰 **sp_OACreate**합니다.  
  
 *methodname*  
 호출할 OLE 개체의 메서드 이름입니다.  
  
 _returnvalue_**출력**  
 OLE 개체 메서드의 반환 값입니다. 지정되는 경우 반드시 적절한 데이터 형식의 지역 변수이어야 합니다.  
  
 로컬 변수를 지정 하거나 단일 값을 반환 하는 메서드 *returnvalue*, 메서드를 반환 하는 로컬 변수에 값을 반환 하거나 지정 하지 마세요 *returnvalue*를 반환 하는 메서드는 단일 열 단일 행 결과 집합으로 클라이언트에 값을 반환 합니다.  
  
 메서드 반환 값은 OLE 개체 *returnvalue* 데이터 형식의 지역 변수 이어야 합니다 **int**합니다. 개체 토큰은 지역 변수에 저장되면 다른 OLE Automation 저장 프로시저에 사용할 수 있습니다.  
  
 때 메서드 반환 값은 배열 하는 경우 *returnvalue* 를 지정 하면 NULL로 설정 됩니다.  
  
 다음 상황에서는 오류가 발생합니다.  
  
-   *returnvalue* 를 지정 하면 메서드가 값을 반환 하지 않습니다.  
  
-   메서드가 두 개 이상의 차원을 가진 배열을 반환합니다.  
  
-   메서드가 배열을 출력 매개 변수로서 반환합니다.  
  
`[ _@parametername = ] parameter[ OUTPUT ]` 메서드 매개 변수가입니다. 를 지정 하는 경우 *매개 변수* 적절 한 데이터 형식의 값 이어야 합니다.  
  
 출력 매개 변수, 반환 값을 얻을 *매개 변수* 적절 한 데이터 형식의 지역 변수 이어야 합니다 하 고 **출력** 지정 해야 합니다. 상수 매개 변수를 지정 여부나 **출력** 지정 하지 않으면 모든 반환 출력 매개 변수의 값은 무시 됩니다.  
  
 를 지정 하는 경우 *parametername* 의 이름 이어야 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 명명 된 매개 변수입니다. 사실은 **@** _parametername_is 하지는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지역 변수입니다. at 기호 ( **@** ) 제거 되 고 *parametername*매개 변수 이름으로 OLE 개체에 전달 됩니다. 모든 명명된 매개 변수는 반드시 모든 위치 매개 변수가 지정된 후에 지정되어야 합니다.  
  
 *n*  
 여러 매개 변수를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
> [!NOTE]
>  *@parametername* 지정 된 메서드의 일부가 고 개체에 전달 됩니다 있기 때문에 명명된 된 매개 변수를 수 있습니다. 이 저장 프로시저의 다른 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)합니다.  
  
## <a name="result-sets"></a>결과 집합  
 메서드 반환 값이 하나 또는 두 개의 차원을 가진 배열인 경우 배열은 결과 집합으로 클라이언트에 반환됩니다.  
  
-   1차원 배열은 배열 내 요소 수만큼의 열이 포함된 단일 행 결과 집합으로 클라이언트에게 반환됩니다. 즉, 배열이 (열)로 반환됩니다.  
  
-   2차원 배열은 배열의 첫 번째 차원에 있는 요소 수만큼의 열과 두 번째 차원에 있는 요소 수만큼의 행이 포함된 결과 집합으로 클라이언트에게 반환됩니다. 즉, 배열이 (열, 행)으로 반환됩니다.  
  
 속성 값을 반환 하는 경우 또는 메서드 반환 값은 배열 **sp_OAGetProperty** 하거나 **sp_OAMethod** 클라이언트에 결과 집합을 반환 합니다. (메서드 출력 매개 변수는 배열이 될 수 없습니다) 이러한 프로시저는 배열의 모든 데이터 값을 검색하여 결과 집합의 각 열에 알맞은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 데이터 길이를 결정합니다. 특정 열에 대해서는 이러한 프로시저에서 해당 열의 모든 데이터 값을 나타내기 위해 필요한 데이터 형식과 길이를 사용합니다.  
  
 하나의 열에 있는 모든 데이터 값이 같은 데이터 형식을 공유하는 경우에는 해당 데이터 형식이 전체 열에 대해 사용됩니다. 한 열의 데이터 값들이 여러 다른 데이터 형식을 가질 경우 전체 열의 데이터 형식이 다음 표를 기준으로 선택됩니다.  
  
||ssNoversion|FLOAT|money|datetime|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>설명  
 사용할 수도 있습니다 **sp_OAMethod** 속성 값을 가져오려고 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 서버 역할 또는 권한이이 저장 프로시저에서 직접 실행 합니다. `Ole Automation Procedures` 구성이 있어야 **활성화** OLE Automation과 관련 된 모든 시스템 프로시저를 사용 하도록 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-a-method"></a>A. 메서드 호출  
 다음 예제에서는 합니다 `Connect` 이전에 만든된 메서드의 **SQLServer** 개체입니다.  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>2\. 속성 가져오기  
 다음 예제에서는 합니다 `HostName` 속성 (이전에 생성 **SQLServer** 개체) 하 고 지역 변수에 저장 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [OLE Automation 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
