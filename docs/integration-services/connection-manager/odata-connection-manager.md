---
title: OData 연결 관리자 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67bb8489c9dd702f26f8d17ec85e8f59f353476b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="odata-connection-manager"></a>OData 연결 관리자
 OData 연결 관리자를 사용하여 OData 데이터 원본에 연결합니다. OData 원본 구성 요소는 OData 연결 관리자를 사용하여 OData 데이터 원본에 연결하고 서비스에서 데이터를 사용합니다. 자세한 내용은 [OData Source](../../integration-services/data-flow/odata-source.md)를 참조하십시오.  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>SSIS 패키지에 OData 연결 관리자 추가  
 세 가지 방법으로 새로운 OData 연결 관리자를 SSIS 패키지에 추가할 수 있습니다.  
  
-   **새로 만들기...** 를 클릭합니다. 에서 **새로 만들기…**  
  
-   **솔루션 탐색기** 에서 **연결 관리자**폴더를 마우스 오른쪽 단추로 클릭하고 **새 연결 관리자**를 클릭합니다. **연결 관리자 유형** 에 대해 **ODATA**를 선택합니다.  
  
-   패키지 디자이너 아래쪽에서 **연결 관리자** 창을 마우스 오른쪽 단추로 클릭하고 **새 연결**을 선택합니다. **연결 관리자 유형** 에 대해 **ODATA**를 선택합니다.  
  
## <a name="connection-manager-authentication"></a>연결 관리자 인증  
 OData 연결 관리자는 5가지 모드의 인증을 지원합니다.  
  
-   Windows 인증  
  
-   기본 인증(사용자 이름 및 암호 사용)  

-   Microsoft Dynamics AX Online(사용자 이름 및 암호 사용)
  
-   Microsoft Dynamics CRM Online(사용자 이름 및 암호 사용)
  
-   Microsoft Online Services(사용자 이름 및 암호 사용)  
  
익명 액세스의 경우 Windows 인증 옵션을 선택합니다.  

Microsoft Dynamics AX Online 또는 Microsoft Dynamics CRM Online에 연결하기 위해 **Microsoft 온라인 서비스** 인증 옵션을 사용할 수 없습니다. 또한 다단계 인증에 대해 구성된 모든 옵션을 사용할 수 없습니다.
  
### <a name="specifying-and-securing-credentials"></a>자격 증명 지정 및 보안  
 OData 서비스에 기본 인증이 필요한 경우 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)에서 사용자 이름과 암호를 지정할 수 있습니다. 편집기에 입력한 값은 패키지에서 유지됩니다. 암호 값은 패키지 보호 수준에 따라 암호화됩니다.  
  
 여러 가지 방법으로 사용자 이름 및 암호 값을 매개 변수화하거나 패키지 외부에 저장할 수 있습니다. 예를 들어 SQL Server Management Studio에서 패키지를 실행할 때 매개 변수를 사용하거나 연결 관리자 속성을 직접 설정할 수 있습니다.  
  
## <a name="odata-connection-manager-properties"></a>OData 연결 관리자 속성  
 다음 목록에서는 OData 연결 관리자의 속성에 대해 설명합니다.  
  
|||  
|-|-|  
|속성|Description|  
|Url|서비스 문서에 대한 URL입니다.|  
|UserName|필요한 경우 인증에 사용할 사용자 이름입니다.|  
|암호|필요한 경우 인증에 사용할 암호입니다.|  
|ConnectionString|연결 관리자의 다른 속성을 포함합니다.|  
  
## <a name="odata-connection-manager-editor"></a>OData 연결 관리자 편집기
  **OData 연결 관리자 편집기** 대화 상자를 사용하여 OData 데이터 원본에 연결을 추가하거나 기존 연결을 편집할 수 있습니다.  
  
### <a name="options"></a>변수  
 **연결 관리자 이름**  
 연결 관리자의 이름입니다.  
  
 **서비스 문서 위치**  
 OData 서비스의 URL입니다. 예를 들어 http://services.odata.org/V3/Northwind/Northwind.svc/을 참조하십시오.  
  
 **인증**  
다음 옵션 중 하나를 선택합니다.
-   **Windows 인증** 익명 액세스의 경우 이 옵션을 선택합니다.
-   **기본 인증** 
-   Dynamics AX Online에 대한 **Microsoft Dynamics AX Online**
-   Dynamics CRM Online에 대한 **Microsoft Dynamics CRM Online**
-   Microsoft Online Services에 대한 **Microsoft Online Services**

Windows 인증 이외의 옵션을 선택하는 경우 **사용자 이름** 및 **암호**를 입력합니다. 

Microsoft Dynamics AX Online 또는 Microsoft Dynamics CRM Online에 연결하기 위해 **Microsoft 온라인 서비스** 인증 옵션을 사용할 수 없습니다. 또한 다단계 인증에 대해 구성된 모든 옵션을 사용할 수 없습니다.

 **연결 테스트**  
 OData 원본에 대한 연결을 테스트하려면 이 단추를 클릭합니다.  
