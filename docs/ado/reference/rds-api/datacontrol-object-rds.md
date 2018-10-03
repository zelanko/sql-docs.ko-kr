---
title: DataControl 개체 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e5c207a6928c82adeb8d45e22ea342bc40f0322
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798831"
---
# <a name="datacontrol-object-rds"></a>DataControl 개체(RDS)
데이터 쿼리에 바인딩하여 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 표시할 하나 이상의 컨트롤 (예: 텍스트 상자, 표 형태 컨트롤 또는 콤보 상자)에 **레코드 집합** 웹 페이지에서 데이터.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Remarks  
 에 대 한 클래스 ID를 **rds. DataControl** 개체가 BD96C556-65A3-11 D 0 983A 00C04FC29E33 합니다.  
  
> [!NOTE]
>  오류가 발생 하는 경우는 [rds. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 또는 **rds. DataControl** 개체가 로드으로 올바른 클래스 ID를 사용 하는 확인 되지 않으면 클래스는 이러한 개체에 대 한 Id 버전 1.0 및 1.1에서에서 변경 되었습니다. 또한를 사용 하는 경우에 null 허용 열을 설정할 수 해야 유의 해야 합니다 **RDS DataControl** 개체입니다.  
  
 기본 시나리오의 경우만 설정 해야 합니다 **SQL**, **Connect**, 및 **Server** 의 속성은 **rds. DataControl** 개체를 기본 비즈니스 개체를 자동으로 호출 합니다 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)합니다.  
  
 모든 속성은 **rds. DataControl** 는 사용자 지정 비즈니스 개체는 해당 기능을 바꿀 수 있으므로 선택 사항입니다.  
  
> [!NOTE]
>  여러 결과 쿼리 하는 경우 첫 번째 메시지만 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 반환 됩니다. 여러 개의 결과 집합이 필요한 경우 각각 자체에 할당할 **DataControl**합니다. 여러 결과 대 한 쿼리의 예는 다음과 같을 수 없습니다. `"Select * from Authors, Select * from Topics"`  
  
 추가 "DFMode = 20;"을 사용 하는 경우 연결 문자열을 **rds. DataControl** 개체 데이터를 업데이트할 때 서버의 성능을 개선할 수 있습니다. 이 설정을 사용 합니다 **업데이트할** 서버의 개체를 덜 리소스 집약적 모드를 사용 합니다. 그러나 다음과 같은 기능이이 구성에서 사용할 수 없습니다.  
  
-   매개 변수가 있는 쿼리를 사용합니다.  
  
-   호출 하기 전에 매개 변수 또는 열 정보를 가져오는 합니다 **Execute** 메서드.  
  
-   설정 **업데이트 &#40;transact** 하 **True**합니다.  
  
-   행 상태를 확인 합니다.  
  
-   호출 된 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드.  
  
-   (명시적 또는 자동으로)를 통해 새로 고침 합니다 [업데이트를 다시 동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 속성입니다.  
  
-   설정 **명령** 하거나 [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성입니다.  
  
-   사용 하 여 **adCmdTableDirect**합니다.  
  
 **rds. DataControl** 기본적으로 비동기 모드에서 실행 되는 개체입니다. 응용 프로그램에 대 한 동기 실행에 필요한 경우 설정 합니다 [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) 매개 변수를 **adcExecSync** 하며 [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) 같음매개변수**adcFetchUpFront**다음 예제에서와 같이 합니다.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 하나를 사용 하 여 **rds. DataControl** 단일 쿼리 결과를 컨트롤에 연결할 하나 이상의 시각적 개체입니다. 예를 들어, 코드 이름, 거주, 출생지, 수명 및 우선 순위 고객 상태와 같은 쿼리 요청 고객 데이터를 가정 합니다. 단일을 사용할 수 있습니다 **rds. DataControl** 고객 이름, 나가 및 영역 3 개의 별도 텍스트 상자에 표시할 개체 확인란; 고객 우선 순위 상태 및 그리드 컨트롤의 모든 데이터입니다.  
  
 사용 하 여 다른 **rds. DataControl** 여러 쿼리 결과를 컨트롤에 연결할 다른 시각적 개체입니다. 예를 들어, 고객에 대 한 정보를 하나의 쿼리 및 두 번째 쿼리는 고객이 구매한 상품에 대 한 정보를 사용 합니다. 세 개의 텍스트 상자 및 하나의 확인란을 그리드 컨트롤의 두 번째 쿼리의 결과에 첫 번째 쿼리의 결과 표시 하려고 합니다. 기본 비즈니스 개체를 사용 하는 경우 (**업데이트할**), 다음을 수행 해야 합니다.  
  
-   두 개의 추가 **rds. DataControl** 웹 페이지에는 개체입니다.  
  
-   각각에 대해 하나씩 두 개의 쓰기 쿼리 **SQL** 의 두 속성 **rds. DataControl** 개체입니다. 하나의 **rds. DataControl** 개체는 고객 정보를 요청 하는 SQL 쿼리를 포함 하는, 두 번째는 고객이 구매한 상품의 목록을 요청 하는 쿼리가 포함 됩니다.  
  
-   각 바인딩된 컨트롤의 OBJECT 태그를 각 시각적 컨트롤에 표시 하려는 데이터에 대 한 값을 설정 하려면 DATAFLD 값을 지정 합니다.  
  
 개수에 대 한 개수 제한은 없습니다 **rds. DataControl** 개체를 단일 웹 페이지에 개체 태그를 사용 하 여 포함할 수 있습니다.  
  
 정의 하는 경우는 **rds. DataControl** 웹 페이지에 개체를 사용 하 여 0이 아닌 **높이** 하 고 **너비** (하지 않으려면 공백 포함) 1 등의 값입니다.  
  
 원격 데이터 서비스에 대 한 클라이언트 구성 요소는 Internet Explorer 4.0;의 일부로 포함 이미 따라서 필요가 없습니다에서 코드 베이스 매개 변수를 포함 하 여 **rds. DataControl** 개체 태그입니다.  
  
 Internet Explorer 4.0 이상, 아파트 모델 컨트롤로 표시 된 경우에 ActiveX® 컨트롤과 HTML 컨트롤을 사용 하 여 데이터를 바인딩할 수 있습니다.  
  
> [!NOTE]
>  **Microsoft Visual Basic** 는 **rds. DataControl** 스크립팅에 대해 안전한 및 웹 기반 응용 프로그램 에서만 사용 됩니다. Visual Basic 클라이언트 응용 프로그램에 필요가 없습니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [DataControl 개체(RDS) 속성, 메서드 및 이벤트](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [DataControl 개체 예제(VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















