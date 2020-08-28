---
description: 레코드 집합을 반환하는 JScript 코드 예제
title: 레코드 집합을 반환 하는 JScript 코드 예제 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- Recordset [ADO]
ms.assetid: 74aad8a6-06cc-4a2c-811a-d78f9b741d84
author: rothja
ms.author: jroth
ms.openlocfilehash: 32c9c97d8baaff41d209a939fdca5d3e5d7a5435
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980414"
---
# <a name="jscript-code-example-to-return-a-recordset"></a>레코드 집합을 반환하는 JScript 코드 예제
## <a name="jscript-code-rsjs"></a>JScript 코드 (rs.js)  
  
```  
main();  
  
function main()  
{  
  DP = "SQLOLEDB";  
  DS = "MySQLServer";  
  DB = "NORTHWIND";  
  
  adOpenForwardOnly = 0;  
  adLockReadOnly = 1;  
  adCmdText = 1;  
  try   
  {  
    var objRs = new ActiveXObject("ADODB.Recordset");  
  }  
  catch (e)  
  {  
    alert("ADODB namespace not found.");  
    exit(0);  
  }  
  
  strConn =  "Provider="         +DP+  
            ";Initial Catalog="  +DB+  
            ";Data Source="      +DS+  
            ";Integrated Security=SSPI;"  
  strComm = "SELECT ProductID,ProductName,UnitPrice "+  
            "FROM Products " +   
            "WHERE CategoryID = 7"  // select Produce  
  
  objRs.open(strComm,   
             strConn,   
             adOpenForwardOnly,  
             adLockReadOnly,  
             adCmdText);  
  
  objRs.MoveFirst();  
  while (objRs.EOF != true)   
  {  
    alert(objRs("ProductID")+"\t"  
         +objRs("ProductName")+"\t"  
         +objRs("UnitPrice"));  
    objRs.MoveNext();  
  }  
  
  objRs.Close  
  objRs = null;  
}  
  
function alert(str)  
{  
  WScript.Echo(str);  
}  
```  
  
#### <a name="try-it"></a>실습  
  
1.  위의 코드를 텍스트 파일에 저장 합니다. rs.js로 파일을 저장 합니다.  
  
2.  명령 프롬프트를 열고 JScript 파일 (rs.js)을 저장 한 디렉터리로 이동 합니다.  
  
3.  `CScript rs.js`명령 프롬프트에서을 입력 합니다.
