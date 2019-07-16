---
title: RDS 프로그래밍 모델 세부 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d7251e3a403168e8383e636a8e6b5f712b9f7bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922522"
---
# <a name="rds-programming-model-in-detail"></a>RDS 프로그래밍 모델 세부 정보
다음은 RDS 프로그래밍 모델의 주요 요소입니다.  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   이벤트  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 클라이언트 응용 프로그램 서버 및 서버 프로그램 호출을 지정 해야 합니다. 반환 시 응용 프로그램 서버 프로그램에 대 한 참조를 수신 하 고 서버 프로그램 자체인 것 처럼 참조를 처리할 수 있습니다.  
  
 RDS 개체 모델을 사용 하 여이 기능을 구현 합니다 [rds. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체입니다.  
  
 프로그램 식별자를 가진 서버 프로그램 지정 하거나 *ProgID*합니다. 서버에서 사용 합니다 *ProgID* 및 서버 컴퓨터의 레지스트리 실제 프로그램 시작에 대 한 정보를 찾을 수 있습니다.  
  
 RDS는 인터넷 또는 인트라넷; 원격 서버에서 서버 프로그램 인지에 따라 내부적으로 구분 작업을 수행합니다 로컬 영역 네트워크; 서버 또는 전혀 서버의 하지 않고 대신 로컬 동적 연결 라이브러리 (DLL). 이 구분 정보를 클라이언트와 서버 간에 교환 하는 방법과 클라이언트 응용 프로그램에 반환 하는 참조 형식에 실질적인 차이가 결정 합니다. 그러나 사용자의 관점에서이 구분은 특별 한 의미가 없습니다. 가장 중요 사용 가능한 프로그램 참조를 받게 됩니다.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS는 데이터 원본 및 반환에 대해 SQL 쿼리를 수행 하거나 기본 서버 프로그램을 제공을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 인수를 **레코드 집합** 개체 및 데이터 소스를 업데이트 합니다.  
  
 RDS 개체 모델을 사용 하 여이 기능을 구현 합니다 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다.  
  
 또한이 개체에 빈을 만드는 메서드를 **Recordset** 프로그래밍 방식으로 채울 수 있는 개체 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)), 및 변환 하기 위한 다른 메서드는 **레코드 집합**  웹 페이지를 작성 하는 텍스트 문자열에는 개체 ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 ADO를 사용 하 여 일부 표준 연결 및 명령 동작을 재정의할 수 있습니다 합니다 **업데이트할** 사용 하 여를 **DataFactory** 명령 처리기와 연결을 포함 하는 사용자 지정 파일 및 보안 매개 변수입니다.  
  
 서버 프로그램 라고 한 *비즈니스 개체*합니다. 복잡 한 데이터 액세스, 유효성 검사 및 등을 수행할 수 있는 사용자 고유의 사용자 지정 비즈니스 개체를 작성할 수 있습니다. 사용자 지정 비즈니스 개체를 작성 하는 경우에의 인스턴스를 만들 수 있습니다는 **업데이트할** 개체 및 사용자 고유의 작업을 수행 하는 일부 메서드를 사용 합니다.  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS의 기능을 결합 하는 수단을 제공 합니다 **rds. DataSpace** 및 **업데이트할**, 고도를 쉽게 사용할 수 있는 시각적 컨트롤이 사용 하도록 설정 합니다 **레코드 집합** 데이터 원본에서 쿼리를 통해 반환 되는 개체입니다. RDS를 자동으로 서버에 대 한 정보에 액세스 하 고 시각적 컨트롤에 표시 가능한 만큼 작업을 수행 하는 가장 일반적인 사례에 대해 시도 합니다.  
  
 RDS 개체 모델을 사용 하 여이 기능을 구현 합니다 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 **rds. DataControl** 에 두 가지 측면이 있습니다. 한 가지 측면인 데이터 원본에 적용 됩니다. 명령 및 연결 정보를 사용 하 여 설정 하는 경우는 **Connect** 및 **SQL** 의 속성을 **rds. DataControl**를 자동으로 사용 된 **rds. DataSpace** 기본값에 대 한 참조를 만들려면 **업데이트할** 개체입니다. 그런 다음 **업데이트할** 사용할지는 **연결** 데이터 원본에 연결을 사용 하 여 속성 값을 **SQL** 가져올 속성 값을  **레코드 집합** 데이터 원본에서 반환 된 **레코드 집합** 개체를 **rds. DataControl**합니다.  
  
 표시에 관련 된 두 번째 측면은 반환 된 **레코드 집합** 시각적 컨트롤에 대 한 정보입니다. 사용 하 여 시각적 컨트롤을 연결할 수는 **rds. DataControl** (바인딩 이라는 프로세스)에 연결 된 정보에 액세스할 수 잇습니다 **레코드 집합** 개체, Microsoft® Internet Explorer에서 웹 페이지에서 쿼리 결과 표시 합니다. 각 **rds. DataControl** 개체 하나에 바인딩합니다 **레코드 집합** 하나 이상의 visual 컨트롤 (예를 들어를 텍스트 상자, 콤보 상자, 표 형태 컨트롤, 및 등)는 단일 쿼리의 결과 나타내는 개체입니다. 둘 이상 있을 수 있습니다 **rds. DataControl** 각 페이지에는 개체입니다. 각 **rds. DataControl** 개체를 다른 데이터 원본에 연결 될 수 있으며 별도의 쿼리 결과 포함 합니다.  
  
 **rds. DataControl** 개체에는 탐색, 정렬 및 관련 된 행을 필터링 하기 위한 자체적인 방법이 **레코드 집합** 개체입니다. 이러한 메서드는 유사 하지만 동일 하지는 않습니다 ADO의 메서드에 **레코드 집합** 개체입니다.  
  
## <a name="events"></a>이벤트  
 RDS 두 ADO 이벤트 모델의 독립적인 자체 이벤트를 지원 합니다. 합니다 [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) 이벤트 라고 때마다는 **rds. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 속성 변경, 따라서 비동기 작업을 성공적으로 완료 되 면 알림 종료 되거나 오류가 발생 했습니다. 합니다 [onError](../../../ado/reference/rds-api/onerror-event-rds.md) 비동기 작업 중 오류가 발생 하는 경우에 이벤트는 오류가 발생할 때마다에 호출 됩니다.  
  
> [!NOTE]
>  RDS에 두 개의 추가 이벤트를 제공 하는 Microsoft Internet Explorer: **onDataSetChanged**를 나타내는 합니다 **레코드 집합** 기능 이지만 여전히 행 검색 및  **onDataSetComplete**를 나타내는 합니다 **레코드 집합** 행 검색을 마치면 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체를 사용 하 여 RDS 프로그래밍 모델](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 개체 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace 개체 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



