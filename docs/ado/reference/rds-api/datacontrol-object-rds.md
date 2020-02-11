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
ms.openlocfilehash: a571e93a070c3ce07fbaf40a86b762c749042ec1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964396"
---
# <a name="datacontrol-object-rds"></a>DataControl 개체(RDS)
텍스트 상자, 표 형태 컨트롤 또는 콤보 상자와 같은 하나 이상의 컨트롤에 데이터 쿼리 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 바인딩하여 웹 페이지에 **레코드 집합** 데이터를 표시 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>설명  
 RDS의 클래스 ID **입니다. DataControl** 개체는 BD96C556-65A3-11D0-983A-00C04FC29E33입니다.  
  
> [!NOTE]
>  오류가 발생 [하는 경우 ](../../../ado/reference/rds-api/dataspace-object-rds.md) **합니다. DataControl** 개체가 로드 되지 않습니다. 올바른 클래스 ID를 사용 하 고 있는지 확인 하십시오. 이러한 개체의 클래스 Id는 1.0 및 1.1 버전에서 변경 되었습니다. 또한 **RDS DataControl** 개체를 사용 하는 경우에도 nullable 열을 설정 해야 합니다.  
  
 기본적인 시나리오의 경우 RDS의 **SQL**, **Connect**및 **서버** 속성만 설정 해야 합니다 **. **기본 비즈니스 개체 [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)를 자동으로 호출 하는 DataControl 개체입니다.  
  
 RDS의 모든 속성 ** **사용자 지정 비즈니스 개체가 해당 기능을 대체할 수 있으므로 DataControl은 선택 사항입니다.  
  
> [!NOTE]
>  여러 결과를 쿼리 하는 경우 첫 번째 [레코드](../../../ado/reference/ado-api/recordset-object-ado.md) 집합만 반환 됩니다. 여러 결과 집합이 필요한 경우에는 각각의 **DataControl**에 할당 합니다. 여러 결과에 대 한 쿼리의 예는 다음과 같습니다.`"Select * from Authors, Select * from Topics"`  
  
 RDS를 사용할 때 연결 문자열에 "DFMode = 20;"을 추가 **합니다. DataControl** 개체는 데이터를 업데이트할 때 서버 성능을 향상 시킬 수 있습니다. 이 설정을 사용 하는 경우 서버의 **RDSServer DataFactory** 개체는 리소스를 많이 사용 하는 모드를 사용 합니다. 그러나이 구성에서는 다음과 같은 기능을 사용할 수 없습니다.  
  
-   매개 변수가 있는 쿼리 사용.  
  
-   **Execute** 메서드를 호출 하기 전에 매개 변수 또는 열 정보를 가져옵니다.  
  
-   **Transact-sql 업데이트** 를 **True**로 설정 합니다.  
  
-   행 상태를 가져오는 중입니다.  
  
-   [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드를 호출 합니다.  
  
-   [업데이트 다시 동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 속성을 통해 (명시적 또는 자동으로) 새로 고침  
  
-   **명령** 또는 [레코드 집합](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성을 설정 합니다.  
  
-   **AdCmdTableDirect**사용.  
  
 **RDS. DataControl** 개체는 기본적으로 비동기 모드에서 실행 됩니다. 응용 프로그램에 대해 동기화를 실행 해야 하는 경우 다음 예제와 같이 [executeoptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) 매개 변수를 **Adcexecsync** 와 동일 하 게 설정 하 고 [Fetchoptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) 매개 변수를 **adcexecsync**으로 설정 합니다.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 하나의 **RDS를 사용 합니다. **단일 쿼리의 결과를 하나 이상의 시각적 컨트롤에 연결 하는 DataControl 개체입니다. 예를 들어 이름, 거주지, 생년월일, 연령 및 우선 순위 고객 상태와 같은 고객 데이터를 요청 하는 쿼리를 코딩 한다고 가정 합니다. 단일 RDS를 사용할 수 있습니다 **. **3 개의 개별 텍스트 상자에 고객의 이름, 나이 및 지역을 표시 하는 DataControl 개체입니다. 확인란의 우선 순위 고객 상태 표 컨트롤의 모든 데이터입니다.  
  
 다른 **RDS를 사용 합니다. **여러 쿼리 결과를 다양 한 시각적 컨트롤에 연결 하는 DataControl 개체입니다. 예를 들어 하나의 쿼리를 사용 하 여 고객에 대 한 정보를 얻고 고객이 구매한 상품에 대 한 정보를 가져오는 두 번째 쿼리를 사용 한다고 가정 합니다. 첫 번째 쿼리 결과를 세 개의 텍스트 상자와 하나의 확인란으로 표시 하 고 두 번째 쿼리의 결과를 grid 컨트롤에 표시 하려고 합니다. 기본 비즈니스 개체 (**RDSServer. DataFactory**)를 사용 하는 경우 다음을 수행 해야 합니다.  
  
-   두 개의 **RDS를 추가 합니다. **웹 페이지에 대 한 DataControl 개체  
  
-   두 RDS의 각 **SQL** 속성에 대해 하나씩, 두 개의 쿼리를 작성 **합니다. DataControl** 개체. **RDS 하나 DataControl** 개체는 고객 정보를 요청 하는 SQL 쿼리를 포함 합니다. 두 번째는 고객이 구매한 상품 목록을 요청 하는 쿼리를 포함 합니다.  
  
-   각 바인딩된 컨트롤의 개체 태그에서 DATAFLD 값을 지정 하 여 각 시각적 컨트롤에 표시 하려는 데이터의 값을 설정 합니다.  
  
 RDS 수에 대 한 개수 제한은 없습니다 **. **단일 웹 페이지에서 개체 태그를 사용 하 여 포함할 수 있는 DataControl 개체입니다.  
  
 RDS를 정의할 때 ** DataControl** 개체 웹 페이지의 0이 아닌 **높이** 및 **너비** 값 (추가 공간이 포함 되지 않도록 하려면 1)을 사용 합니다.  
  
 원격 데이터 서비스 클라이언트 구성 요소가 이미 Internet Explorer 4.0의 일부로 포함 되어 있습니다. 따라서 RDS에 CODEBASE 매개 변수를 포함할 필요가 없습니다 **. DataControl** 개체 태그입니다.  
  
 Internet Explorer 4.0 이상에서는 아파트 모델 컨트롤로 표시 된 경우에만 HTML 컨트롤과 ActiveX® 컨트롤을 사용 하 여 데이터에 바인딩할 수 있습니다.  
  
> [!NOTE]
>  **Microsoft Visual Basic 사용자** **RDS. DataControl** 은 스크립팅에 안전 하며 웹 기반 응용 프로그램 에서만 사용 됩니다. Visual Basic 클라이언트 응용 프로그램은 필요 하지 않습니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [DataControl 개체(RDS) 속성, 메서드 및 이벤트](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataControl 개체 예제(VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















