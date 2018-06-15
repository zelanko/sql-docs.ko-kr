---
title: RDS 프로그래밍 모델을 상세히 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcfed19cda8ce9675b656add6f1a15e0912efe31
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274432"
---
# <a name="rds-programming-model-in-detail"></a>RDS 프로그래밍 모델 세부 정보
다음은 RDS 프로그래밍 모델의 주요 요소입니다.  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   이벤트  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 클라이언트 응용 프로그램 서버 및 서버 프로그램 호출을 지정 해야 합니다. 응용 프로그램 서버 프로그램에 대 한 참조를 수신 하 고 마치 서버 프로그램 자체인 것 처럼 참조를 처리할 수 있습니다.  
  
 RDS 개체 모델에는이 기능을 구체화는 [.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체입니다.  
  
 프로그램 식별자를 가진 지정 된 서버 프로그램 또는 *ProgID*합니다. 서버에서 사용 하는 *ProgID* 및 서버 컴퓨터의 레지스트리 실제 프로그램을 시작 하는 방법에 대 한 정보를 찾을 수 있습니다.  
  
 RDS 구분 인터넷 이나 인트라넷;를 통해 원격 서버에 서버 프로그램 인지에 따라 내부적으로 작업을 수행합니다 local area network;에 서버 또는 전혀, 서버의 하지 않고 대신 로컬 동적 연결 라이브러리 (DLL)에 합니다. 이러한 구분 정보가 클라이언트와 서버 사이 교환 되는 방법과 클라이언트 응용 프로그램에 반환 하는 참조의 유형 유형 달라 집니다 결정 합니다. 그러나 사용자의 관점에서 이러한 구분이 특별 한 의미가 없습니다. 중요 한 모든 사용 가능한 프로그램 참조를 나타나는입니다.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS 제공 데이터 원본 및 반환에 대 한 SQL 쿼리를 수행 하거나 기본 서버 프로그램은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 걸릴 또는 개체는 **레코드 집합** 개체 및 데이터 소스를 업데이트 합니다.  
  
 RDS 개체 모델에는이 기능을 구체화는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다.  
  
 또한이 개체에는 빈을 만드는 방법을 **레코드 집합** 프로그래밍 방식으로 채울 수 있는 개체 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)), 및 변환 하는 다른 방법은 **레코드 집합**  개체에는 웹 페이지에 텍스트 문자열 ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Ado, 일부 표준 연결 및 명령 동작을 재정의할 수 있습니다는 **업데이트할** 와 **DataFactory** 명령 처리기와 연결을 포함 하는 사용자 지정 파일 및 보안 매개 변수입니다.  
  
 서버 프로그램 라고도 *비즈니스 개체*합니다. 복잡 한 데이터 액세스, 유효성 검사 및 등을 수행할 수 있는 사용자 지정 비즈니스 개체를 작성할 수 있습니다. 인스턴스를 만들 수 있는 사용자 지정 비즈니스 개체를 작성 하는 경우에 프로그램 **업데이트할** 개체 및 해당 메서드 중 일부를 사용 하 여 사용자 고유의 작업을 수행 합니다.  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS의 기능을 결합 하는 수단을 제공 된 **.rds입니다 DataSpace** 및 **업데이트할**, 쉽게 사용할 수 있는 시각적 컨트롤을 사용 하도록 설정할 수도 및는 **레코드 집합** 데이터 원본에서 쿼리가 반환 하는 개체입니다. 자동으로 서버에 대 한 정보에 액세스 하 고 시각적 컨트롤에 표시 가능한 한 작업을 수행 하는 가장 일반적인 경우에 대 한 RDS 시도 합니다.  
  
 RDS 개체 모델에는이 기능을 구체화는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 **.rds입니다 DataControl** 두 가지 측면이 있습니다. 한 가지 측면인 데이터 소스에 적용 됩니다. 명령 및 사용 하 여 연결 정보를 설정 하는 경우는 **연결** 및 **SQL** 의 속성은 **.rds입니다 DataControl**, 자동으로 사용 됩니다는 **.rds입니다 DataSpace** 기본값에 대 한 참조를 만들려면 **업데이트할** 개체입니다. 그런 다음 **업데이트할** ´ ֲ는 **연결** 속성 값을 사용 하 여 데이터 원본에 연결 하려면는 **SQL** 속성 값을 가져오는 한  **레코드 집합** 데이터 원본과 반환 된 **레코드 집합** 개체는 **.rds입니다 DataControl**합니다.  
  
 두 번째 측면은 표시 되는 관련 반환 된 **레코드 집합** 시각적 컨트롤에 대 한 정보입니다. 시각적 컨트롤과 연결할 수 있습니다는 **.rds입니다 DataControl** (에 프로세스 바인딩)은 연결 된 정보에 액세스 하 고 **레코드 집합** 개체, Microsoft® Internet Explorer에서 웹 페이지에서 쿼리 결과 표시 합니다. 각 **.rds입니다 DataControl** 개체 하나에 바인딩합니다 **레코드 집합** 하나 이상의 컨트롤 (예를 들어, 한 입력란, 콤보 상자, 표 형태 컨트롤 등)는 단일 쿼리의 결과 나타내는 개체입니다. 여러 개 있을 수 있습니다 **.rds입니다 DataControl** 각 페이지에는 개체입니다. 각 **.rds입니다 DataControl** 개체는 다른 데이터 원본에 연결할 수와 별도의 쿼리 결과 포함 합니다.  
  
 **.rds입니다 DataControl** 개체에는 탐색, 정렬 및 관련 된 행을 필터링 하기 위한 고유한 메서드 **레코드 집합** 개체입니다. 이러한 메서드는 비슷하지만, ADO에서 메서드로 동일 하지만 **레코드 집합** 개체입니다.  
  
## <a name="events"></a>이벤트  
 RDS 자체 이벤트는 ADO 이벤트 모델의 독립적인 두 지원 합니다. [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) 이벤트가 호출 될 때마다는 **.rds입니다 DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 속성이 변경 되므로 사용자에 게 알리는 비동기 작업이 완료 된 경우 종료 되거나 오류가 발생 했습니다. [onError](../../../ado/reference/rds-api/onerror-event-rds.md) 는 비동기 작업 중에 오류가 발생 하는 경우에 이벤트는 오류가 발생할 때마다에 호출 됩니다.  
  
> [!NOTE]
>  RDS에 두 개의 추가 이벤트를 제공 하는 Microsoft Internet Explorer: **onDataSetChanged**, 않는다는 의미는 **레코드 집합** 기능 이지만 여전히 행 검색 및  **onDataSetComplete**, 않는다는 의미는 **레코드 집합** 행 검색을 완료 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 프로그래밍 모델 개체와 사용](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 개체 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [데이터 공간 개체 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



