---
title: DataControl 개체 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88fa818b04e55e7d6ad8c8c1c8d984e5cd0680bf
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="datacontrol-object-rds"></a>DataControl 개체 (RDS)
데이터 쿼리 바인딩하여 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 표시 하려면 하나 이상의 컨트롤 (예: 텍스트 상자, 표 형태 컨트롤 또는 콤보 상자)에 **레코드 집합** 웹 페이지에는 데이터입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>주의  
 에 대 한 클래스 ID는 **.rds입니다 DataControl** 개체는 BD96C556-65A3-11 D 0 983A 00C04FC29E33 합니다.  
  
> [!NOTE]
>  오류가 발생 하는 경우는 [.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 또는 **.rds입니다 DataControl** 개체는 로드, 올바른 클래스 ID를 사용 하 고 있는지 확인 하지 클래스는 이러한 개체에 대 한 Id 버전 1.0 및 1.1에서에서 변경 되었습니다. 또한 사용 하는 경우에 null 허용 열을 설정할 수 해야 유의 해야 합니다는 **RDS DataControl** 개체입니다.  
  
 기본 시나리오에만 설정 해야는 **SQL**, **연결**, 및 **서버** 의 속성은 **.rds입니다 DataControl** 개체를 기본 비즈니스 개체를 자동으로 호출, [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)합니다.  
  
 모든 속성은 **.rds입니다 DataControl** 는 사용자 지정 비즈니스 개체의 기능을 바꿀 수 있으므로 선택 사항입니다.  
  
> [!NOTE]
>  여러 결과 쿼리 하는 경우 첫 번째 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 반환 됩니다. 여러 개의 결과 집합이 필요한 경우 자체에 각각 할당 **DataControl**합니다. 여러 결과 대 한 쿼리의 예는 다음 수 있습니다. `"Select * from Authors, Select * from Topics"`  
  
 추가 "DFMode = 20;" 연결 문자열을 사용 하는 경우에 **.rds입니다 DataControl** 데이터를 업데이트할 때 개체 서버의 성능을 향상 시킬 수 있습니다. 이 설정을 통해는 **업데이트할** 많이 모드를 사용 하는 서버에서 개체입니다. 그러나 다음과 같은 기능을이 구성에서 사용할 수 없습니다.  
  
-   매개 변수가 있는 쿼리를 사용 합니다.  
  
-   호출 하기 전에 매개 변수 또는 열 정보 가져오기는 **Execute** 메서드.  
  
-   설정 **업데이트 Transact** 를 **True**합니다.  
  
-   행 상태를 확인 합니다.  
  
-   호출 된 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
-   통해 명시적으로 이동해 왔거나 자동으로 새로 고치는 [업데이트 다시 동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 속성입니다.  
  
-   설정 **명령** 또는 [레코드 집합](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성입니다.  
  
-   사용 하 여 **adCmdTableDirect**합니다.  
  
 **.rds입니다 DataControl** 기본적으로 비동기 모드에서 실행 하는 개체입니다. 응용 프로그램에 대해 동기화 실행 해야 하는 경우에 설정 된 [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) 매개 변수를 **adcExecSync** 및 [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) 매개 변수를 **adcFetchUpFront**다음 예제에 나온 것 처럼 합니다.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 하나를 사용 하 여 **.rds입니다 DataControl** 단일 쿼리의 결과를 컨트롤에 연결할 하나 이상의 시각적 개체입니다. 예를 들어, 코드 이름, 거주지, 출생 위치, 나이, 및 우선 순위 고객 상태와 같은 쿼리 요청 고객 데이터를 가정 합니다. 단일을 사용할 수 있습니다 **.rds입니다 DataControl** ; 세 개의 별도 텍스트 상자에 고객의 이름, 나가 및 영역을 표시 하는 개체 확인란; 고객 우선 순위 상태 및 표 컨트롤에서 모든 데이터입니다.  
  
 사용 하 여 다른 **.rds입니다 DataControl** 여러 개의 쿼리 결과를 컨트롤에 연결할 다른 시각적 개체입니다. 예를 들어, 한 쿼리는 고객에 대 한 정보 및 두 번째 쿼리는 고객이 구매한 제품에 대 한 정보를 사용 합니다. 세 가지 텍스트 상자 및 하나의 확인란 및 표 형태 컨트롤에서 두 번째 쿼리의 결과에 첫 번째 쿼리의 결과 표시 하려고 합니다. 기본 비즈니스 개체를 사용 하는 경우 (**업데이트할**), 다음을 수행 해야 합니다.  
  
-   두 개의 추가 **.rds입니다 DataControl** 웹 페이지에는 개체입니다.  
  
-   각각에 대해 하나씩 두 개의 쓰기 쿼리 **SQL** 속성 두 **.rds입니다 DataControl** 개체입니다. 하나의 **.rds입니다 DataControl** 개체 고객 정보를 요청 하는 SQL 쿼리를 포함 됩니다; 두 번째는 고객이 구매한 제품 목록을 요청 하는 쿼리를 포함 합니다.  
  
-   바인딩된 각 컨트롤의 개체 태그에 시각적 각 컨트롤에 표시 하려는 데이터에 대 한 값을 설정 하려면 DATAFLD 값을 지정 합니다.  
  
 Count의 수에는 제한이 없으며 **.rds입니다 DataControl** 개체를 단일 웹 페이지에 개체 태그를 사용 하 여 포함할 수 있습니다.  
  
 정의 하는 경우는 **.rds입니다 DataControl** 웹 페이지에 개체를 가져오려면 0이 아닌 **높이** 및 **너비** (방지 하기 위해 추가 공간이 포함) 1 등의 값입니다.  
  
 원격 데이터 서비스 클라이언트 구성 요소가 이미 Internet Explorer 4.0;의 일부로 포함 되어 있습니다. 따라서 불필요에서 코드 베이스 매개 변수를 포함 하 여 **.rds입니다 DataControl** 태그 개체입니다.  
  
 Internet Explorer 4.0 이상, HTML 컨트롤 및 ActiveX® 컨트롤이 아파트 모델 컨트롤로 표시 된 경우에 사용 하 여 데이터에 바인딩할 수 있습니다.  
  
> [!NOTE]
>  **Microsoft Visual Basic 사용자** 는 **.rds입니다 DataControl** 를 안전 하 게 스크립트 및 웹 기반 응용 프로그램에만 사용 됩니다. Visual Basic 클라이언트 응용 프로그램에 필요 하지 않습니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [DataControl 개체(RDS) 속성, 메서드 및 이벤트](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [DataControl 개체 예제(VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















