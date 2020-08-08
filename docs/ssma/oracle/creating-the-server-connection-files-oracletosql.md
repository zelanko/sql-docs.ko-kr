---
title: 서버 연결 파일 만들기 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server Connection File Creation
- Server Connection File, Server Connection File Validation
ms.assetid: 002f129e-0868-48ad-a4b4-c68b5007e12e
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 499543ea1790e5f9c1f1e1f2ddf6111e9d846dc9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934941"
---
# <a name="creating-the-server-connection-files-oracletosql"></a>서버 연결 파일 만들기(OracleToSQL)
서버 정보는 스크립트 파일의 servers 섹션 또는 별도의 서버 연결 파일에서 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는, `-c <serverconnectionfile>` 입니다. 스크립트 파일 및 서버 연결 파일에 동일한 서버 id가 있는 경우 스크립트 파일의 서버 정의가 고려 됩니다.  
  
**예: 1**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <tns-name-mode>  
  
    <connection-provider value="OracleClient"/>  
  
    <service-name value="(DESCRIPTION =(ADDRESS_LIST =(ADDRESS = (PROTOCOL = TCP)(HOST = <host-name>)(PORT = 1521)))(CONNECT_DATA =(SERVICE_NAME = <service-name>)))"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </tns-name-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
**예: 2**  
  
```  
<!--Sample of server connection file commands -->  
  
<oracle name="<source-server-unique-name>">  
  
  <connection-string-mode>  
  
    <connection-provider value="OleDB Provider"/>  
  
    <custom-connection-string value="Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<host-name>)(PORT=1521))(CONNECT_DATA=(SID=<instance-name>)));User ID=<user-name>;Password=<password>"/>  
  
  </connection-string-mode>  
  
</oracle>  
```  
  
```  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <server value="<server-name>"/>  
  
    <database value="<database-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
## <a name="next-step"></a>다음 단계  
콘솔 운영의 다음 단계에서는 [SSMA 콘솔 &#40;OracleToSQL를 실행 합니다&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행](executing-the-ssma-console-oracletosql.md)  
  
