---
title: 서버 연결 파일 만들기 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Server Connection Files
- Sybase Console,Server Connection File Validation
ms.assetid: 35ef396f-9f98-429d-9fc5-4f413d08fb37
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ece41e157ddad4f62a041d8e06dde073f681d274
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029363"
---
# <a name="creating-the-server-connection-files-sybasetosql"></a>서버 연결 파일 만들기(SybaseToSQL)
서버 정보는 스크립트 파일의 servers 섹션 또는 별도의 서버 연결 파일에서 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는, `-c <serverconnectionfile>`입니다. 스크립트 파일 및 서버 연결 파일에 동일한 서버 id가 있는 경우 스크립트 파일의 서버 정의가 고려 됩니다.  
  
**예제:**  
  
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
2.<!-Sample of server connection file commands-->  
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
  
## <a name="server-connection-file-validation"></a>서버 연결 파일 유효성 검사  
사용자는 ' 스키마 ' 폴더에서 사용할 수 있는 **S2SSConsoleScriptServersSchema** 스키마 정의 파일에 대해 서버 연결 파일의 유효성을 쉽게 검사할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
콘솔을 운영 하는 다음 단계에서는 [SSMA 콘솔 &#40;SybaseToSQL&#41;를 실행](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) 합니다.  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행](executing-the-ssma-console-sybasetosql.md)  
  
