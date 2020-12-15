---
description: 페이지 쓰기
title: 페이지 쓰기 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- pages
ms.assetid: 409c8753-03c4-436d-839c-6a5879971551
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3c9fc200c47ffdb82c15a86469244cd17bd75821
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97403389"
---
# <a name="writing-pages"></a>페이지 쓰기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스의 I/O에는 논리적 읽기 수 및 물리적 읽기 수가 포함되어 있습니다. 논리적 쓰기는 버퍼 캐시에 있는 페이지의 데이터가 수정될 때 발생합니다. 물리적 쓰기는 페이지를 [버퍼 캐시](../relational-databases/memory-management-architecture-guide.md) 에서 디스크로 쓸 때 발생합니다.

페이지가 버퍼 캐시에서 수정될 때 페이지는 디스크에 바로 다시 기록되지 않고 대신 더티로 표시됩니다. 즉, 페이지는 물리적으로 디스크에 기록되기 전에 두 개 이상의 논리적 쓰기를 수행할 수 있습니다. 각 논리적 쓰기의 경우 트랜잭션 로그 레코드는 수정 사항을 기록하는 로그 캐시에 삽입됩니다. 로그 레코드는 관련된 더티 페이지가 버퍼 캐시에서 디스크로 제거되기 전에 디스크에 기록되어야 합니다. SQL Server는 연결된 로그 레코드가 디스크에 작성되기 전에 더티 페이지 작성을 방지하는 미리 쓰기 로깅이라는 기술을 사용합니다. 이는 복구 관리자가 정확하게 작업하는 데 필수적입니다. 자세한 내용은 [미리 쓰기 트랜잭션 로그](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)를 참조하세요.

다음 그림에서는 수정한 데이터 페이지를 쓰는 프로세스를 보여 줍니다.

![Writing_Pages](../relational-databases/media/writing-pages.gif)

버퍼 관리자가 페이지를 쓸 때 단일 수집-쓰기 작업에 포함될 수 있는 인접한 더티 페이지를 검색합니다. 인접한 페이지는 연속되는 페이지 ID를 포함하며 같은 파일에서 가져온 것입니다. 이러한 페이지는 메모리에서 연속되지 않아도 됩니다. 다음 이벤트 중 하나가 발생할 때까지 앞뒤로 계속 검색합니다.

 * 커밋된 페이지를 찾았습니다.
 * 32개의 페이지를 찾았습니다.
 * LSN(로그 시퀀스 번호)이 로그에 아직 플러시되지 않은 커밋되지 않은 페이지를 찾았습니다.
 * 즉시 래치할 수 없는 페이지를 찾았습니다.

이렇게 단일 수집 쓰기 작업으로 전체 페이지 집합을 디스크에 쓸 수 있습니다. 

페이지를 쓰기 직전에 데이터베이스에 지정된 페이지 보호 형식이 페이지에 추가됩니다. 조각난 페이지 보호가 추가되면 페이지는 I/O에 대해 배타적으로 래치되어야 합니다. 이는 조각난 페이지 보호가 페이지를 수정하여 다른 스레드가 읽기에 적합하지 않은 페이지로 만들기 때문입니다. 체크섬 페이지 보호가 추가되거나 데이터베이스가 페이지 보호를 사용하지 않으면 페이지는 I/O에 대해 UP(업데이트) 래치됩니다. 이렇게 래치하면 쓰는 동안 다른 사람은 페이지를 수정할 수 없지만 읽는 사람은 페이지를 계속 사용할 수 있습니다. 디스크 I/O 페이지 보호 옵션에 대한 자세한 내용은 [버퍼 관리](../relational-databases/memory-management-architecture-guide.md)를 참조하세요.

커밋되지 않은 페이지가 다음 3가지 방법 중 하나로 디스크에 기록됩니다. 

* 지연 기록   
 지연 기록기는 버퍼 캐시에서 자주 사용하지 않는 페이지를 제거하여 사용 가능한 버퍼를 제공하는 시스템 프로세스입니다. 더티 페이지가 맨 처음으로 디스크에 기록됩니다. 

* 즉시 기록   
 즉시 기록 프로세스에서는 BULK INSERT 또는 SELECT INTO와 같은 최소로 기록된 작업과 관련된 더티 데이터 페이지를 기록합니다. 이 프로세스를 통해 병렬로 새 페이지를 만들고 기록할 수 있습니다. 즉, 디스크에 페이지를 기록하기 전에 전체 작업을 완료할 때까지 호출 작업이 대기할 필요가 없습니다.

* 검사점   
 검사점 프로세스는 주기적으로 버퍼 캐시에서 지정된 특정 데이터베이스의 페이지를 포함하는 버퍼를 검색한 다음 모든 더티 페이지를 디스크에 기록합니다. 검사점은 모든 더티 페이지가 디스크에 기록되었음을 확인하는 지점을 만들어 나중에 복구하는 동안 시간을 절약할 수 있습니다. 사용자가 CHECKPOINT 명령을 사용하여 검사점 작업을 요청하거나 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 마지막 검사점 이후 경과된 시간 및 사용된 로그 공간에 따라 자동 검사점을 생성할 수 있습니다. 또한 검사점은 데이터 또는 로그 파일이 데이터베이스에서 제거 또는 추가되는 경우나 SQL Server 인스턴스가 중지되는 경우 등의 특정 작업이 수행될 때 생성됩니다. 자세한 내용은 [검사점 및 로그의 활성 부분](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)을 참조하세요.

지연 기록, 즉시 기록 및 검사점 프로세스는 I/O 작업이 완료할 때까지 대기하지 않습니다. 이 프로세스는 항상 비동기 또는 겹친 I/O를 사용하고 기타 작업을 계속 진행하여 이후에 I/O 성공을 확인합니다. 이에 따라 SQL Server에서 해당하는 태스크에 대해 CPU 리소스와 I/O 리소스를 모두 최대화할 수 있습니다.

## <a name="see-also"></a>참고 항목
[페이지 및 익스텐트 아키텍처 가이드](../relational-databases/pages-and-extents-architecture-guide.md)   
 [페이지 읽기](../relational-databases/reading-pages.md)
