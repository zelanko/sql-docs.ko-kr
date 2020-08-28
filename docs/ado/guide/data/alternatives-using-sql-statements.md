---
description: '대안: SQL 문 사용'
title: '대안: SQL 문 사용 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: rothja
ms.author: jroth
ms.openlocfilehash: 423a0afa6bba082cbebc28bee07c5be3ba90c6f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991624"
---
# <a name="alternatives-using-sql-statements"></a>대안: SQL 문 사용
ADO를 사용 하면 데이터를 편집 하는 데 사용할 수 있는 기본 제공 속성 및 방법 대신 명령을 사용할 수도 있습니다. 공급자에 따라이 섹션에 설명 된 모든 작업은 데이터 원본에 명령을 전달 하 여 수행할 수도 있습니다. 예를 들어 SQL UPDATE 문을 사용 하 여 **필드**의 **Value** 속성을 사용 하지 않고 데이터를 수정할 수 있습니다. SQL INSERT 문을 사용 하 여 ADO 메서드 **AddNew**대신 데이터 원본에 새 레코드를 추가할 수 있습니다. 공급자의 SQL 또는 데이터 조작 언어에 대 한 자세한 내용은 데이터 원본 설명서를 참조 하십시오.  
  
 예를 들어 다음 코드와 같이 DELETE 문을 포함 하는 SQL 문자열을 데이터베이스에 전달할 수 있습니다.  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
