---
title: 서버 연결 파일 (AccessToSQL) 만들기 | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10cdd1a711d23d8934631c30a317aca4ca247a10
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="creating-the-server-connection-files-accesstosql"></a>서버 연결 파일 (AccessToSQL) 만들기
서버 정보 수 스크립트 파일의 서버 섹션에서 지정 합니다. 별도 서버 연결 파일에 서버 정보를 지정할 수도 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는 `-c <serverconnectionfile>`합니다. 동일한 서버 id가 스크립트와 서버 둘 다 연결 파일에 있는 스크립트 파일의 서버 정의 간주 됩니다.  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>서버 연결에 대 한 파일 유효성 검사  
사용자가 서버 연결 파일 스키마 정의 파일에 대해 유효성을 검사할 쉽게 수 **'A2SSConsoleScriptServersSchema.xsd'** '스키마' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에 다음 단계는 [SSMA 콘솔 실행 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 (Access)를 실행합니다.](http://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
