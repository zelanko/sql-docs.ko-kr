---
title: "OData 연결 관리자 | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: f54562b59e8c61f723c17e2812ca39cb2e95f273
ms.contentlocale: ko-kr
ms.lasthandoff: 08/28/2017

---
# <a name="odata-connection-manager"></a>OData 연결 관리자
 OData 연결 관리자와 OData 데이터 원본에 연결 합니다. OData 원본 구성 요소는 OData 연결 관리자를 사용 하 여 OData 데이터 원본에 연결 하 고 데이터 서비스를 사용 합니다. 자세한 내용은 [OData Source](../../integration-services/data-flow/odata-source.md)를 참조하십시오.  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>SSIS 패키지에 OData 연결 관리자 추가  
 세 가지 방법으로 SSIS 패키지에는 새 OData 연결 관리자를 추가할 수 있습니다.  
  
-   **새로 만들기...**를 클릭합니다. 에서 **새로 만들기…**  
  
-   **솔루션 탐색기** 에서 **연결 관리자**폴더를 마우스 오른쪽 단추로 클릭하고 **새 연결 관리자**를 클릭합니다. **연결 관리자 유형** 에 대해 **ODATA**를 선택합니다.  
  
-   마우스 오른쪽 단추로 클릭는 **연결 관리자** 패키지 디자이너를 선택한 다음 아래쪽 창에 **새 연결**합니다. **연결 관리자 유형** 에 대해 **ODATA**를 선택합니다.  
  
## <a name="connection-manager-authentication"></a>연결 관리자 인증  
 OData 연결 관리자는 5 개 모드의 인증을 지원합니다.  
  
-   Windows 인증  
  
-   기본 인증(사용자 이름 및 암호 사용)  

-   Microsoft Dynamics AX Online(사용자 이름 및 암호 사용)
  
-   Microsoft Dynamics CRM Online(사용자 이름 및 암호 사용)
  
-   Microsoft Online Services(사용자 이름 및 암호 사용)  
  
익명 액세스의 경우 Windows 인증 옵션을 선택합니다.  

온라인 Microsoft Dynamics AX Online 또는 Microsoft Dynamics CRM에 연결 하는 데 사용할 수 없습니다는 **Microsoft 온라인 서비스** 인증 옵션입니다. 또한 다단계 인증에 대 한 모든 구성 된 옵션을 사용할 수 없습니다.
  
### <a name="specifying-and-securing-credentials"></a>자격 증명 지정 및 보안  
 OData 서비스에 기본 인증이 필요한 경우 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)에서 사용자 이름과 암호를 지정할 수 있습니다. 편집기에 입력한 값은 패키지에서 유지됩니다. 암호 값은 패키지 보호 수준에 따라 암호화됩니다.  
  
 여러 가지 방법으로 사용자 이름 및 암호 값을 매개 변수화하거나 패키지 외부에 저장할 수 있습니다. 예를 들어 연결 관리자 속성을 설정할 직접 SQL Server Management Studio에서 패키지를 실행 하는 경우 또는 매개 변수를 사용할 수 있습니다.  
  
## <a name="odata-connection-manager-properties"></a>OData 연결 관리자 속성  
 다음 목록에는 OData 연결 관리자의 속성을 설명 합니다.  
  
|||  
|-|-|  
|속성|Description|  
|Url|서비스 문서에 대한 URL입니다.|  
|UserName|필요한 경우 인증에 사용할 사용자 이름입니다.|  
|암호|필요한 경우 인증에 사용할 암호입니다.|  
|ConnectionString|연결 관리자의 다른 속성을 포함합니다.|  
  
## <a name="odata-connection-manager-editor"></a>OData 연결 관리자 편집기
  사용 하 여는 **OData 연결 관리자 편집기** 대화 상자를 OData 데이터 원본에 기존 연결을 편집 하거나 연결을 추가 합니다.  
  
### <a name="options"></a>옵션  
 **연결 관리자 이름**  
 연결 관리자의 이름입니다.  
  
 **서비스 문서 위치**  
 OData 서비스의 URL입니다. 예를 들어: http://services.odata.org/V3/Northwind/Northwind.svc/입니다.  
  
 **인증**  
다음 옵션 중 하나를 선택합니다.
-   **Windows 인증**합니다. 익명 액세스에 대 한이 옵션을 선택 합니다.
-   **기본 인증** 
-   **Microsoft Dynamics AX, 온라인** Dynamics AX 온라인에 대 한
-   **Microsoft Dynamics CRM Online** Dynamics CRM Online에 대 한
-   **Microsoft 온라인 서비스** Microsoft 온라인 서비스에 대 한

Windows 인증 이외의 옵션을 선택 하는 경우 입력은 **사용자 이름** 및 **암호**합니다. 

온라인 Microsoft Dynamics AX Online 또는 Microsoft Dynamics CRM에 연결 하는 데 사용할 수 없습니다는 **Microsoft 온라인 서비스** 인증 옵션입니다. 또한 다단계 인증에 대 한 모든 구성 된 옵션을 사용할 수 없습니다.

 **연결 테스트**  
 OData 원본에 대 한 연결을 테스트 하려면이 단추를 클릭 합니다.  

