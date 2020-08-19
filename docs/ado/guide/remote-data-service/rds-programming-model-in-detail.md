---
description: RDS 프로그래밍 모델 세부 정보
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ad3cd950c958fce95c0264533040fbe9e1df634b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452125"
---
# <a name="rds-programming-model-in-detail"></a>RDS 프로그래밍 모델 세부 정보
다음은 RDS 프로그래밍 모델의 주요 요소입니다.  
  
-   RDS. 스페이스가  
  
-   RDSServer. DataFactory  
  
-   RDS. DataControl  
  
-   이벤트  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="rdsdataspace"></a>RDS. 스페이스가  
 클라이언트 응용 프로그램에서 호출할 서버 및 서버 프로그램을 지정 해야 합니다. 반환 시 응용 프로그램은 서버 프로그램에 대 한 참조를 받고 참조를 서버 프로그램 자체인 것 처럼 처리할 수 있습니다.  
  
 RDS 개체 모델은 Rds를 사용 하 여이 기능을 구현 합니다 [. 공간](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체입니다.  
  
 서버 프로그램은 프로그램 식별자 또는 *ProgID*를 사용 하 여 지정 됩니다. 서버는 *ProgID* 와 서버 컴퓨터의 레지스트리를 사용 하 여 시작할 실제 프로그램에 대 한 정보를 찾습니다.  
  
 RDS는 서버 프로그램이 인터넷 또는 인트라넷을 통해 원격 서버에 있는지 여부에 따라 내부적으로 구분 됩니다. 로컬 영역 네트워크의 서버 그렇지 않고 로컬 DLL (동적 연결 라이브러리)에 있는 서버에는 그렇지 않습니다. 이러한 구분은 클라이언트와 서버 간에 정보를 교환 하는 방법을 결정 하 고 클라이언트 응용 프로그램에 반환 되는 참조의 형식에 대 한 명백한 차이점을 만듭니다. 그러나 관점에서 이러한 구분은 특별 한 의미가 없습니다. 이는 사용 가능한 프로그램 참조를 수신 하는 것이 중요 합니다.  
  
## <a name="rdsserverdatafactory"></a>RDSServer. DataFactory  
 RDS는 데이터 원본에 대 한 SQL 쿼리를 수행 하 고 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 반환 하거나 **레코드 집합** 개체를 가져와 데이터 원본을 업데이트할 수 있는 기본 서버 프로그램을 제공 합니다.  
  
 RDS 개체 모델은 [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체를 사용 하 여이 기능을 구현 합니다.  
  
 또한이 개체에는 프로그래밍 방식으로 채울 수 있는 빈 **레코드 집합** 개체 ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md))와 **레코드 집합** 개체를 텍스트 문자열로 변환 하 여 웹 페이지를 빌드하는 데 사용할 수 있는 다른 방법 ([converttostring](../../../ado/reference/rds-api/converttostring-method-rds.md))이 있습니다.  
  
 ADO를 사용 하면 **DataFactory** 처리기 및 연결, 명령 및 보안 매개 변수를 포함 하는 사용자 지정 파일을 사용 하 여 **RDSServer. DataFactory** 의 표준 연결 및 명령 동작 중 일부를 재정의할 수 있습니다.  
  
 서버 프로그램을 *비즈니스 개체*라고도 합니다. 복잡 한 데이터 액세스, 유효성 검사 등을 수행할 수 있는 고유한 사용자 지정 비즈니스 개체를 작성할 수 있습니다. 사용자 지정 비즈니스 개체를 작성 하는 경우에도 **RDSServer** 개체의 인스턴스를 만들고 해당 메서드 중 일부를 사용 하 여 고유한 작업을 수행할 수 있습니다.  
  
## <a name="rdsdatacontrol"></a>RDS. DataControl  
 RDS는 Rds의 기능을 결합 하는 수단을 제공 합니다 **. ** RDSServer 및 **DataFactory**를 사용 하 여 시각적 컨트롤에서 데이터 원본의 쿼리에 의해 반환 되는 **레코드 집합** 개체를 쉽게 사용 하도록 할 수도 있습니다. RDS는 가장 일반적인 경우에서 서버에 대 한 정보에 대 한 액세스를 자동으로 얻고 시각적 컨트롤에 표시 하는 데 최대한 많은 작업을 시도 합니다.  
  
 RDS 개체 모델은 Rds를 사용 하 여이 기능을 구현 합니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 **RDS. DataControl** 에는 두 가지 측면이 있습니다. 데이터 소스와 관련 된 한 가지 측면이 있습니다. RDS의 **연결** 및 **SQL** 속성을 사용 하 여 명령 및 연결 정보를 설정 하는 경우 ** **즉, RDS가 자동으로 사용 됩니다 **. ** 기본 **RDSServer DataFactory** 개체에 대 한 참조를 만들기 위한 공간을 만듭니다. 그런 다음 **RDSServer DataFactory** 는 **connect** 속성 값을 사용 하 여 데이터 원본에 연결 하 고, **SQL** 속성 값을 사용 하 여 데이터 원본에서 **레코드 집합** 을 가져오고, **레코드 집합** 개체를 RDS로 반환 합니다. ** DataControl**.  
  
 두 번째 측면은 시각적 컨트롤에서 반환 된 **레코드 집합** 정보를 표시 하는 것과 관련이 있습니다. 시각적 컨트롤을 RDS와 연결할 수 있습니다 **. ** Microsoft® Internet Explorer의 웹 페이지에 쿼리 결과를 표시 하 고 연결 된 **레코드 집합** 개체의 정보에 대 한 액세스 권한을 얻을 수 있습니다. 각 **RDS. DataControl** 개체는 단일 쿼리의 결과를 나타내는 하나의 **레코드 집합** 개체를 하나 이상의 시각적 컨트롤 (예: 텍스트 상자, 콤보 상자, 그리드 컨트롤 등)에 바인딩합니다. 둘 이상의 RDS가 있을 수 있습니다 **. ** 각 페이지의 DataControl 개체입니다. 각 **RDS. DataControl** 개체는 다른 데이터 원본에 연결 하 고 별도의 쿼리 결과를 포함할 수 있습니다.  
  
 **RDS. 또한 DataControl** 개체에는 연결 된 **레코드 집합** 개체의 행을 탐색, 정렬 및 필터링 하는 고유한 메서드도 있습니다. 이러한 메서드는 비슷하지만 ADO **레코드 집합** 개체의 메서드와는 다릅니다.  
  
## <a name="events"></a>이벤트  
 RDS는 ADO 이벤트 모델과 독립적인 두 가지 자체 이벤트를 지원 합니다. [OnReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) 이벤트는 RDS가 될 때마다 호출 됩니다 **. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 속성이 변경 되어 비동기 작업이 성공적으로 완료, 종료 또는 오류가 발생 한 경우 사용자에 게 알립니다. [OnError](../../../ado/reference/rds-api/onerror-event-rds.md) 이벤트는 비동기 작업 중에 오류가 발생 하더라도 오류가 발생할 때마다 호출 됩니다.  
  
> [!NOTE]
>  Microsoft Internet Explorer는 두 개의 추가 이벤트를 RDS: **Ondatasetchanged**로 제공 합니다 .이는 **레코드 집합** 의 기능이 작동 하지만 행을 검색 하 고 있으며,이는 **레코드 집합** 에서 행 검색이 완료 되었음을 나타내는 **ondatasetchanged**입니다.  
  
## <a name="see-also"></a>참고 항목  
 [개체를 사용 하는 RDS 프로그래밍 모델](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 개체 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [스페이스 개체 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



