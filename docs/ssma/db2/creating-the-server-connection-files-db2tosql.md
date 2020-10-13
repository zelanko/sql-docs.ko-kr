---
description: 서버 연결 파일 만들기 (DB2ToSQL)
title: 서버 연결 파일 만들기 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 754f9002dd5b9e8f9111dce59bc81417c704e40d
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91984919"
---
# <a name="creating-the-server-connection-files-db2tosql"></a>서버 연결 파일 만들기 (DB2ToSQL)

서버 정보는 스크립트 파일의 servers 섹션 또는 별도의 서버 연결 파일에서 지정할 수 있습니다. 서버 연결 파일에 대 한 명령줄 매개 변수는, `-c <serverconnectionfile>` 입니다. 스크립트 파일 및 서버 연결 파일에 동일한 서버 ID가 있는 경우 스크립트 파일의 서버 정의가 고려 됩니다.

**예: 1**

```xml
<!-- Sample of server connection file commands -->
<db2 name="<source-server-unique-name>">
  <standard-mode>

    <connection-provider value="OleDB Provider" />

    <!-- Defines server manager to connect.
         Available manager attribute values
           • zOs - DB2 for z/OS
           • LUW - DB2 for Linux, Unix and Windows
           • DBi - DB2 for i -->
    <database-manager value="$Db2Manager$" />

    <server-name value="$Db2HostName$" />

    <port value="$Db2Port$" />

    <initial-catalog value="$Db2Instance$" />

    <user-id value="$Db2UserName$" />

    <password value="$Db2Password$"/>

  </standard-mode>
</db2>
```

```xml
<sql-server name="<target-server-unique-name>">
  <sql-server-authentication>

    <server value="<server-name>" />

    <database value="<database-name>" />
  
    <user-id value="<user-name>"/>
  
    <password value="<password>"/>

  </sql-server-authentication>
</sql-server>
```

## <a name="next-step"></a>다음 단계

콘솔 운영의 다음 단계에서는 [SSMA 콘솔 &#40;DB2ToSQL를 실행 합니다&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)

## <a name="see-also"></a>참고 항목

- [SSMA 콘솔 실행](./executing-the-ssma-console-db2tosql.md)