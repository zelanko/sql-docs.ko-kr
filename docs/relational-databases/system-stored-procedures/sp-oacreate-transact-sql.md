---
title: sp_OACreate (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2ad8059466ac520b6f9f793af7670cbd73b96b38
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68107929"
---
# <a name="sp_oacreate-transact-sql"></a>sp_OACreate(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE 개체의 인스턴스를 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>인수  
 *progid*  
 만들 OLE개체의 ProgID(프로그래밍 식별자)입니다. 이 문자열은 OLE 개체의 클래스를 설명 하 고 **'**_OLEComponent_' 형식을 갖습니다 **.** _개체_**'**  
  
 *OLEComponent*는 OLE Automation 서버의 구성 요소 이름이며 *Object*는 OLE 개체의 이름입니다. 지정 된 OLE 개체는 유효 해야 하 고 **IDispatch** 인터페이스를 지원 해야 합니다.  
  
 예를 들면 SQLDMO입니다. SQLServer는 sql-dmo **sqlserver** 개체의 ProgID입니다. Sql-dmo의 구성 요소 이름은 SQLDMO이 고 **sqlserver** 개체는 올바르지만 (모든 sql-dmo 개체와 마찬가지로) **sqlserver** 개체가 **IDispatch**를 지원 합니다.  
  
 *가*  
 만들 OLE 개체의 CLSID(클래스 식별자)입니다. 이 문자열은 OLE 개체의 클래스를 설명 하 고 **' {**_nnnnnnnn_-nnnn-nnnnnnnnnnnn **} '** 형식입니다. 지정 된 OLE 개체는 유효 해야 하 고 **IDispatch** 인터페이스를 지원 해야 합니다.  
  
 예를 들어 {00026BA1-0000-0000-C000-000000000046}은 SQL-DMO **SQLServer** 개체의 CLSID입니다.  
  
 _objecttoken_ **출력**  
 반환 된 개체 토큰이 며 **int**데이터 형식의 지역 변수 여야 합니다. 이 개체 토큰은 만들어진 OLE 개체를 식별 하 고 다른 OLE 자동화 저장 프로시저에 대 한 호출에 사용 됩니다.  
  
 *context*  
 새로 만든 OLE 개체가 실행되는 실행 컨텍스트를 지정합니다. 지정되는 경우 다음 값 중 하나여야 합니다.  
  
 **1** = in-process (.DLL) OLE 서버만 해당 됩니다.  
  
 **4** = 로컬 (.EXE) OLE 서버에만 해당 합니다.  
  
 **5** = in-process 및 로컬 OLE 서버 모두 허용  
  
 지정 하지 않으면 기본값은 **5**입니다. 이 값은 **CoCreateInstance**호출의 *dwclscontext* 매개 변수로 전달 됩니다.  
  
 컨텍스트 값이 **1** 또는 **5** 인 컨텍스트 값을 사용 하거나 컨텍스트 값을 지정 하지 않아 in-process OLE 서버가 허용 되는 경우에는에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]소유 하는 메모리 및 기타 리소스에 액세스할 수 있습니다. in-process OLE 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 또는 리소스를 손상시켜 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 위반과 같은 예기치 못한 결과를 초래할 수도 있습니다.  
  
 컨텍스트 값을 **4**로 지정 하면 로컬 OLE 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스에 액세스할 수 없으며 메모리 또는 리소스를 손상 시킬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수 없습니다.  
  
> [!NOTE]  
>  이 저장 프로시저의 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)를 참조 하세요.  
  
## <a name="remarks"></a>설명  
 OLE Automation 프로시저가 설정되어 있는 경우 **sp_OACreate**를 호출하면 OLE Automation 공유 실행 환경이 시작됩니다. OLE 자동화 사용에 대 한 자세한 내용은 [Ole Automation 프로시저 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)을 참조 하십시오.  
  
 만들어진 OLE 개체는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 일괄 처리의 끝 부분에서 자동으로 삭제됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버 자격 또는이 저장 프로시저에 대 한 execute 권한이 필요 합니다. `Ole Automation Procedures`OLE 자동화와 관련 된 시스템 프로시저를 사용 하려면 구성을 사용 하도록 **설정** 해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-progid"></a>A. ProgID 사용  
 다음 예에서는 ProgID를 사용 하 여 SQL-DMO **SQLServer** 개체를 만듭니다.  
  
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
  
### <a name="b-using-clsid"></a>B. CLSID 사용  
 다음 예에서는 CLSID를 사용 하 여 SQL-DMO **SQLServer** 개체를 만듭니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;OLE 자동화 저장 프로시저](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ole 자동화 프로시저 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
