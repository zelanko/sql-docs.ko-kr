---
title: 명령 실행 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 876ce5b140ab590fd1a599f9a05391a236021f68
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796009"
---
# <a name="executing-a-command"></a>명령 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  소비자를 호출 하는 데이터 원본에 대 한 연결 설정 되 면 합니다 **idbcreatesession:: Createsession** 메서드 세션을 만듭니다. 세션은 명령, 행 집합 또는 트랜잭션 팩토리로 작동합니다.  
  
 개별 테이블이나 인덱스를 직접 사용하기 위해 소비자는 **IOpenRowset** 인터페이스를 요청합니다. **IOpenRowset::OpenRowset** 메서드는 단일 기본 테이블이나 인덱스의 모든 행이 포함된 행 집합을 열고 반환합니다.  
  
 SELECT \* FROM Authors와 같은 명령을 실행하기 위해 소비자는 **IDBCreateCommand** 인터페이스를 요청합니다. 소비자가 실행할 수 있습니다는 **idbcreatecommand:: Createcommand** 명령 개체를 만들고 요청 하는 메서드는 **ICommandText** 인터페이스입니다. 합니다 **icommandtext:: Setcommandtext** 메서드를 실행 해야 하는 명령을 지정를 사용 합니다.  
  
 명령을 실행하는 데는 **Execute** 명령을 사용합니다. SQL 문이나 프로시저 이름은 모두 명령으로 사용할 수 있습니다. 결과 집합(행 집합) 개체를 생성하지 않는 명령도 있습니다. SELECT * FROM Authors와 같은 명령은 결과 집합을 생성합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 애플리케이션용 OLE DB 드라이버 만들기](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
