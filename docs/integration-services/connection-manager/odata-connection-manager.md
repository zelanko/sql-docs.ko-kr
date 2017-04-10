---
title: "OData 연결 관리자 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# OData 연결 관리자
  OData 연결 관리자를 사용하면 OData 원본에 연결할 수 있습니다. OData 원본 구성 요소는 OData 연결 관리자를 사용하여 OData 원본에 연결하고 서비스에서 데이터를 사용합니다. 자세한 내용은 [OData Source](../../integration-services/data-flow/odata-source.md)를 참조하십시오.  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>SSIS 패키지에 OData 연결 관리자 추가  
 세 가지 방법으로 새로운 OData 연결 관리자를 SSIS 패키지에 추가할 수 있습니다.  
  
-    **새로 만들기...**를 클릭합니다. 에서 **새로 만들기…**  
  
-   **솔루션 탐색기** 에서 **연결 관리자**폴더를 마우스 오른쪽 단추로 클릭하고 **새 연결 관리자**를 클릭합니다. **연결 관리자 유형** 에 대해 **ODATA**를 선택합니다.  
  
-   패키지 디자이너 아래쪽에서 **연결 관리자** 창을 마우스 오른쪽 단추로 클릭하고 **새 연결...**을 선택합니다. **연결 관리자 유형** 에 대해 **ODATA**를 선택합니다.  
  
## <a name="connection-manager-authentication"></a>연결 관리자 인증  
 OData 연결 관리자는 5가지 모드의 인증을 지원합니다.  
  
-   Windows 인증  
  
-   기본 인증(사용자 이름 및 암호 사용)  

-   Microsoft Dynamics AX Online(사용자 이름 및 암호 사용)
  
-   Microsoft Dynamics CRM Online(사용자 이름 및 암호 사용)
  
-   Microsoft Online Services(사용자 이름 및 암호 사용)  
  
 익명 액세스의 경우 Windows 인증 옵션을 선택합니다.  
  
### <a name="specifying-and-securing-credentials"></a>자격 증명 지정 및 보안  
 OData 서비스에 기본 인증이 필요한 경우 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)에서 사용자 이름과 암호를 지정할 수 있습니다. 편집기에 입력한 값은 패키지에서 유지됩니다. 암호 값은 패키지 보호 수준에 따라 암호화됩니다.  
  
 여러 가지 방법으로 사용자 이름 및 암호 값을 매개 변수화하거나 패키지 외부에 저장할 수 있습니다. 예를 들어 매개 변수를 사용하여 이 작업을 수행할 수도 있고, SQL Server Management Studio를 사용하여 패키지를 실행할 때는 연결 관리자 속성을 직접 설정할 수도 있습니다.  
  
## <a name="odata-connection-manager-properties"></a>OData 연결 관리자 속성  
 다음 목록에서는 OData 연결 관리자의 속성에 대해 설명합니다.  
  
|||  
|-|-|  
|속성|Description|  
|Url|서비스 문서에 대한 URL입니다.|  
|UserName|기본 인증에 사용할 사용자 이름입니다.|  
|암호|기본 인증에 사용할 암호입니다.|  
|ConnectionString|연결 관리자의 다른 속성을 반영합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [OData 연결 관리자 편집기](../../integration-services/connection-manager/odata-connection-manager-editor.md)  
  
  