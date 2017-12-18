---
title: catalog.cleanup_server_log | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0dedb685-d3a6-4bd6-8afd-58d98853deee
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6cf0f550930ac73199276dc403763f49ce45b5e7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="catalogcleanupserverlog"></a>catalog.cleanup_server_log
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  작업 로그를 정리하여 SERVER_OPERATION_ENCRYPTION_LEVEL 속성 값을 변경할 수 있는 상태로 SSISDB 데이터베이스를 전환합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.cleanup_server_log  
```  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 성공은 0, 실패는 1입니다.  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 EXECUTE 권한과 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할의 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 이 저장 프로시저는 다음 시나리오에서 오류를 발생시킵니다.  
  
-   SSISDB 데이터베이스에 활성 작업이 하나 이상 있습니다.  
  
-   SSISDB 데이터베이스가 단일 사용자 모드가 아닙니다.  
  
## <a name="remarks"></a>주의  
 SQL Server 2012 서비스 팩 2에는 SERVER_OPERATION_ENCRYPTION_LEVEL 속성이 **internal.catalog_properties** 테이블에 추가되었습니다. 이 속성에는 두 가지 가능한 값이 있습니다.  
  
-   **PER_EXECUTION (1)** – 중요한 실행 매개 변수 및 실행 로그를 보호하는 데 사용되는 인증서 및 대칭 키는 각 실행에 대해 만들어집니다. 각 실행에 대해 인증서/키가 생성되기 때문에 프로덕션 환경에서 성능 문제(교착 상태, 유지 관리 작업 실패 등)가 발생할 수 있습니다. 하지만 이 설정은 다른 값(2)보다 높은 수준의 보안을 제공합니다.  
  
-   **PER_PROJECT (2)** – 중요한 매개 변수를 보호하는 데 사용되는 인증서 및 대칭 키가 각 프로젝트에 대해 만들어집니다. PER_PROJECT (2)가 기본값입니다. 이 설정은 키와 인증서가 각 실행에 대해서 생성되지 않고 프로젝트에 대해 한 번 생성되기 때문에 PER_EXECUTION 수준보다 높은 성능을 제공합니다.  
  
 SERVER_OPERATION_ENCRYPTION_LEVE를 2에서 1로 또는 1에서 2로 변경하려면 [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) 저장 프로시저를 실행해야 합니다. 저장 프로시저를 실행하기 전에 다음을 수행해야 합니다.  
  
1.  [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 테이블에 OPERATION_CLEANUP_ENABLED 속성의 값이 TRUE로 설정되어 있는지 확인합니다.  
  
2.  Integration Services 데이터베이스(SSISDB)를 단일 사용자 모드로 설정합니다. SQL Server Management Studio에서 SSISDB의 데이터베이스 속성 대화 상자를 시작하여 옵션 탭으로 전환하고 액세스 제한 속성을 단일 사용자 모드(SINGLE_USER)로 설정합니다. cleanup_server_log 저장 프로시저를 실행한 후에 속성 값을 다시 원래 값으로 설정합니다.  
  
3.  저장 프로시저 [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)를 실행합니다.  
  
4.  계속해서 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 테이블에서 SERVER_OPERATION_ENCRYPTION_LEVEL 속성 값을 변경합니다.  
  
5.  [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) 저장 프로시저를 실행하여 SSISDB 데이터베이스에서 인증서 키를 정리합니다. SSISDB 데이터베이스에서 인증서와 키를 삭제하는 데 시간이 오래 걸릴 수 있으므로 사용량이 적은 시간에 주기적으로 실행해야 합니다.  
  
     범위 또는 수준(실행 및 프로젝트) 및 삭제할 키 수를 지정할 수 있습니다. 삭제할 기본 일괄 처리 크기는 1000입니다. 수준을 2로 설정하면 연결된 프로젝트가 삭제된 경우에만 키와 인증서가 삭제됩니다.  
  
 자세한 내용은 [수정: SQL Server 2012에서 SSISDB를 배포 저장소로 사용하는 경우 성능 문제](http://support.microsoft.com/kb/2972285)에서 다음 기술 문서를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제는 cleanup_server_log 저장 프로시저를 호출합니다.  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
EXEC@return_value = [internal].[cleanup_server_log]  
SELECT'Return Value' = @return_value  
GO   
```  
  
  
