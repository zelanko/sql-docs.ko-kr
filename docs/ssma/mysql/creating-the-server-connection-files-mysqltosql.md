---
title: 서버 연결 파일 (MySQLToSQL) 만들기 | Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d827a48f76639b15cc63e295e7f40190b60a4694
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132278"
---
# <a name="creating-the-server-connection-files-mysqltosql"></a>서버 연결 파일 만들기(MySQLToSQL)
스크립트 파일의 서버 섹션에서 또는 별도 서버 연결 파일에 서버 정보를 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는 `-c <serverconnectionfile>`합니다. 동일한 서버 id가 스크립트 파일과 서버 연결 파일에 있는 스크립트 파일의 서버 정의 간주 됩니다.  
  
**예제:**  
  
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
사용자 스키마 정의 파일에 대해 자신의 서버 연결 파일을 쉽게 확인할 수 있습니다 **'M2SSConsoleScriptServersSchema.xsd'** 'Schemas' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에서 다음 단계 [SSMA 콘솔 실행 &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SSMA 콘솔 (MySQL)를 실행합니다.](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
