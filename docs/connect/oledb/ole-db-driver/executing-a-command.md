---
title: 명령 실행(OLE DB 드라이버) | Microsoft Docs
description: 명령 실행
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5077f621e8a3698e5aec09b79f28a2f5cf9257e7
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244854"
---
# <a name="executing-a-command"></a>명령 실행
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  데이터 원본에 대한 연결이 설정된 후 소비자는 **IDBCreateSession::CreateSession** 메서드를 호출하여 세션을 만듭니다. 세션은 명령, 행 집합 또는 트랜잭션 팩토리로 작동합니다.  
  
 개별 테이블이나 인덱스를 직접 사용하기 위해 소비자는 **IOpenRowset** 인터페이스를 요청합니다. **IOpenRowset::OpenRowset** 메서드는 단일 기본 테이블이나 인덱스의 모든 행이 포함된 행 집합을 열고 반환합니다.  
  
 SELECT \* FROM Authors와 같은 명령을 실행하기 위해 소비자는 **IDBCreateCommand** 인터페이스를 요청합니다. 소비자는 **IDBCreateCommand::CreateCommand** 메서드를 호출하여 명령 개체를 만들고 **ICommandText** 인터페이스를 요청할 수 있습니다. 실행할 명령을 지정하는 데는 **ICommandText::SetCommandText** 메서드를 사용합니다.  
  
 명령을 실행하는 데는 **Execute** 명령을 사용합니다. SQL 문이나 프로시저 이름은 모두 명령으로 사용할 수 있습니다. 결과 집합(행 집합) 개체를 생성하지 않는 명령도 있습니다. SELECT * FROM Authors와 같은 명령은 결과 집합을 생성합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 애플리케이션용 OLE DB 드라이버 만들기](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
