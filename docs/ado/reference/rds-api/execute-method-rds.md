---
title: "Execute 메서드 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 68796c4fa28d3ee553ccf7c44e9bbd9850f32fb7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-rds"></a>Execute 메서드 (RDS)
요청을 실행 하 고 2.5 이상 ADO에서 사용 하기 위해 ADO 레코드 집합을 만듭니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>매개 변수  
 *연결 문자열*  
 실행에는 요청을 보낼 위치 OLE DB 공급자에 연결 하는 데 사용 하는 문자열입니다. 처리기를 사용 하 여 지정 된 경우 *HandlerString* 편집 하거나 연결 문자열을 바꿀 수 있습니다.  
  
 *HandlerString*  
 이 실행에서 사용 되는 처리기를 식별 하는 두 부분 문자열입니다. 문자열에는 두 부분 포함 되어 있습니다. 첫 번째 부분은 사용할 처리기의 이름 (ProgID)을 포함 합니다. 두 번째 부분에는 처리기에 전달 될 인수를 포함 합니다. 인수 문자열 해석 되는 방식을 대 한 세부 정보를 각 처리기에 적용 됩니다. 두 부분 문자열에 쉼표의 첫 번째 인스턴스로 구분 됩니다. 인수 문자열 추가 쉼표를 포함할 수 있습니다. 인수는 선택적입니다.  
  
 *쿼리 문자열*  
 연결 문자열에 식별 되는 OLE DB 공급자에서 지 원하는 명령 언어에 사용 되는 명령입니다. SQL 기반 공급자에 대 한 *QueryString* 는 TRANSACT-SQL 명령 문이 포함 될 수 있지만 비 SQL 공급자 (예를 들어 MSDataShape)에 대 한이 아닐 수 있습니다는 [!INCLUDE[tsql](../../../includes/tsql_md.md)] 쿼리 문입니다.  
  
 처리기를 사용 하는 경우 처리기 alter 하거나 여기에 지정 된 값을 바꿀 수 있습니다. 예를 들어 처리기 대체 일반적으로 *QueryString* .ini 파일에서 쿼리 문자열을 사용 합니다. Msdfmap.ini 파일은 기본적으로 사용 됩니다.  
  
 *lFetchOptions*  
 비동기 인출의 유형을 나타냅니다.  
  
 자세한 내용은 참조 [FetchOptions 속성 (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)합니다.  
  
 *TableID*  
 A **Variant** 형식의 VT_EMPTY 또는 VT_BSTR 중 하나입니다. VT_EMPTY 유형의이 값이 있는 경우 무시 됩니다. 레코드 집합을 사용 하 여 만들어집니다 VT_BSTR 형식의 없으면 **adCmdTableDirect** 및 여기에 지정 된 값 및 *QueryString* 매개 변수가 무시 됩니다.  
  
 *lExecuteOptions*  
 실행 옵션의 비트 마스크:  
  
 1 =*ReadOnly* 레코드 집합 사용 하 여 열립니다 **adLockReadOnly**합니다.  
  
 2 =*NoBatch* 레코드 집합 사용 하 여 열립니다 **adLockOptimistic**합니다.  
  
 4 =*AllParamInfoSupplied* 호출자에 게 모든 매개 변수에 대 한 매개 변수 정보에 제공 됨을 보장 *pParameters*합니다.  
  
 8 =*GetInfo* 쿼리에 대 한 매개 변수 정보 OLE DB 공급자에서 가져오고는에서 반환 되는 *pParameters* 매개 변수입니다. 쿼리가 실행 되지 하 고 없는 레코드 집합이 반환 됩니다.  
  
 16 =*GetHiddenColumns* 레코드 집합 사용 하 여 열립니다 **adLockBatchOptimistic** 숨겨진된 열은 레코드 집합에 포함 됩니다.  
  
 *읽기 전용*, *NoBatch* 및 *GetHiddenColumns* 는 상호 배타적인 옵션; 하지만 그 중 하나 이상 설정 하는 오류를 생성 하지 않습니다. 여러 옵션이 설정 된 경우 *GetHiddenColumns* 우선 모든 다른 사용자 뒤 *ReadOnly*합니다. 레코드 집합을 사용 하 여 열릴 옵션이 기본적으로 지정 된 경우 **adLockBatchOptimistic** 숨겨진된 열은 레코드 집합에 포함 되어 있지 않습니다.  
  
 *pParameters*  
 A **Variant** 하는 매개 변수 정의의 안전 배열을 포함 합니다. 경우는 *GetInfo* 옵션에 지정 되었습니다 *lExecuteOptions*,이 매개 변수는 사용 하는 OLE DB 공급자에서 가져온 매개 변수 정의 반환 합니다. 그렇지 않으면이 매개 변수는 비어 있을 수 있습니다.  
  
 *lcid*  
 LCID 작성 하는 데에 반환 되는 모든 오류 *pInformation*합니다.  
  
 *pInformation*  
 실행에서 반환 된 정보 오류에 대 한 포인터입니다. NULL 인 경우에 오류 정보가 반환 됩니다.  
  
## <a name="remarks"></a>주의  
 *HandlerString* 매개 변수는 null 일 수 있습니다. 이 경우 어떻게 될까요 RDS 서버를 구성 하는 방법에 따라 달라 집니다. "MSDFMAP.handler" 처리기 문자열로 제공 하는 Microsoft 처리기 (Msdfmap.dll)을 사용 해야 함을 나타냅니다. "MASDFMAP.handler,sample.ini" 처리기 문자열로 Msdfmap.dll 처리기를 사용 해야 함을 "sample.ini" 인수를 처리기에 전달 해야 한다고 나타냅니다. MSDFMAP.dll는 인수를 사용 하 여 sample.ini 연결 및 쿼리 문자열을 검사 하는 방향으로 해석 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



