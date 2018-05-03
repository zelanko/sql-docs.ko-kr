---
title: ADO를 사용 하 여 스크립트 언어 | Microsoft Docs
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
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90ecb29cd796cade5154bf293fd81c470d26b0b1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-ado-with-scripting-languages"></a>스크립트 언어와 함께 ADO 사용
스크립팅 환경 내에서 ADO를 사용 하면 서버 쪽 스크립트를 통해 데이터를 노출할 수 있습니다. 이 시나리오에서는 ADO, OLE DB 공급자를 사용 하 고 다른 모든 구성 요소는 지정 된 데이터 저장소를 참조 하는 데 필요한 인터넷 정보 서비스 (IIS)를 실행 하는 서버에 설치 되어 있는 원본으로 사용 합니다. ASP Active Server Pages ()를 사용 하 여 ADO는 예를 들어 HTML을 생성할 수 있는 스크립트에서 참조 하는 구성 요소입니다. 이 HTML 콘텐츠를 클라이언트 웹 브라우저에 HTTP를 통해 전달할 수 있습니다. 스크립트를 사용 하 여 웹 페이지 업데이트 트래버스하거나 특정 데이터를 볼 수 있도록 서버 쪽 스크립트에 다시 작업을 보낼 수 있습니다.  
  
 웹 페이지에는 ActiveX 개체를 사용 하기 전에는 개체가 스크립트에 대 한 안전 하 게 보호 되는지 확인 해야 합니다. 개체는 스크립팅에 안전한 것으로 간주 됩니다, 컨트롤 사용자의 컴퓨터에서 모든 유해한 작업을 수행할 수 없습니다 및 사용자의 승인 요청 하지 않고 실행할 수 있습니다 의미 합니다. 다음 표에서 ADO 개체를 나열 하 고 안전한 지 여부를 나타냅니다.  
  
|개체|스크립트 사용에 대 한 안전?|  
|------------|-------------------------|  
|ADO 연결|예|  
|ADO 명령|아니요|  
|ADO 매개 변수|아니요|  
|ADO 레코드 집합|예|  
|ADO 레코드|예|  
|ADO 스트림|예|  
|ADO 오류|아니요|  
|ADOX 카탈로그|아니요|  
|ADOX 셀 집합|아니요|  
|RDS DataControl|예|  
|RDS DataSpace|예|  
|RDS DataFactory|아니요|  
  
 다음 표에서 Windows DAC/MDAC와 포함 된 공급자를 나열 하 고 안전한 지 여부를 나타냅니다.  
  
|공급자|스크립트 사용에 대 한 안전?|  
|--------------|-------------------------|  
|셰이프|예|  
|유지|예|  
|원격|예|  
|OLE DB Provider for SQL Server (SQLOLEDB)|아니요|  
|OLE DB Provider for ODBC (MSDASQL)|아니요|  
  
## <a name="odbc-data-sources"></a>ODBC 데이터 원본  
 사용 하는 경우 중요 한 차이점 스크립팅 및 비 스크립팅 ADO 코드는 ODBC 데이터 원본으로 지정. 비 스크립팅 응용 프로그램에 대 한 사용자 DSN이 ODBC 데이터 원본 관리자를 만들 수 있습니다. IIS에서 실행 되는 스크립트에 대 한 시스템 DSN; 만들어야 합니다. 그렇지 않은 경우 스크립트에서 만든 데이터 원본을 인식 되지 않습니다. 이 Microsoft OLE DB Provider를 사용 하 여 Microsoft IIS를 통해 ODBC에 대 한 모든 ADO 스크립팅 응용 프로그램에 적용 됩니다.  
  
## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조  
 스크립트 언어는 적용 되지 않습니다.  
  
## <a name="handling-events"></a>이벤트 처리  
 스크립트 언어는 적용 되지 않습니다.  
  
 스크립트 언어와 함께 ADO 사용에 대 한 보다 구체적인 정보를 포함 하는 다음 항목:  
  
-   [VBScript ADO 프로그래밍](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 프로그래밍](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Microsoft Visual Basic ADO를 사용 하 여](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Microsoft Visual C++으로 ADO 사용](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
