---
title: "2 단계: 서버 프로그램 (RDS 자습서) 호출 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b660e20a92bdebe80def1d487cfa47b8c79109a9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>2 단계: 서버 프로그램 (RDS 자습서) 호출
클라이언트에 대 한 메서드를 호출 하는 경우 *프록시*, 서버에서 실제 프로그램 메서드를 실행 합니다. 이 단계에서는 서버에서 쿼리를 실행 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 **A 파트** 사용 하지 않는 경우 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 이 자습서의이 단계를 수행 하는 가장 편리한 방법은 사용 하려는 것은 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다. **.rds입니다 DataControl** 쿼리 실행이 단계를 사용 하 여 프록시를 만드는 이전 단계를 결합 합니다.  
  
 설정의 **.rds입니다 DataControl** 개체 [서버](../../../ado/reference/rds-api/server-property-rds.md) 여기서 서버 프로그램은 인스턴스화할 수; 식별 하기 위해 속성은 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성은 데이터 소스에 액세스 하는 연결 문자열을 지정 하 고 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성을 통해 쿼리 명령 텍스트를 지정 합니다. 그런 후 실행 하는 [새로 고침](../../../ado/reference/rds-api/refresh-method-rds.md) 를 데이터 원본에 연결 하는 쿼리로 지정 된 행을 검색 하 여 서버 프로그램는 **레코드 집합** 클라이언트에는 개체입니다.  
  
 이 자습서를 사용 하지 않는 **.rds입니다 DataControl**, 있지만이 같습니다 가입 하지 않은 경우:  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 또는 않습니다 자습서 호출 RDS ADO 개체와 사용 하지만 같습니다 경우 이것이:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 파트** 호출 하는 것이 단계를 수행 하는 일반적인 방법은 **업데이트할** 개체 [쿼리](../../../ado/reference/rds-api/query-method-rds.md) 메서드. 해당 메서드를 사용 되는 데이터 원본에 연결 하는 연결 문자열 및 데이터 원본에서 반환 될 행을 지정 하는 데 사용 되는 명령 텍스트를 사용 합니다.  
  
 이 자습서에서는 **DataFactory** 개체 **쿼리** 메서드:  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>관련 항목:  
 [3 단계: 서버가 가져옵니다 (RDS 자습서) 레코드 집합을](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
