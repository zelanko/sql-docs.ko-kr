---
description: '2단계: 서버 프로그램 호출(RDS 자습서)'
title: '2 단계: 서버 프로그램 호출 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: rothja
ms.author: jroth
ms.openlocfilehash: 4771957c1895f6ac861d04f63a43e32a77e3d931
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977594"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>2단계: 서버 프로그램 호출(RDS 자습서)
클라이언트 *프록시에서*메서드를 호출 하면 서버의 실제 프로그램이 메서드를 실행 합니다. 이 단계에서는 서버에서 쿼리를 실행 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 **A 부** 이 자습서에서 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 를 사용 하지 않은 경우이 단계를 수행 하는 가장 편리한 방법은 RDS를 사용 하는 것입니다. [ DataControl](../../reference/rds-api/datacontrol-object-rds.md) 개체입니다. **RDS. DataControl** 은 프록시를 만드는 이전 단계를 결합 합니다 .이 단계에서는 쿼리를 실행 합니다.  
  
 RDS를 설정 **합니다. ** 서버 프로그램을 인스턴스화해야 하는 위치를 식별 하는 DataControl 개체 [서버](../../reference/rds-api/server-property-rds.md) 속성 연결 [속성을](../../reference/rds-api/connect-property-rds.md) 사용 하 여 데이터 원본에 액세스 하는 연결 문자열을 지정 합니다. 그리고 [SQL](../../reference/rds-api/sql-property.md) 속성을 통해 쿼리 명령 텍스트를 지정할 수 있습니다. 그런 다음 [Refresh](../../reference/rds-api/refresh-method-rds.md) 메서드를 실행 하 여 서버 프로그램이 데이터 원본에 연결 하 고, 쿼리에 지정 된 행을 검색 하 고, **레코드 집합** 개체를 클라이언트에 반환 하도록 합니다.  
  
 이 자습서에서는 RDS를 사용 하지 않습니다 **. 무엇 보다도이**방법이 무엇 인지 확인 하는 방법은 다음과 같습니다.  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 자습서에서 ADO 개체로 RDS를 호출 하는 것은 아니지만이 자습서에서 다음과 같은 작업을 수행 하는 방법을 보여 줍니다.  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 파트** 이 단계를 수행 하는 일반적인 방법은 **DataFactory** 개체 [쿼리](../../reference/rds-api/query-method-rds.md) 메서드를 호출 하는 것입니다. 이 메서드는 데이터 원본에 연결 하는 데 사용 되는 연결 문자열과 데이터 원본에서 반환 될 행을 지정 하는 데 사용 되는 명령 텍스트를 사용 합니다.  
  
 이 자습서에서는 **DataFactory** object **쿼리** 메서드를 사용 합니다.  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>참고 항목  
 [3 단계: 서버에서 레코드 집합 가져오기 (RDS 자습서)](./step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 자습서(VBScript)](./rds-tutorial-vbscript.md)