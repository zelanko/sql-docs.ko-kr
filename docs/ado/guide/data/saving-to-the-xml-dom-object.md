---
title: "XML DOM 개체에 저장 | Microsoft Docs"
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
helpviewer_keywords: XML DOM object [ADO], saving to
ms.assetid: 4d20fd28-aaf8-4232-83ce-f9d1e5f93dae
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c16e724cd4a6e66d377da20a1b5b575941235b66
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="saving-to-the-xml-dom-object"></a>XML DOM 개체에 저장
다음 Visual Basic 코드에서와 같이 MSXML DOM 개체의 인스턴스를 XML 형식의 레코드 집합을 저장할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
