---
title: Execute 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
author: rothja
ms.author: jroth
ms.openlocfilehash: b4c44e48c46abab1cc15e3fbf90592414fad7c9c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82752673"
---
# <a name="execute-method-rds"></a>Execute 메서드(RDS)
요청을 실행 하 고 ADO 2.5 이상에서 사용할 ADO 레코드 집합을 만듭니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 요청을 실행 하기 위해 전송 되는 OLE DB 공급자에 연결 하는 데 사용 되는 문자열입니다. *Handlerstring* 을 사용 하 여 처리기를 지정 하는 경우 연결 문자열을 편집 하거나 바꿀 수 있습니다.  
  
 *HandlerString*  
 이 실행에 사용할 처리기를 식별 하는 두 부분으로 구성 된 문자열입니다. 문자열에는 두 부분이 포함 됩니다. 첫 번째 부분에는 사용할 처리기의 이름 (ProgID)이 포함 되어 있습니다. 두 번째 부분은 처리기에 전달할 인수를 포함 합니다. 인수 문자열을 해석 하는 방법에 대 한 세부 정보는 각 처리기와 관련이 있습니다. 문자열의 첫 번째 인스턴스는 두 부분으로 구분 됩니다. 인수 문자열에는 추가 쉼표를 사용할 수 있습니다. 인수는 선택 사항입니다.  
  
 *QueryString*  
 연결 문자열에서 식별 된 OLE DB 공급자가 지 원하는 명령 언어의 명령입니다. SQL 기반 공급자의 경우 *QueryString* 은 transact-sql 명령 문을 포함할 수 있지만 sql이 아닌 공급자 (예: MSDataShape)의 경우 쿼리 문이 아닐 수 있습니다 [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
 처리기를 사용 하는 경우 처리기는 여기에 지정 된 값을 변경 하거나 바꿀 수 있습니다. 예를 들어 처리기는 일반적으로 *QueryString* 파일의 쿼리 문자열로 QueryString을 대체 합니다. 기본적으로 Msdfmap .ini 파일이 사용 됩니다.  
  
 *lFetchOptions*  
 비동기 인출의 유형을 나타냅니다.  
  
 자세한 내용은 [Fetchoptions 속성 (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)을 참조 하십시오.  
  
 *TableID*  
 VT_EMPTY 또는 VT_BSTR 형식의 **변형** 입니다. 이 값이 VT_EMPTY 형식이 면 무시 됩니다. VT_BSTR 형식인 경우 **adCmdTableDirect** 를 사용 하 여 레코드 집합을 만들고 여기에 지정 된 값과 *QueryString* 매개 변수는 무시 됩니다.  
  
 *lExecuteOptions*  
 실행 옵션의 비트 마스크입니다.  
  
 1 =*Readonly* **adlockreadonly**를 사용 하 여 레코드 집합을 엽니다.  
  
 2 =*Nobatch* 레코드 집합은 **adlockoptimistic**을 사용 하 여 열립니다.  
  
 4 =*Allparaminfosupplied* 호출자는 모든 매개 변수에 대 한 매개 변수 정보가 *pparameters*에 제공 되도록 보장 합니다.  
  
 8 =*GetInfo* 공급자 OLE DB에서 쿼리에 대 한 매개 변수 정보를 가져오고 *pparameters* 매개 변수에 반환 합니다. 쿼리가 실행 되지 않으며 레코드 집합이 반환 되지 않습니다.  
  
 16 =*GetHiddenColumns* 는 **Adlockbatchoptimistic** 을 사용 하 여 레코드 집합을 열고 숨겨진 열은 레코드 집합에 포함 됩니다.  
  
 *ReadOnly*, *Nobatch* 및 *GetHiddenColumns* 는 함께 사용할 수 없는 옵션입니다. 그러나 둘 이상의 항목을 설정 하는 오류는 생성 하지 않습니다. 여러 옵션을 설정 하는 경우 *GetHiddenColumns* 는 다른 모든 옵션 보다 우선 하 고 그 다음에 *ReadOnly*로 설정 됩니다. 옵션이 지정 되지 않은 경우 기본적으로 **Adlockbatchoptimistic** 을 사용 하 여 레코드 집합을 열고 숨겨진 열은 레코드 집합에 포함 되지 않습니다.  
  
 *pParameters*  
 매개 변수 정의의 안전 배열을 포함 하는 **Variant** 입니다. *Lexecuteoptions*에 *GetInfo* 옵션이 지정 된 경우이 매개 변수는 OLE DB 공급자에서 가져온 매개 변수 정의를 반환 하는 데 사용 됩니다. 그렇지 않으면이 매개 변수는 비어 있을 수 있습니다.  
  
 *lcid*  
 *Pinformation*에서 반환 되는 오류를 작성 하는 데 사용 되는 LCID입니다.  
  
 *pInformation*  
 Execute에서 반환 된 정보 오류에 대 한 포인터입니다. NULL 인 경우에는 오류 정보가 반환 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 *Handlerstring* 매개 변수는 null 일 수 있습니다. 이 경우에 발생 하는 상황은 RDS 서버를 구성 하는 방법에 따라 달라 집니다. "MSDFMAP. handler"의 처리기 문자열은 Microsoft에서 제공 하는 처리기 (Msdfmap .dll)를 사용 해야 함을 나타냅니다. "MASDFMAP, .sample"의 처리기 문자열은 Msdfmap .dll 처리기를 사용 해야 하며 "sample. .ini" 인수를 처리기에 전달 해야 함을 나타냅니다. MSDFMAP .dll은이 인수를 샘플 .ini를 사용 하 여 연결 및 쿼리 문자열을 확인 하는 방향으로 해석 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


