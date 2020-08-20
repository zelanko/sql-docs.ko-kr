---
description: 서버 연결 파일 만들기 (AccessToSQL)
title: 서버 연결 파일 만들기 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 207aa406df3f426658afa569d434ea71db5eba1e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480509"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>서버 연결 파일 만들기 (AccessToSQL)
서버 정보는 스크립트 파일의 서버 섹션에서 지정할 수 있습니다. 서버 정보는 별도의 서버 연결 파일에도 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는 `-c <serverconnectionfile>` 입니다. 스크립트 및 서버 연결 파일에 동일한 서버 id가 있는 경우 스크립트 파일의 서버 정의가 고려 됩니다.  
  
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
  
## <a name="server-connection-file-validation"></a>서버 연결 파일 유효성 검사  
사용자는 ' 스키마 ' 폴더에서 사용할 수 있는 **' A2SSConsoleScriptServersSchema '** 스키마 정의 파일에 대해 서버 연결 파일의 유효성을 쉽게 검사할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
콘솔 운영의 다음 단계에서는 [SSMA 콘솔 &#40;AccessToSQL를 실행 합니다&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행 (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
