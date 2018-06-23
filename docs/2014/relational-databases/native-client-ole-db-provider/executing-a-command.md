---
title: 명령 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d9c0f935bf4d3cd903346281080a8b08384c1e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172868"
---
# <a name="executing-a-command"></a>명령 실행
  소비자를 호출 하는 데이터 원본에 대 한 연결 설정 되 면는 **idbcreatesession:: Createsession** 메서드 세션을 만들 수 있습니다. 세션은 명령, 행 집합 또는 트랜잭션 팩토리로 작동합니다.  
  
 개별 테이블이나 인덱스를 직접 사용하기 위해 소비자는 `IOpenRowset` 인터페이스를 요청합니다. `IOpenRowset::OpenRowset` 메서드는 단일 기본 테이블이나 인덱스의 모든 행이 포함된 행 집합을 열고 반환합니다.  
  
 명령을 실행 하려면 (예: SELECT \* FROM Authors), 소비자의 요청은 `IDBCreateCommand` 인터페이스입니다. 소비자는 `IDBCreateCommand::CreateCommand` 메서드를 호출하여 명령 개체를 만들고 `ICommandText` 인터페이스를 요청할 수 있습니다. 실행할 명령을 지정하는 데는 `ICommandText::SetCommandText` 메서드를 사용합니다.  
  
 명령을 실행하는 데는 `Execute` 명령을 사용합니다. SQL 문이나 프로시저 이름은 모두 명령으로 사용할 수 있습니다. 결과 집합(행 집합) 개체를 생성하지 않는 명령도 있습니다. SELECT * FROM Authors와 같은 명령은 결과 집합을 생성합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client OLE DB 공급자 응용 프로그램 만들기](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  