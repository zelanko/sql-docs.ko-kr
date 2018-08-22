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
ms.openlocfilehash: ad55d02436d5d2ef0667e1b444ab68da5c526f46
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40393236"
---
# <a name="execute21-method-rds"></a>Execute21 메서드(RDS)
요청을 실행 하 고 ADO 2.1의에서 사용에 대 한 ADO 레코드 집합을 만듭니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 실행 된 요청을 보낼 OLE DB 공급자에 연결할 때 사용 하는 문자열입니다. 처리기를 사용 하 여 지정 된 경우 *HandlerString*, 편집 또는 연결 문자열을 바꿀 수 있습니다.  
  
 *HandlerString*  
 이 실행에 사용할 처리기를 식별 하는 문자열입니다. 문자열에 두 가지 파트가 있습니다. 첫 번째 부분에 사용할 처리기의 이름을 (progid 프로그램) 포함 되어 있습니다. 두 번째 부분 문자열의 처리기에 전달할 인수를 포함 합니다. 인수 문자열 해석 되는 방법을 하는 것은 특정 처리기입니다. 두 부분 (인수 문자열 추가 쉼표를 포함할 수 있음) 되지만 첫 번째 인스턴스의 문자열의 쉼표로 구분 됩니다. 인수는 선택적입니다.  
  
 *QueryString*  
 연결 문자열에 나오는 OLE DB 공급자가 지 원하는 명령 언어에 사용 되는 명령입니다. SQL 기반 공급자에 포함 될 수 있습니다는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령 문 하지만 비 SQL 공급자 (예를 들어 MSDataShape)에 대 한이 아닐 수 있습니다는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리 문입니다.  
  
 또한 처리기를 사용 하 되 고 (및 처리기를 사용할 것이 좋습니다) 하는 경우 처리기를 변경 하거나 바꿀 수 있습니다 여기에 지정 된 값. 예를 들어 처리기 대체 일반적으로 *QueryString* .ini 파일에서 쿼리 문자열을 사용 하 여 합니다. Msdfmap.ini 파일은 기본적으로 사용 됩니다.  
  
 *lMarshalOptions*  
 반환 되는 행 집합/recordset에서 마샬링 옵션을 설정 하는 데 사용 합니다.  
  
 *TableID*  
 변형은 VT_EMPTY 또는 VT_BSTR를 입력 합니다. 이 값 VT_EMPTY 유형의 경우 무시 됩니다. 레코드 집합을 사용 하 여 만들어집니다 VT_BSTR 형식의 경우 **adCmdTableDirect** 여기 지정 된 값을 사용 하 고 *QueryString* 매개 변수가 무시 됩니다.  
  
 *lExecuteOptions*  
 실행 옵션의 비트 마스크:  
  
 1 =*읽기 전용* 레코드 집합을 사용 하 여 열릴 **adLockReadOnly**합니다.  
  
 2 =*NoBatch* 레코드 집합을 사용 하 여 열릴 **adLockOptimistic**합니다.  
  
 4 =*AllParamInfoSupplied* 호출자에 게 모든 매개 변수에 대 한 매개 변수 정보에 제공 되는 보장 *pParameters*합니다.  
  
 8 =*GetInfo* 쿼리에 대 한 매개 변수 정보는 OLE DB 공급자에서 가져온 되며 반환 된 *pParameters* 매개 변수입니다. 쿼리가 실행 되지 않습니다 하 고 없는 레코드 집합이 반환 됩니다.  
  
 16 = 레코드 집합을 사용 하 여 열릴 GetHiddenColumns **adLockBatchOptimistic** 있으며 숨겨진된 열은 레코드 집합에 포함 됩니다.  
  
 하지만 *읽기 전용*를 *NoBatch* 및 *GetHiddenColumns* 상호 배타적인 옵션은 하나 이상의 오류가 아닙니다. 여러 옵션을 설정 하는 경우 *GetHiddenColumns* 뒤에 다른 모든 옵션 보다 우선 *ReadOnly*합니다. 기본적으로 없음 옵션을 지정 하는 레코드를 사용 하 여 열려 **adLockBatchOptimistic** 되지만 숨겨진된 열은 레코드 집합에 포함 되지 않습니다.  
  
 *pParameters*  
 매개 변수 정의의 안전 배열을 포함 하는 variant입니다. 경우는 *GetInfo* 옵션에 지정 되었습니다 *lExecuteOptions*,이 매개 변수를 사용 하 여 OLE DB 공급자에서 가져온 매개 변수 정의 반환 하 합니다. 그렇지 않으면이 매개 변수는 빈 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 *HandlerString* 매개 변수는 null 일 수 있습니다. 이 경우 생기는 RDS 서버를 구성 하는 방법에 따라 달라 집니다. "MSDFMAP.handler" 처리기 문자열 (Msdfmap.dll) Microsoft 제공 된 처리기를 사용 해야 함을 나타냅니다. "MASDFMAP.handler,sample.ini" 처리기 문자열 Msdfmap.dll 처리기를 사용 해야 함을 나타내고 "sample.ini" 인수는 처리기에 전달 해야 합니다. MSDFMAP.dll는 인수를 사용 하 여 sample.ini 연결 및 쿼리 문자열은 확인 방향으로 해석 합니다.  
  
> [!NOTE]
>  **Execute21** 메서드 버전이 합니다 [Execute 메서드 (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)합니다. 사용 해야 합니다 **Execute** 2.1, ADO와 통신 하는 방법 합니다 **Execute21** 메서드를 대신 호출할 수 있습니다. 기능을 **Execute** ADO 2.5 이상에서 메서드는 ADO 2.1의에서 동일한 메서드에 대해 제공 된 기능의 하위 집합입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


