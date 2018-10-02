---
title: 대량 데이터 가져오기 준비(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e3196670f21070297b27046ca70878fb94c39d12
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622551"
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>대량 데이터 가져오기 준비(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **bcp** 명령, BULK INSERT 문 또는 OPENROWSET(BULK) 함수를 사용하여 데이터 파일의 데이터만 대량으로 가져올 수 있습니다.  
  
> [!NOTE]  
>  텍스트 파일이 아닌 개체의 데이터를 대량으로 가져오는 사용자 지정 응용 프로그램을 작성할 수 있습니다. 메모리 버퍼에서 데이터를 대량으로 가져오려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client(ODBC) API(응용 프로그래밍 인터페이스) 또는 OLE DB **IRowsetFastLoad** 인터페이스에 bcp 확장을 사용합니다.  C# 데이터 테이블에서 데이터를 대량으로 가져오려면 ADO.NET 대량 복사 API인 **SqlBulkCopy**를 사용합니다.  
  
> [!NOTE]  
>  원격 테이블로 데이터를 대량으로 가져올 수 없습니다.  
  
 데이터 파일에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 데이터를 대량으로 가져올 경우 다음 지침을 따르십시오.  
  
-   사용자 계정에 대해 필요한 권한 가져오기  
  
     **bcp** 유틸리티, BULK INSERT 문 또는 INSERT ... SELECT * FROM OPENROWSET(BULK...) 문을 사용하는 사용자 계정에는 테이블에 대해 필요한 권한(테이블 소유자가 할당)이 있어야 합니다. 각 방법에 필요한 사용 권한에 대한 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) 및 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
-   대량 로그 복구 모델 사용  
  
     이 지침은 전체 복구 모델을 사용하는 데이터베이스에 대한 내용입니다. 대량 로그된 복구 모델은 인덱싱되지 않은 테이블( *힙*)로 대량 작업을 수행할 때 유용합니다. 대량 로그 복구는 로그 행 삽입을 수행하지 않으므로 대량 로그 복구를 사용하면 트랜잭션 로그의 공간 부족 문제를 방지할 수 있습니다. 대량 로그된 복구 모델에 대한 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
     대량 가져오기 작업을 수행하기 바로 전에 대량 로그 복구 모델을 사용하여 데이터베이스를 변경하는 것이 좋습니다. 변경한 직후에는 데이터베이스를 전체 복구 모델로 다시 설정해야 합니다. 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
    > [!NOTE]  
    >  대량 가져오기 작업 동안의 로깅을 최소화하는 방법은 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
-   데이터를 대량으로 가져온 후 백업  
  
     단순 복구 모델을 사용하는 데이터베이스의 경우 대량 가져오기 작업이 완료된 후 전체 또는 차등 백업을 수행하는 것이 좋습니다. 자세한 내용은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) 또는 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)를 참조하세요.  
  
     대량 로그 복구 모델 또는 전체 복구 모델의 경우에는 로그 백업으로 충분합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)을 참조하세요.  
  
-   대규모 대량 가져오기의 성능 향상을 위해 테이블 인덱스 삭제  
  
     이 지침은 이미 테이블에 있는 데이터에 비해 많은 양의 데이터를 가져오는 경우에 대한 내용입니다. 이 경우 대량 가져오기 작업을 수행하기 전에 테이블의 인덱스를 삭제하면 성능이 매우 향상됩니다.  
  
    > [!NOTE]  
    >  이미 테이블에 있는 데이터에 비해 적은 양의 데이터를 로드하는 경우에는 인덱스를 삭제하면 성능이 저하됩니다. 인덱스를 다시 작성하는 데 필요한 시간이 대량 가져오기 작업 동안 절약된 시간보다 길 수도 있습니다.  
  
-   데이터 파일의 숨겨진 문자 찾기 및 제거  
  
     주로 데이터 파일의 끝 부분에 있는 숨겨진 문자는 다양한 유틸리티와 텍스트 편집기를 사용하여 표시할 수 있습니다. 대량 가져오기 작업 동안 ASCII 데이터 파일에 있는 숨겨진 문자가 문제를 일으켜 "예기치 않은 Null 발견" 오류가 발생할 수 있습니다. 이 경우 숨겨진 문자를 모두 찾아서 제거하면 이 문제가 해결됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [BULK INSERT 또는 OPENROWSET&#40;BULK...&#41;를 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  
