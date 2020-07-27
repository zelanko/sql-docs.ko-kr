---
title: 복구 모델 오류 표시 안 함 - 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a59ff201edb153487640b4c5781d38a2df3756f9
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942228"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>복구 모델 오류 표시 안 함 서버 구성 옵션

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

SQL Server [복구 모델](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server)은 트랜잭션 로그 유지 관리를 제어합니다. 전체 복구 모델을 사용하면 데이터 파일의 손실 또는 손상으로 인해 어떠한 작업도 손실되지 않으며, 백업 보존 정책 내의 임의 시점으로의 복구가 지원됩니다. 전체 복구 모델은 SQL Managed Instance에서 지원되는 유일한 복구 모델이자 기본값입니다. SQL Managed Instance에서 복구 모델을 변경하려고 시도하면 오류 메시지가 반환됩니다.

**복구 모델 오류 표시 안 함** 고급 구성 옵션을 사용하여 SQL Managed Instance에서 실행되는 데이터베이스 복구 모델을 변경하는 명령이 오류와 경고 중 어느 것을 반환할지 지정할 수 있습니다. SQL Managed Instance에서 이 옵션을 1(ON)로 설정하면 ALTER DATABASE SET RECOVERY 명령을 실행해도 데이터베이스의 복구 모델이 변경되지 않지만 오류 대신 경고 메시지만 반환됩니다. SQL Managed Instance에서 이 옵션을 0(OFF)으로 설정하면 ALTER DATABASE SET RECOVERY 명령을 실행했을 때 오류 메시지가 반환됩니다.

**복구 모델 오류 표시 안 함** 옵션은 중요한 요구 사항이 나 필수 요구 사항은 아니지만, 레거시 또는 타사 애플리케이션이 복구 모델을 단순 모델 또는 대량 로깅 모델로 변경하려고 시도하는 경우에 유용합니다. 복구 모델 변경이 SQL Managed Instance의 사용을 저해하는 유일한 차단기인 경우, 복구 모델 오류 표시 안 함 구성 옵션을 설정하면 해당 차단기가 제거됩니다. 이 옵션은 애플리케이션 코드를 변경하는 대체 솔루션이 불가능하거나 경제적이지 않은 경우에 특히 유용합니다.

## <a name="examples"></a>예제

다음 예에서는 데이터베이스 복구 모델의 변경과 관련된 오류 메시지 표시 안 함을 사용하도록 설정하고 데이터베이스 복구 모델을 변경하는 명령을 실행한 결과 경고만 반환됩니다. 실제로는 복구 모델이 변경되지 않습니다. *my_database*를 실제 데이터베이스 이름으로 바꾸어야 합니다.

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>참고 항목

[서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
