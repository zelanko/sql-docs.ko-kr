---
title: Execute21 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bfe6de22f60ff43ab41144f0ee2e6e0fbb667766
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288332"
---
# <a name="execute21-method-rds"></a>Execute21 메서드 (RDS)
요청을 실행 하 고 ADO 2.1에서에서 사용 하기 위해 ADO 레코드 집합을 만듭니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 실행에는 요청을 보낼 위치 OLE DB 공급자에 연결 하는 데 사용 하는 문자열입니다. 처리기를 사용 하 여 지정 된 경우 *HandlerString*, 편집 하거나 연결 문자열을 바꿀 수 있습니다.  
  
 *HandlerString*  
 문자열이이 실행에서 사용 되는 처리기를 식별 합니다. 문자열에는 두 부분 포함 되어 있습니다. 첫 번째 부분은 사용할 처리기의 이름 (ProgID)을 포함 합니다. 두 번째 부분 문자열의 처리기에 전달 될 인수를 포함 합니다. 인수 문자열 해석 되는 방식을 특정 처리기입니다. 두 부분 (하지만 인수 문자열 추가 쉼표를 포함할 수 있음) 첫 번째 인스턴스의 문자열의 쉼표로 구분 됩니다. 인수는 선택적입니다.  
  
 *QueryString*  
 연결 문자열에 식별 되는 OLE DB 공급자에서 지 원하는 명령 언어에 사용 되는 명령입니다. SQL 기반 공급자에 대 한 포함 될 수 있습니다는 [!INCLUDE[tsql](../../../includes/tsql_md.md)] 명령 문 하지만 비 SQL 공급자 (예를 들어 MSDataShape)에 대 한이 아닐 수 있습니다는 [!INCLUDE[tsql](../../../includes/tsql_md.md)] 쿼리 문입니다.  
  
 또한 경우 사용 되는 처리기 (좋습니다 처리기를 사용할 수), 처리기 하거나 변경할 수 여기에서 지정 된 값을 대체 합니다. 예를 들어 처리기 대체 일반적으로 *QueryString* .ini 파일에서 쿼리 문자열을 사용 합니다. Msdfmap.ini 파일은 기본적으로 사용 됩니다.  
  
 *lMarshalOptions*  
 반환 되는 행 집합/recordset 마샬링 옵션을 설정 하는 데 사용 합니다.  
  
 *TableID*  
 변수는 VT_EMPTY 또는 VT_BSTR를 입력 합니다. VT_EMPTY 유형의이 값이 있는 경우 무시 됩니다. VT_BSTR 형식의 경우 레코드 집합 사용 하 여 만들어집니다 **adCmdTableDirect** 여기에 지정 된 값을 사용 하 고 *QueryString* 매개 변수가 무시 됩니다.  
  
 *lExecuteOptions*  
 실행 옵션의 비트 마스크.  
  
 1 =*ReadOnly* 레코드 집합 사용 하 여 열립니다 **adLockReadOnly**합니다.  
  
 2 =*NoBatch* 레코드 집합 사용 하 여 열립니다 **adLockOptimistic**합니다.  
  
 4 =*AllParamInfoSupplied* 호출자에 게 모든 매개 변수에 대 한 매개 변수 정보에 제공 됨을 보장 *pParameters*합니다.  
  
 8 =*GetInfo* 쿼리에 대 한 매개 변수 정보 OLE DB 공급자에서 가져오고는에서 반환 되는 *pParameters* 매개 변수입니다. 쿼리가 실행 되지 하 고 없는 레코드 집합이 반환 됩니다.  
  
 16 =를 사용 하 여 레코드 집합 열립니다 GetHiddenColumns **adLockBatchOptimistic** 숨겨진된 열은 레코드 집합에 포함 됩니다.  
  
 하지만 *ReadOnly*, *NoBatch* 및 *GetHiddenColumns* 상호 배타적인 옵션은 둘 중 하나 이상 설정 하려면 오류로 간주 되지 않습니다. 여러 옵션이 설정 된 경우 *GetHiddenColumns* 뒤, 다른 모든 옵션 보다 우선 *ReadOnly*합니다. 레코드 집합을 사용 하 여 열릴 옵션이 기본적으로 지정 된 경우 **adLockBatchOptimistic** 있지만 숨겨진된 열은 레코드 집합에 포함 되지 않습니다.  
  
 *pParameters*  
 매개 변수 정의의 안전 배열을 포함 하는 variant입니다. 경우는 *GetInfo* 옵션에 지정 되었습니다 *lExecuteOptions*,이 매개 변수는 사용 하는 OLE DB 공급자에서 가져온 매개 변수 정의 반환 합니다. 그렇지 않으면이 매개 변수는 비어 있을 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 *HandlerString* 매개 변수는 null 일 수 있습니다. 이 경우 수행 해야 할 작업 RDS 서버를 구성 하는 방법에 따라 달라 집니다. "MSDFMAP.handler" 처리기 문자열로 제공 하는 Microsoft 처리기 (Msdfmap.dll)을 사용 해야 함을 나타냅니다. "MASDFMAP.handler,sample.ini" 처리기 문자열로 Msdfmap.dll 처리기를 사용 해야 함을 "sample.ini" 인수를 처리기에 전달 해야 한다고 나타냅니다. MSDFMAP.dll는 인수를 사용 하 여 sample.ini 연결 및 쿼리 문자열을 검사 하는 방향으로 해석 합니다.  
  
> [!NOTE]
>  **Execute21** 메서드는 버전의는 [Execute 메서드 (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)합니다. 사용 해야는 **Execute** 2.1, ADO와 통신 하는 메서드는 **Execute21** 메서드를 대신 호출할 수 있습니다. 기능은 **Execute** ADO 2.5 이상에서 메서드는 ado 2.1 동일한 메서드에 제공 된 기능의 상위 집합입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


