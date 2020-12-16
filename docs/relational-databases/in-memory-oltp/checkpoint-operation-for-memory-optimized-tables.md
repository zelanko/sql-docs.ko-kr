---
title: 메모리 액세스에 최적화된 테이블에 대한 검사점 작업 | Microsoft 문서
description: SQL Server에서 메모리 최적화 테이블의 검사점에 대해 알아봅니다. 메모리 최적화 테이블 검사점 작업은 디스크 기반 테이블의 검사점 작업과는 다릅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ea64147c8a7bf9f6142b36cb048d7ad39f43b66
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465394"
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에 대한 검사점 작업
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  트랜잭션 로그의 활성 부분을 처리하기 위해서는 데이터 및 델타 파일에서 메모리 최적화 데이터에 대한 검사점이 정기적으로 설정되어야 합니다. 검사점을 사용하면 메모리 최적화 테이블이 마지막으로 성공한 검사점으로 복원되거나 복구될 수 있으며, 이때 메모리 최적화 테이블을 업데이트하여 복구를 완료하기 위해 트랜잭션 로그의 활성 부분이 적용됩니다. 디스크 기반 테이블의 검사점 작업과 메모리 최적화 테이블의 검사점 작업은 전혀 다른 작업입니다. 아래에서는 디스크 기반 테이블과 메모리 최적화 테이블의 서로 다른 시나리오 및 검사점 동작에 대해 설명합니다.  
  
## <a name="manual-checkpoint"></a>수동 검사점  
 수동 검사점을 실행하면 디스크 기반 테이블 및 메모리 최적화 테이블에 대한 검사점이 닫힙니다. 또한 부분적으로 채워졌을 수도 있는 활성 데이터 파일이 닫힙니다.  
  
## <a name="automatic-checkpoint"></a>자동 검사점  
 데이터가 지속되는 방식의 차이 때문에 자동 검사점은 디스크 기반 테이블과 메모리 최적화 테이블에 대해 다르게 구현됩니다.  
  
 디스크 기반 테이블의 경우 복구 간격 구성 옵션을 기반으로 자동 검사점이 확인됩니다(자세한 내용은 [데이터베이스의 대상 복구 시간 변경&#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md) 참조).  
  
 메모리 최적화 테이블의 경우 마지막 검사점 이후 트랜잭션 로그 파일이 1.5GB보다 커질 때 자동 검사점이 확인됩니다. 이 1.5GB 크기는 디스크 기반 테이블과 메모리 최적화 테이블에 대한 트랜잭션 로그 레코드를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 개체에 대한 스토리지 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
