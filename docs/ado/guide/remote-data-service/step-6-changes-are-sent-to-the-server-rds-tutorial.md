---
title: '6 단계: (RDS 자습서) 서버에 변경 내용이 보내집니다 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd14dcfa918afc5bc252822ceacccfe10ddd7302
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274732"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>(RDS 자습서) 서버에 변경 내용이 보내집니다 6 단계:
경우는 **레코드 집합** 개체를 편집, 변경 (즉, 추가, 변경 또는 삭제 하는 행) 서버에 다시 보낼 수 있습니다.  
  
> [!NOTE]
>  ADO 개체 및 Microsoft OLE DB 원격 서비스 공급자와 함께 RDS의 기본 동작을 암시적으로 호출할 수 있습니다. 쿼리에서 반환할 수 있습니다 **레코드 집합**s, 편집 및 **레코드 집합**의데이터 소스를 업데이트할 수 있습니다. 이 자습서는 ADO 개체와 RDS를 호출 하지 않습니다 하지만 어떻게 했던 유사할 것입니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=http://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **A 파트** 이 대/이 소문자만 사용에 대 한 가정 된 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 하 고는 **레코드 집합** 개체가 연결 된 이제는 **.rds입니다 DataControl**합니다. [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 메서드 변경 내용을 데이터 소스 업데이트의 **레코드 집합** 경우 개체는 [서버](../../../ado/reference/rds-api/server-property-rds.md) 및 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성 설정 계속 됩니다.  
  
```  
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "http://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **B 파트** 또는 사용 하 여 서버를 업데이트할 수 있습니다는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체, 한 연결 지정 하 고 **레코드 집합** 개체입니다.  
  
```  
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **이 자습서의 끝입니다.**  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft OLE DB Remoting Provider (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
