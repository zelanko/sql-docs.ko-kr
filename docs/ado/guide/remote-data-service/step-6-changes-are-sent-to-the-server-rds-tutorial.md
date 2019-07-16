---
title: '6단계: 변경 내용 (RDS 자습서) 서버로 보내집니다. | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a48b9c54496100bfe502bd496b12f35ced9ea8ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922041"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>6단계: 서버에 변경 내용이 보내집니다(RDS 자습서).
경우는 **레코드 집합** 개체를 편집, 변경 (즉, 추가, 변경 또는 삭제 하는 행) 서버에 다시 보낼 수 있습니다.  
  
> [!NOTE]
>  ADO 개체 및 Microsoft OLE DB 원격 공급자를 사용 하 여 RDS의 기본 동작을 암시적으로 호출할 수 있습니다. 쿼리에서 반환할 수 있습니다 **Recordset**s, 편집 하 고 **레코드 집합**의데이터 소스를 업데이트할 수 있습니다. 이 자습서 ADO 개체를 사용 하 여 RDS를 호출 하지 않습니다 이지만 같습니다 경우:  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **Part A** 만 했던이 사례에 대 한 가정은 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 하 고는 **레코드 집합** 개체가 이제 연결 된 된 **rds. DataControl**합니다. [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 의 변경 내용으로 데이터 소스를 업데이트 하는 메서드는 **레코드 집합** 경우 개체를 [Server](../../../ado/reference/rds-api/server-property-rds.md) 및 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성 설정 계속 됩니다.  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
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
  
 **B 부분** 또는 사용 하 여 서버를 업데이트할 수 있습니다 합니다 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체에 대 한 연결 및 **레코드 집합** 개체입니다.  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **이 자습서의 끝입니다.**  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft OLE DB 원격 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
