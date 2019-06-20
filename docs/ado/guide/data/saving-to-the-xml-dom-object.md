---
title: XML DOM 개체 저장 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML DOM object [ADO], saving to
ms.assetid: 4d20fd28-aaf8-4232-83ce-f9d1e5f93dae
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 47462e323e77e23b70a85321764413c40494f3f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701609"
---
# <a name="saving-to-the-xml-dom-object"></a>XML DOM 개체에 저장
다음 Visual Basic 코드에 나와 있는 것 처럼 MSXML DOM 개체의 인스턴스를 XML 형식의 레코드 집합을 저장할 수 있습니다.  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\Program Files" & _  
        "\Common Files\System\msadc\samples\NWind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistADO   'Save Recordset directly into a DOM tree.  
...  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
