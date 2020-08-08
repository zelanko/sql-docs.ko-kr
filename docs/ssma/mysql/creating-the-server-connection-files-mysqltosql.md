---
title: 서버 연결 파일 만들기 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server connection file validation
- Server connection files
ms.assetid: df0e970c-da0b-4118-b359-c9dcbbad16d6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fa9505c0f5c40dcf2ff7cd84fc956240728385b3
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935732"
---
# <a name="creating-the-server-connection-files-mysqltosql"></a>서버 연결 파일 만들기(MySQLToSQL)
서버 정보는 스크립트 파일의 servers 섹션 또는 별도의 서버 연결 파일에서 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는, `-c <serverconnectionfile>` 입니다. 스크립트 파일 및 서버 연결 파일에 동일한 서버 id가 있는 경우 스크립트 파일의 서버 정의가 고려 됩니다.  
  
**예:**  
  
```xml  
<!--Sample of server connection file commands -->  
  
<mysql name ="<source-server-unique-name>">  
  
   <standard-mode>  
  
      <server value ="<server-name>"/>  
  
      <user-id value ="<user-name>"/>  
  
      <password value ="<password>"/>  
  
      <port value ="<port>"/>  
  
   </standard-mode>  
  
</mysql>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
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
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="<target-server-unique-name>">  
  
   <server value="<server-name>"/>  
  
   <database value="<database-name>"/>  
  
   <user-id value="<user-name>"/>  
  
   <password value="<password>"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>서버 연결 파일 유효성 검사  
사용자는 ' 스키마 ' 폴더에서 사용 가능한 스키마 정의 파일 ' **m 2ssconsolescriptserversschema '** 에 대해 서버 연결 파일의 유효성을 쉽게 검사할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
콘솔 운영의 다음 단계에서는 [SSMA 콘솔 &#40;MySQLToSQL&#41;실행](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) 합니다.  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행 (MySQL)](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
