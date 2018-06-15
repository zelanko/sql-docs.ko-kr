---
title: sp_OACreate (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2c7f4598f309549a34cc9dbc39b0ba1a964160bc
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263501"
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE 개체의 인스턴스를 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>인수  
 *progid*  
 만들 OLE개체의 ProgID(프로그래밍 식별자)입니다. 이 문자열은 OLE 개체의 클래스를 설명 및 형식은: **'***OLEComponent***. ***개체***'**  
  
 *OLEComponent* OLE 자동화 서버의 구성 요소 이름 및 *개체* OLE 개체의 이름입니다. 지정 된 OLE 개체가 유효 해야 하며 지원 해야 합니다는 **IDispatch** 인터페이스입니다.  
  
 예를 들어 SQLDMO입니다. Sql Server는 SQL-DMO의 ProgID **SQLServer** 개체입니다. SQL-DMO의 구성 요소 이름은 SQLDMO는 **SQLServer** 개체 유효 하다 고 (모든 SQL-DMO와 같은 개체)는 **SQLServer** 지원 개체 **IDispatch**합니다.  
  
 *clsid*  
 만들 OLE 개체의 CLSID(클래스 식별자)입니다. 이 문자열은 OLE 개체의 클래스를 설명 및 형식은: **' {***nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn***}'** 합니다. 지정 된 OLE 개체가 유효 해야 하며 지원 해야 합니다는 **IDispatch** 인터페이스입니다.  
  
 예를 들어 {00026BA1-0000-0000-C000-000000000046}은 SQL-DMO의 CLSID **SQLServer** 개체입니다.  
  
 *objecttoken* **출력**  
 반환 된 개체 토큰이 며 데이터 형식의 지역 변수 이어야 합니다 **int**합니다. 이 개체 토큰은 만들어진 OLE 개체를 식별하고 다른 OLE Automation 저장 프로시저 호출에 사용됩니다.  
  
 *context*  
 새로 만든 OLE 개체가 실행되는 실행 컨텍스트를 지정합니다. 지정되는 경우 다음 값 중 하나여야 합니다.  
  
 **1** = in-process (.dll) OLE 서버만 합니다.  
  
 **4** = 로컬 (.exe) OLE 서버만 합니다.  
  
 **5** = in-process 및 로컬 모두 OLE 서버가 허용  
  
 기본값은 지정 하지 않으면 **5**합니다. 이 값은 고 *dwClsContext* 에 대 한 호출의 매개 변수 **CoCreateInstance**합니다.  
  
 종속 프로세스 OLE 서버가 허용 된 경우 (의 컨텍스트 값을 사용 하 여 **1** 또는 **5** 또는 컨텍스트 값을 지정 하 여), 메모리에 액세스할 수 및 기타 리소스를 소유한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. in-process OLE 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 또는 리소스를 손상시켜 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 위반과 같은 예기치 못한 결과를 초래할 수도 있습니다.  
  
 컨텍스트 값을 지정 하는 경우 **4**, 로컬 OLE 서버에 액세스할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하며 리소스를 손상 시킬 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 나 리소스가 있습니다.  
  
> [!NOTE]  
>  이 저장 프로시저의 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 참조 [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)합니다.  
  
## <a name="remarks"></a>주의  
 OLE automation procedures가 설정 되어 있는 경우에 대 한 호출 **sp_OACreate** OLE 자동화 공유 실행 환경이 시작 됩니다. OLE 자동화를 설정 하는 방법에 대 한 자세한 내용은 참조 [Ole Automation Procedures 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)합니다.  
  
 만들어진 OLE 개체는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 일괄 처리의 끝 부분에서 자동으로 삭제됩니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-progid"></a>1. ProgID 사용  
 다음 예제에서는 SQL-DMO **SQLServer** ProgID를 사용 하 여 개체입니다.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>2. CLSID 사용  
 다음 예제에서는 SQL-DMO **SQLServer** 의 CLSID를 사용 하 여 개체입니다.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OLE 자동화 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ole Automation Procedures 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
