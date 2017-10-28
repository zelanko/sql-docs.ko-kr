---
title: "서버 연결 파일 (DB2ToSQL) 만들기 | Microsoft Docs"
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
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c49bcf7ccc71e5e2b441ec4e9bfcdbbdc2dd62e6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="creating-the-server-connection-files-db2tosql"></a>서버 연결 파일 (DB2ToSQL) 만들기
별도 서버 연결 파일 또는 스크립트 파일의 서버 섹션에 서버 정보를 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는 `-c <serverconnectionfile>`합니다. 동일한 서버 id가 스크립트 파일 및 서버 연결 파일에 있는 스크립트 파일의 서버 정의 간주 됩니다.  
  
**예: 1**  
  
```  
<!--Sample of server connection file commands -->  
  
<db2 name="<source-server-unique-name>">  
  
    <standard-mode>  
  
      <connection-provider value ="OleDB Provider"/>  
  
      <!-- Defines server manager to connect.  
  
              Available manager attribute values  
  
              • zOs      - upgrades the project (default)  
  
              • LUW       - displays an error and halts the execution-->  
  
      <database-manager value="$Db2Manager$"/>  
  
      <server-name value="$Db2HostName$" />  
  
      <port value="$Db2Port$" />  
  
      <initial-catalog value="$Db2Instance$" />  
  
      <user-id value="$Db2UserName$" />  
  
      <password value="$Db2Password$"/>  
  
    </standard-mode>  
  
</db2>  
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
운영 콘솔에 다음 단계는 [실행 SSMA 콘솔 &#40; DB2ToSQL &#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  

