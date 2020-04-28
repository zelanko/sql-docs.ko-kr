---
title: 명령 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f94cc014a04c3392fefb61f4fa291a8f5a44ad8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638450"
---
# <a name="executing-a-command"></a>명령 실행
  데이터 원본에 대한 연결이 설정된 후 소비자는 **IDBCreateSession::CreateSession** 메서드를 호출하여 세션을 만듭니다. 세션은 명령, 행 집합 또는 트랜잭션 팩토리로 작동합니다.  
  
 개별 테이블이나 인덱스를 직접 사용하기 위해 소비자는 `IOpenRowset` 인터페이스를 요청합니다. `IOpenRowset::OpenRowset` 메서드는 단일 기본 테이블이나 인덱스의 모든 행이 포함된 행 집합을 열고 반환합니다.  
  
 명령을 실행 하기 위해 (예: Authors \* 에서 선택) 소비자는 `IDBCreateCommand` 인터페이스를 요청 합니다. 소비자는 `IDBCreateCommand::CreateCommand` 메서드를 호출하여 명령 개체를 만들고 `ICommandText` 인터페이스를 요청할 수 있습니다. 실행할 명령을 지정하는 데는 `ICommandText::SetCommandText` 메서드를 사용합니다.  
  
 명령을 실행하는 데는 `Execute` 명령을 사용합니다. SQL 문이나 프로시저 이름은 모두 명령으로 사용할 수 있습니다. 결과 집합(행 집합) 개체를 생성하지 않는 명령도 있습니다. SELECT * FROM Authors와 같은 명령은 결과 집합을 생성합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client OLE DB 공급자 애플리케이션 만들기](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
