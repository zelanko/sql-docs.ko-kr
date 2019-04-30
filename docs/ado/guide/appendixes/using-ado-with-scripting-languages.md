---
title: ADO를 사용 하 여 스크립트 언어를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fda0fb6446609a04178b533173a82bacc34c8cb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217751"
---
# <a name="using-ado-with-scripting-languages"></a>스크립트 언어로 ADO 사용
스크립팅 환경 내에서 ADO를 사용 하면 서버 쪽 스크립트를 통해 데이터를 노출할 수 있습니다. 이 시나리오, ADO, OLE DB 공급자를 사용 하는 기본 및 지정 된 데이터를 참조 하는 데 필요한 기타 구성 요소 저장소는 인터넷 정보 서비스 (IIS)를 실행 하는 서버에 설치 됩니다. ASP Active Server Pages ()를 사용 하 여 ADO는 예를 들어 HTML을 생성할 수 있는 스크립트에서 참조 구성 요소입니다. 이 HTML 콘텐츠를 클라이언트 웹 브라우저에 HTTP를 통해 전달할 수 있습니다. 스크립트를 사용 하 여 웹 페이지를 업데이트, 트래버스 또는 특정 데이터를 볼 수 있도록 서버 쪽 스크립트를 다시 작업을 보낼 수 있습니다.  
  
 웹 페이지에서 ActiveX 개체를 사용 하기 전에 것이 중요 스크립트 인지 여부를 알아야 합니다. 개체는 스크립팅에 안전한 것으로 간주 됩니다, 컨트롤 사용자의 컴퓨터에서 위험한 조치를 취할 수 없습니다 하 고 사용자의 승인을 요청 하지 않고 실행할 수 있습니다 의미 합니다. 다음 표에서 ADO 개체를 나열 하 고 안전한 지 여부를 나타냅니다.  
  
|Object|스크립팅에 안전한?|  
|------------|-------------------------|  
|ADO 연결|사용자 계정 컨트롤|  
|ADO 명령|아니요|  
|ADO 매개 변수|아니요|  
|ADO 레코드 집합|사용자 계정 컨트롤|  
|ADO 레코드|사용자 계정 컨트롤|  
|ADO Stream|사용자 계정 컨트롤|  
|ADO 오류|아니요|  
|ADOX 카탈로그|아니요|  
|ADOX 셀 집합|아니요|  
|RDS DataControl|사용자 계정 컨트롤|  
|RDS DataSpace|사용자 계정 컨트롤|  
|RDS DataFactory|아니요|  
  
 다음 표에서 MDAC/Windows DAC를 사용 하 여 포함 된 공급자를 나열 하 고 안전한 지 여부를 나타냅니다.  
  
|공급자|스크립팅에 안전한?|  
|--------------|-------------------------|  
|셰이프|사용자 계정 컨트롤|  
|유지|사용자 계정 컨트롤|  
|원격|사용자 계정 컨트롤|  
|OLE DB Provider for SQL Server (SQLOLEDB)|아니요|  
|OLE DB Provider for ODBC (MSDASQL)|아니요|  
  
## <a name="odbc-data-sources"></a>ODBC 데이터 원본  
 스크립팅 및 비-스크립팅 ADO 코드 간의 주요 차이점 중 하나는 ODBC 데이터 원본을 경우 사용 합니다. 비 스크립팅 응용 프로그램에 대 한 ODBC 데이터 원본 관리자에서 사용자 DSN을 만들 수 있습니다. IIS에서 실행 되는 스크립트를 만들어야 합니다 시스템 DSN입니다. 그렇지 않은 경우 스크립트는 만든 데이터 소스를 인식 하지 못합니다. Microsoft OLE DB Provider를 사용 하 여 Microsoft IIS를 통해 ODBC에 대 한 ADO 스크립팅 응용 프로그램에 적용 됩니다.  
  
## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조하기  
 스크립팅 언어를 사용 하 여 적용 되지 않습니다.  
  
## <a name="handling-events"></a>이벤트 처리  
 스크립팅 언어를 사용 하 여 적용 되지 않습니다.  
  
 스크립팅 언어를 사용 하 여 ADO를 사용 하는 방법에 대 한 보다 구체적인 정보를 포함 하는 다음 항목:  
  
-   [VBScript ADO 프로그래밍](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 프로그래밍](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Microsoft Visual Basic로 ADO 사용](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Microsoft Visual C++으로 ADO 사용](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
