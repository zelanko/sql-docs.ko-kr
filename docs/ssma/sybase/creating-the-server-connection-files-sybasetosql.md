---
title: "서버 연결 파일 (SybaseToSQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Creating Server Connection Files
- Sybase Console,Server Connection File Validation
ms.assetid: 35ef396f-9f98-429d-9fc5-4f413d08fb37
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f7cea05ac113d752a67202cebb6a072876666315
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="creating-the-server-connection-files-sybasetosql"></a>서버 연결 파일 (SybaseToSQL) 만들기
별도 서버 연결 파일 또는 스크립트 파일의 서버 섹션에 서버 정보를 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는 `-c <serverconnectionfile>`합니다. 동일한 서버 id가 스크립트 파일 및 서버 연결 파일에 있는 스크립트 파일의 서버 정의 간주 됩니다.  
  
**예:**  
  
```  
1.<!--Sample of server connection file commands -->  
  
<sybase name="<source-server-unique-name>">  
  
  <standard-mode>  
  
    <provider value="Ole DB Provider"/>  
  
    <server-name value="<server-name>"/>  
  
    <server-port value="<port>"/>  
  
    <user-id value="<password>"/>  
  
  </standard-mode>  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
```  
2.<!—Sample of server connection file commands-->  
<sybase name="<source-server-unique-name>">  
  
  <advanced-mode>  
  
    <connection-string value="User ID=<user-name>;Password=<password>;Provider=ASEOLEDB.1;Server=<server-name>;Port=<port>;OLE DB Services = -2;"/>  
  
  </advanced-mode >  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication >  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
## <a name="server-connection-file-validation"></a>서버 연결에 대 한 파일 유효성 검사  
사용자가 서버 연결 파일 스키마 정의 파일에 대해 유효성을 검사할 쉽게 수 **S2SSConsoleScriptServersSchema.xsd** '스키마' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에 다음 단계는 [SSMA 콘솔 &#40; 실행 SybaseToSQL &#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  

