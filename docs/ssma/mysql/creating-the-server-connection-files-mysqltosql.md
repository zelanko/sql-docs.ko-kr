---
title: "서버 연결 파일 (MySQLToSQL) 만들기 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
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
- Server connection file validation
- Server connection files
ms.assetid: df0e970c-da0b-4118-b359-c9dcbbad16d6
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9aa45d743a62fb3c2a111b64e254c78db22a7e90
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="creating-the-server-connection-files-mysqltosql"></a>서버 연결 파일 (MySQLToSQL) 만들기
별도 서버 연결 파일 또는 스크립트 파일의 서버 섹션에 서버 정보를 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는 `-c <serverconnectionfile>`합니다. 동일한 서버 id가 스크립트 파일 및 서버 연결 파일에 있는 스크립트 파일의 서버 정의 간주 됩니다.  
  
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
  
## <a name="server-connection-file-validation"></a>서버 연결에 대 한 파일 유효성 검사  
사용자가 서버 연결 파일 스키마 정의 파일에 대해 유효성을 검사할 쉽게 수 **'M2SSConsoleScriptServersSchema.xsd'** '스키마' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에 다음 단계는 [SSMA 콘솔 &#40; 실행 MySQLToSQL &#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 (MySQL)를 실행합니다.](http://msdn.microsoft.com/en-us/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  

