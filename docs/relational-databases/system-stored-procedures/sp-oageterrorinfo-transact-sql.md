---
title: sp_OAGetErrorInfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b5124a091b59ec1669f5d77cbe989f780fee46c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738121"
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE Automation 오류 정보를 얻습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>인수  
 *objecttoken*  
 사용 하 여 이전에 만든 OLE 개체의 개체 토큰 **sp_OACreate** null입니다. 하는 경우 *objecttoken* 는 지정 하면 해당 개체에 대 한 오류 정보가 반환 됩니다. NULL이 지정되면 전체 일괄 처리에 대한 오류 정보가 반환됩니다.  
  
 *소스* **출력**  
 오류 정보의 원본입니다. 를 지정 하는 경우 로컬 이어야 합니다 **char**, **nchar**합니다 **varchar**, 또는 **nvarchar** 변수입니다. 필요한 경우 반환 값을 잘라내어 지역 변수에 맞춥니다.  
  
 *설명을* **출력**  
 오류에 대한 설명입니다. 를 지정 하는 경우 로컬 이어야 합니다 **char**, **nchar**합니다 **varchar**, 또는 **nvarchar** 변수입니다. 필요한 경우 반환 값을 잘라내어 지역 변수에 맞춥니다.  
  
 *helpfile* **출력**  
 OLE 개체의 도움말 파일입니다. 를 지정 하는 경우 로컬 이어야 합니다 **char**, **nchar**합니다 **varchar**, 또는 **nvarchar** 변수입니다. 필요한 경우 반환 값을 잘라내어 지역 변수에 맞춥니다.  
  
 *helpid* **출력**  
 도움말 파일 컨텍스트 ID입니다. 를 지정 하는 경우 로컬 이어야 합니다 **int** 변수입니다.  
  
> [!NOTE]  
>  이 저장 프로시저의 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 참조 하세요. [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)합니다.  
  
## <a name="result-sets"></a>결과 집합  
 출력 매개 변수가 지정되지 않으면 오류 정보는 클라이언트에 결과 집합으로 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|------------------|---------------|-----------------|  
|**오류**|**binary(4)**|오류 번호의 이진 표시입니다.|  
|**원본**|**nvarchar(nn)**|오류의 원본입니다.|  
|**설명**|**nvarchar(nn)**|오류 설명입니다.|  
|**도움말 파일**|**nvarchar(nn)**|원본에 대한 도움말 파일입니다.|  
|**HelpID**|**int**|도움말 원본 파일에 있는 도움말 컨텍스트 ID입니다.|  
  
## <a name="remarks"></a>Remarks  
 각 호출 OLE automation 저장 프로시저 (제외한 **sp_OAGetErrorInfo**) 오류 정보를 다시 설정 하므로 **sp_OAGetErrorInfo** 가장 최근 OLE에 대해서만 오류 정보 Automation 저장 프로시저를 호출 합니다. 되므로 **sp_OAGetErrorInfo** 오류 정보를 다시 설정 하지 않습니다 동일한 오류 정보를 가져오려면 여러 번 호출 될 수 있습니다.  
  
 다음은 OLE Automation 오류 및 일반적 원인을 나열한 표입니다.  
  
|오류 및 HRESULT|일반적 원인|  
|-----------------------|------------------|  
|**잘못 된 변수 형식 (0x80020008)**|데이터 형식의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 메서드 매개 변수와 일치 하지 않습니다 값 전달를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 메서드 매개 변수 또는 NULL 값의 데이터 형식이 메서드 매개 변수로 전달 되었습니다.|  
|**알 수 없는 이름 (0x8002006)**|지정한 개체에 대해 지정한 속성 또는 메서드 이름이 없습니다.|  
|**잘못 된 클래스 문자열 (0x800401f3)**|지정된 ProgID 또는 CLSID가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 OLE 개체로 등록되어 있지 않습니다. 인스턴스화되기를 사용 하 여 사용자 지정 OLE 자동화 서버 등록 해야 **sp_OACreate**합니다. In-process (.dll) 서버의 경우 Regsvr32.exe 유틸리티를 사용 하 여이 수행할 수 있습니다 또는 **/REGSERVER** 로컬 (.exe) 서버에 대 한 명령줄 스위치입니다.|  
|**서버 실행이 실패 했습니다 (0x80080005)**|지정된 OLE 개체가 로컬 OLE 서버(.exe 파일)로 등록되어 있지만 .exe 파일을 찾거나 시작할 수 없습니다.|  
|**지정된 된 모듈 (0x8007007e) 찾을 수 없습니다.**|지정된 OLE 개체가 종속 OLE 서버(.dll 파일)로 등록되어 있지만 .dll 파일을 찾거나 로드할 수 없습니다.|  
|**형식이 일치 하지 않습니다 (0x80020005)**|반환된 속성 값 또는 메서드 반환 값을 저장하는 데 사용한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지역 변수의 데이터 형식이 속성 또는 메서드 반환 값의 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 데이터 형식과 일치하지 않습니다. 또는 속성 또는 메서드 반환 값을 요청했으나 값이 반환되지 않았습니다.|  
|**Datatype or value of the 'context' parameter of sp_OACreate is invalid. (0x8004275B)**|컨텍스트 매개 변수 값 중 하나 여야 합니다. 1, 4 또는 5입니다.|  
  
 HRESULT 반환 코드를 처리 하는 방법에 대 한 자세한 내용은 참조 하십시오 [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음은 OLE Automation 오류 정보를 표시하는 예입니다.  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>관련 항목  
 [OLE Automation 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
