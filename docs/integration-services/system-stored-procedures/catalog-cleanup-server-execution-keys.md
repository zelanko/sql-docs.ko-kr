---
title: catalog.cleanup_server_execution_keys | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 172925d5a63aa831881b6a6325f0dbcbccd4dd56
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcleanupserverexecutionkeys"></a>catalog.cleanup_server_execution_keys
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SSISDB 데이터베이스에서 인증서와 대칭 키를 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>인수  
 [ @cleanup_flag =] *cleanup_flag*  
 실행 수준 (1) 또는 프로젝트 수준 (2) 인증서 삭제할 대칭 키가 있는지 여부를 나타냅니다.  
  
 여 SERVER_OPERATION_ENCRYPTION_LEVEL PER_EXECUTION (1)로 설정 된 경우에 실행 수준 (1)를 사용 합니다.  
  
 여 SERVER_OPERATION_ENCRYPTION_LEVEL PER_PROJECT (2)로 설정 된 경우에 프로젝트 수준 (2)를 사용 합니다. 인증서 및 대칭 키 삭제 및 작업 로그를 정리 된 프로젝트에만 삭제 됩니다.  
  
 [ @delete_batch_size =] *delete_batch_size*  
 삭제할 인증서 및 키의 수입니다. 기본값은 1000입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 성공 및 실패에 대 한 1 0입니다.  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   읽기 및 실행 권한이 프로젝트 및 해당 하는 경우 참조 된 환경에 대 한 읽기 권한.  
  
-   멤버 자격이 **ssis_admin** 데이터베이스 역할입니다.  
  
-   멤버 자격에는 **sysadmin** 서버 역할입니다.  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 이 저장된 프로시저는 다음과 같은 시나리오에서 오류를 발생 시킵니다.  
  
-   SSISDB 데이터베이스에서 하나 이상의 활성 작업이 있습니다.  
  
-   SSISDB 데이터베이스를 단일 사용자 모드에 없습니다.  
  
## <a name="remarks"></a>주의  
 SQL Server 2012 서비스 팩 2 추가 하 여 SERVER_OPERATION_ENCRYPTION_LEVEL 속성은 **internal.catalog_properties** 테이블입니다. 이 속성에는 두 개의 가능한 값:  
  
-   **(1) PER_EXECUTION** – 중요 한 실행 매개 변수를 보호 하는 데 사용 되는 인증서와 대칭 키 및 실행 로그는 각 실행에 대해 생성 됩니다. 이 값은 기본값입니다. 각 실행에 대해 인증서/키 생성 되기 때문에 프로덕션 환경에서 성능 문제 (교착 상태, 실패 한 유지 관리 작업 등)에 발생할 수 있습니다. 그러나이 설정을 (2) 다른 값 보다 더 높은 수준의 보안을 제공합니다.  
  
-   **(2) PER_PROJECT** – 각 프로젝트에 대 한 인증서와 중요 한 매개 변수를 보호 하는 데 사용 되는 대칭 키 생성 됩니다. 이렇게 하면 PER_EXECUTION 수준 보다 더 나은 성능을 키와 인증서 생성 되기 때문에 한 번이 아니라 각 실행에 대 한 프로젝트입니다.  
  
 실행 해야는 [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) 2-1 (또는) 1에서 2는 여 SERVER_OPERATION_ENCRYPTION_LEVEL를 변경 하려면 먼저 저장 프로시저입니다. 이 명령을 실행 하는 저장 프로시저를 하기 전에 다음을 수행 합니다.  
  
1.  OPERATION_CLEANUP_ENABLED 속성의 값을 TRUE로 설정 되어 있는지 확인은 [catalog.catalog_properties &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 테이블입니다.  
  
2.  Integration Services 데이터베이스 (SSISDB) 단일 사용자 모드를 설정 합니다. SQL Server Management Studio에서 SSISDB에 대 한 데이터베이스 속성 대화 상자를 시작, 옵션 탭으로 전환 하 고 단일 사용자 모드 (SINGLE_USER)로 액세스 제한 속성을 설정 합니다. 저장된 프로시저는 cleanup_server_log 실행 한 후 속성 값을 원래 값으로 다시 설정 합니다.  
  
3.  저장된 프로시저 실행 [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md)합니다.  
  
4.  이제 계속 진행 하 고 여 SERVER_OPERATION_ENCRYPTION_LEVEL 속성에 값을 변경는 [catalog.catalog_properties &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 테이블입니다.  
  
5.  저장된 프로시저 실행 [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) SSISDB 데이터베이스에서 인증서 키를 정리할 수 있습니다. SSISDB 데이터베이스에서 인증서 및 키를 삭제 하면 사용량이 적은 시간 동안 정기적으로 실행 해야 하므로 시간이 오래 걸릴 수 있습니다.  
  
     범위 또는 수준 (프로젝트 및 실행)와 삭제할 키의 수를 지정할 수 있습니다. 삭제에 대 한 기본 일괄 처리 크기는 1000입니다. 수준을 2로 설정한 경우 키 및 인증서는 관련 된 프로젝트를 삭제 하는 경우에 삭제 됩니다.  
  
 자세한 내용은 다음 기술 자료 문서를 참조 합니다. [FIX: SQL Server 2012에 저장 된 배포도 SSISDB를 사용할 때의 성능 문제](http://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>예제  
 다음 예제에서는 cleanup_server_execution_keys 저장 프로시저를 호출 합니다.  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
  
EXEC@return_value = [internal].[cleanup_server_execution_keys]  
@cleanup_flag = 1,  
@delete_batch_size = 500  
  
SELECT'Return Value' = @return_value  
  
GO  
```  
  
  

