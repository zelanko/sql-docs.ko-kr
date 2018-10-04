---
title: '2 단계: 서버 프로그램 (RDS 자습서)를 호출 합니다. | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a2e7b62276234dcf11067395ff2512a8e93af96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800511"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>2단계: 서버 프로그램 호출(RDS 자습서)
클라이언트에서 메서드를 호출 하는 경우 *프록시*를 서버의 실제 프로그램 메서드를 실행 합니다. 이 단계에서는 서버에서 쿼리를 실행 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 **Part A** 사용 하지 않는 경우 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 이 자습서에서는이 단계를 수행 하는 가장 편리한 방법은 사용할 것을 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다. **rds. DataControl** 쿼리 실행이 단계를 사용 하 여 프록시를 만드는 이전 단계를 결합 합니다.  
  
 설정 된 **rds. DataControl** 개체 [Server](../../../ado/reference/rds-api/server-property-rds.md) 여기서 서버 프로그램 인스턴스화해야; 식별 하는 속성을 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) ; 데이터 원본에 액세스 하는 연결 문자열을 지정 하는 속성 및 합니다 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성을 쿼리 명령 텍스트를 지정 합니다. 발급 합니다 [새로 고침](../../../ado/reference/rds-api/refresh-method-rds.md) 데이터 원본에 연결 하는 쿼리에 의해 지정 된 행을 검색 하 여 서버 프로그램을 반환 하는 메서드를 **레코드 집합** 클라이언트 개체입니다.  
  
 이 자습서를 사용 하지 않습니다는 **rds. DataControl**, 같습니다 경우 이지만:  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 나는 자습서 호출 RDS ADO 개체를 사용 하지만 같습니다 경우 이것이:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 부분** 이 단계를 수행 하는 일반 메서드 호출 하는 것은 **업데이트할** 개체 [쿼리](../../../ado/reference/rds-api/query-method-rds.md) 메서드. 해당 메서드는 데이터 원본에 연결에 사용 되는 연결 문자열 및 데이터 원본에서 반환 될 행을 지정 하는 데 사용 되는 명령 텍스트를 사용 합니다.  
  
 이 자습서에서는 합니다 **DataFactory** 개체 **쿼리** 메서드:  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>관련 항목  
 [3 단계: 서버가 가져옵니다 (RDS 자습서) 레코드 집합을](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
