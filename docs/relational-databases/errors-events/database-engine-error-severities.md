---
title: 데이터베이스 엔진 오류 심각도 | Microsoft 문서
description: 이 심각도 수준 목록을 사용하여 SQL Server 데이터베이스 엔진이 오류를 생성할 때 SQL Server에 발생한 문제의 유형을 이해할 수 있습니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16bf5154c5ab08b790739e287ccb2934b942e591
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727522"
---
# <a name="database-engine-error-severities"></a>데이터베이스 엔진 오류 심각도
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 오류가 발생한 경우 오류 심각도는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발견된 문제의 유형을 나타냅니다.  
  
## <a name="levels-of-severity"></a>심각도  
 다음 표에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 발생하는 오류의 심각도를 나열하고 그 내용을 설명합니다.  
  
|심각도 수준|Description|  
|--------------------|-----------------|  
|0-9|상태 정보를 반환하거나 심각하지 않은 오류를 보고하는 정보 메시지입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 심각도가 0 ~ 9인 경우 시스템 오류를 발생시키지 않습니다.|  
|10|상태 정보를 반환하거나 심각하지 않은 오류를 보고하는 정보 메시지입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 호환성을 위해 오류 정보를 호출 애플리케이션으로 반환하기 전에 심각도 10을 심각도 0으로 변환합니다.|  
|11-16|사용자가 해결할 수 있는 오류를 나타냅니다.|  
|11|지정한 개체 또는 엔터티가 없음을 나타냅니다.|  
|12|특수한 쿼리 힌트로 인해 잠금을 사용하지 않는 쿼리에 대한 특수 심각도입니다. 일관성을 유지하는 기능인 잠금을 사용하지 않는 이러한 문으로 읽기 작업을 수행하면 데이터 일관성이 손상될 수 있습니다.|  
|13|트랜잭션 교착 상태 오류를 나타냅니다.|  
|14|거부된 권한 등의 보안 관련 오류를 나타냅니다.|  
|15|[!INCLUDE[tsql](../../includes/tsql-md.md)] 명령의 구문 오류를 나타냅니다.|  
|16|사용자가 해결할 수 있는 일반 오류를 나타냅니다.|  
|17-19|사용자가 해결할 수 없는 소프트웨어 오류를 나타냅니다. 문제를 시스템 관리자에게 알립니다.|  
|17|문이 실행되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스에 사용되는 디스크 공간, 메모리 또는 잠금 등의 리소스가 부족하게 되거나 시스템 관리자가 설정한 일정한 한계를 초과했음을 나타냅니다.|  
|18|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 소프트웨어에 문제가 있지만 문이 완료되고 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 대한 연결이 유지됨을 나타냅니다. 심각도가 18인 메시지가 발생하면 시스템 관리자에게 알려야 합니다.|  
|19|구성할 수 없는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 한계를 초과하여 현재 일괄 처리가 종료되었음을 나타냅니다. 심각도가 19 이상인 오류 메시지는 현재 일괄 처리의 실행을 중지합니다. 심각도가 19인 오류는 거의 발생하지 않습니다. 그러나 이 오류가 발생하면 시스템 관리자 또는 주 지원 공급자를 통해 해결해야 합니다. 심각도가 19인 메시지가 발생하면 시스템 관리자에게 문의합니다. 심각도가 19부터 25인 오류 메시지는 오류 로그에 기록됩니다.|  
|20-24|시스템 문제 및 심각한 오류를 나타냅니다. 즉 문 또는 일괄 처리를 실행하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 태스크가 더 이상 수행되지 않습니다. 태스크는 발생한 문제에 대한 정보를 기록한 다음 종료됩니다. 대부분의 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 애플리케이션과의 연결도 끊어집니다. 이 경우 문제에 따라 다를 수 있지만 애플리케이션에서 다시 연결하지 못합니다.<br /><br /> 이 범위의 오류 메시지는 동일한 데이터베이스의 데이터에 액세스하는 모든 프로세스에 영향을 미칠 수 있고 데이터베이스 또는 개체가 손상되었음을 나타내기도 합니다. 심각도가 19부터 25인 오류 메시지는 오류 로그에 기록됩니다.|  
|20|문에 문제가 발생했음을 나타냅니다. 발생한 문제는 현재 태스크에만 영향을 주므로 데이터베이스 자체는 손상되지 않습니다.|  
|21|현재 데이터베이스의 모든 태스크에 영향을 미치는 문제가 발생했음을 나타냅니다. 그러나 데이터베이스 자체는 손상되지 않습니다.|  
|22|메시지에서 지정된 테이블 또는 인덱스가 소프트웨어 또는 하드웨어 문제로 인해 손상되었음을 나타냅니다.<br /><br /> 심각도가 22인 오류는 거의 발생하지 않습니다. 그러나 이 오류가 발생한 경우 DBCC CHECKDB를 실행하여 데이터베이스 내의 다른 개체도 손상되었는지 확인해야 합니다. 문제가 버퍼 캐시에 한정되고 디스크 자체에는 아무 이상이 없을 수도 있습니다. 그럴 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 다시 시작하면 문제가 해결됩니다. 작업을 계속하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 다시 연결해야 합니다. 그렇지 않으면 DBCC를 사용하여 문제를 해결할 수 있습니다. 경우에 따라 데이터베이스를 복원해야 할 수도 있습니다.<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 다시 시작해도 문제가 해결되지 않는다면 디스크의 문제입니다. 가끔 오류 메시지에 지정된 개체를 제거하여 문제를 해결할 수도 있습니다. 예를 들어 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 비클러스터형 인덱스에서 길이가 0인 행을 발견했다는 메시지가 표시되면 해당 인덱스를 삭제하고 다시 작성합니다.|  
|23|하드웨어 또는 소프트웨어 문제로 인해 전체 데이터베이스의 무결성이 의심된다는 것을 나타냅니다.<br /><br /> 심각도가 23인 오류는 거의 발생하지 않습니다. 그러나 이 오류가 발생한 경우 DBCC CHECKDB를 실행하여 손상된 범위를 확인해야 합니다. 문제가 캐시에 한정되고 디스크 자체에는 아무 이상이 없을 수도 있습니다. 그럴 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 다시 시작하면 문제가 해결됩니다. 작업을 계속하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 다시 연결해야 합니다. 그렇지 않으면 DBCC를 사용하여 문제를 해결할 수 있습니다. 경우에 따라 데이터베이스를 복원해야 할 수도 있습니다.|  
|24|미디어 오류를 나타냅니다. 시스템 관리자가 데이터베이스를 복원해야 할 수도 있습니다. 또는 하드웨어 공급업체에 문의해야 할 경우도 있습니다.|  
  
## <a name="user-defined-error-message-severity"></a>사용자 정의 오류 메시지 심각도  
 **sp_addmessage** 를 사용하여 심각도가 1부터 25까지의 사용자 정의 오류 메시지를 **sys.messages** 카탈로그 뷰에 추가할 수 있습니다. 이 사용자 정의 오류 메시지는 RAISERROR에서 사용될 수 있습니다. 자세한 내용은 [sp_addmessage&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)을 참조하세요.  
  
 RAISERROR는 심각도가 1부터 25까지의 사용자 정의 오류 메시지를 생성하는 데 사용될 수 있습니다. RAISERROR는 **sys.messages** 카탈로그 뷰에 저장된 사용자 정의 오류 메시지를 참조하거나 동적으로 메시지를 작성할 수 있습니다. 오류 발생 시 **sys.messages** 의 사용자 정의 오류 메시지를 사용하면 RAISERROR에서 지정한 심각도가 **sys.messages**에 지정된 심각도 대신 사용됩니다. 자세한 내용은 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)를 참조하세요.  
  
## <a name="error-severity-and-trycatch"></a>오류 심각도 및 TRY...CATCH  
 TRY...CATCH 구문은 데이터베이스 연결이 종료되지 않는 심각도가 10 이상인 모든 실행 오류를 catch합니다.  
  
 심각도가 0부터 10 사이인 오류는 정보 메시지이며 실행을 TRY...CATCH 구문의 CATCH 블록에서 점프하지 않습니다.  
  
 연결이 종료되면 실행이 중단되기 때문에 일반적으로 심각도가 20부터 25까지이며 데이터베이스 연결을 종료하는 오류는 CATCH 블록에서 처리되지 않습니다.  
  
 자세한 내용은 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)를 참조하세요.  
  
## <a name="retrieving-error-severity"></a>오류 심각도 검색  
 ERROR_SEVERITY 시스템 함수를 사용하여 TRY...CATCH 구문의 CATCH 블록 실행으로 이어지는 오류 심각도를 검색할 수 있습니다. CATCH 블록의 범위를 벗어나 호출한 경우 ERROR_SEVERITY는 NULL을 반환합니다. 자세한 내용은 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 오류 이해](../../relational-databases/errors-events/understanding-database-engine-errors.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
