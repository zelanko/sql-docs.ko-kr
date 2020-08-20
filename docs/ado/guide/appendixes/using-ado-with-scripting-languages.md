---
description: 스크립트 언어로 ADO 사용
title: 스크립팅 언어와 함께 ADO 사용 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6decee7fddc4748a7d0931ab671f66b11161cc9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453995"
---
# <a name="using-ado-with-scripting-languages"></a>스크립트 언어로 ADO 사용
스크립팅 환경 내에서 ADO를 사용 하면 서버 쪽 스크립팅을 통해 데이터를 노출할 수 있습니다. 이 시나리오에서 사용 하는 기본 OLE DB 공급자와 지정 된 데이터 저장소를 참조 하는 데 필요한 다른 모든 구성 요소는 인터넷 정보 서비스 (IIS)를 실행 하는 서버에 설치 됩니다. ADO는 ASP (Active Server Pages)를 사용 하 여 HTML을 생성할 수 있는 스크립트에서 참조 되는 구성 요소입니다 (예:). 이 HTML 콘텐츠는 HTTP를 통해 클라이언트 웹 브라우저에 전달 될 수 있습니다. 스크립팅을 사용 하면 웹 페이지에서 서버 쪽 스크립트로 작업을 다시 보낼 수 있으므로 특정 데이터를 업데이트 하거나 트래버스 하거나 볼 수 있습니다.  
  
 웹 페이지에서 ActiveX 개체를 사용 하기 전에 개체가 스크립팅에 안전 하 게 보호 되는지 여부를 확인 하는 것이 중요 합니다. 개체가 스크립팅에 안전한 것으로 간주 되 면 컨트롤은 사용자의 컴퓨터에서 유해한 작업을 수행할 수 없으므로 사용자의 승인을 요청 하지 않고 실행할 수 있습니다. 다음 표에서는 ADO 개체를 나열 하 고 스크립트를 안전 하 게 사용할 수 있는지 여부를 나타냅니다.  
  
|Object|스크립팅에 안전 합니까?|  
|------------|-------------------------|  
|ADO 연결|예|  
|ADO 명령|예|  
|ADO 매개 변수|예|  
|ADO 레코드 집합|예|  
|ADO 레코드|예|  
|ADO 스트림|예|  
|ADO 오류|예|  
|ADOX 카탈로그|예|  
|ADOX 셀 집합|예|  
|RDS DataControl|예|  
|RDS 공간|예|  
|RDS DataFactory|예|  
  
 다음 표에서는 Windows DAC/MDAC에 포함 된 공급자를 나열 하 고 해당 공급자를 스크립팅에 안전 하 게 사용할 수 있는지 여부를 나타냅니다.  
  
|공급자|스크립팅에 안전 합니까?|  
|--------------|-------------------------|  
|도형|예|  
|Persist|예|  
|원격|예|  
|SQL Server에 대 한 OLE DB 공급자 (SQLOLEDB)|예|  
|ODBC 용 OLE DB 공급자 (MSDASQL)|예|  
  
## <a name="odbc-data-sources"></a>ODBC 데이터 원본  
 스크립팅 및 비 스크립팅 ADO 코드의 중요 한 차이점 중 하나는 ODBC 데이터 원본입니다 (사용 되는 경우). 비 스크립팅 응용 프로그램의 경우 ODBC 데이터 원본 관리자에서 사용자 DSN을 만들 수 있습니다. IIS에서 실행 되는 스크립트의 경우 시스템 DSN을 만들어야 합니다. 그렇지 않은 경우 스크립트는 사용자가 만든 데이터 원본을 인식 하지 못합니다. Microsoft IIS를 통해 Microsoft OLE DB Provider for ODBC를 사용 하는 모든 ADO 스크립팅 응용 프로그램에 적용 됩니다.  
  
## <a name="referencing-the-ado-library"></a>ADO 라이브러리 참조  
 스크립팅 언어에는 적용 되지 않습니다.  
  
## <a name="handling-events"></a>이벤트 처리  
 스크립팅 언어에는 적용 되지 않습니다.  
  
 다음 항목에는 스크립팅 언어와 함께 ADO를 사용 하는 방법에 대 한 자세한 내용이 포함 되어 있습니다.  
  
-   [VBScript ADO 프로그래밍](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript ADO 프로그래밍](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft ADO(ActiveX Data Objects) (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Microsoft Visual Basic에서 ADO 사용](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Microsoft Visual C++으로 ADO 사용](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
