---
description: MSSQLSERVER_5242
title: MSSQLSERVER_5242 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5242 (Database Engine error)
ms.assetid: 712b1a10-2f87-41df-a111-1ed9f14102d4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 47e4d3ed7cac78764d8ff1069a0a38ca78603c22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470991"
---
# <a name="mssqlserver_5242"></a>MSSQLSERVER_5242
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|5242|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|데이터베이스 '%.*ls'(ID:%d)의 페이지 %S_PGID에서 내부 작업을 수행하는 중 불일치가 감지되었습니다. 기술 지원 서비스에 문의하십시오. 참조 번호는 %ld입니다.|  
  
## <a name="explanation"></a>설명  
오류 메시지에 언급된 데이터베이스 페이지에 구조적 불일치가 발생했습니다.  
  
## <a name="see-also"></a>참고 항목  
[DBCC CHECKDB&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[데이터베이스 파일 및 파일 그룹](~/relational-databases/databases/database-files-and-filegroups.md)  
  
