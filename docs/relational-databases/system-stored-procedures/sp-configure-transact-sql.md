---
title: sp_configure (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d6ff78066f307e70f37880eb57e2430774c242ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spconfigure-transact-sql"></a>sp_configure(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  현재 서버에 대한 전역 구성 설정을 표시하거나 변경합니다.  
  
> [!NOTE]  
>  데이터베이스 수준 구성 옵션에 대 한 참조 [ALTER DATABASE SCOPED configuration&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). 소프트 NUMA를 구성 하려면 참조 [소프트 NUMA &#40; SQL Server &#41; ](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ **@configname=** ] **'***option_name***'**  
 구성 옵션의 이름입니다. *option_name* 은 **varchar(35)**이며 기본값은 NULL입니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 구성 이름의 일부인 고유 문자열을 모두 인식합니다. 이 인수를 지정하지 않으면 옵션의 전체 목록이 반환됩니다.  
  
 사용 가능한 구성 옵션 및 해당 설정에 대 한 정보를 참조 하십시오. [서버 구성 옵션 &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 [ **@configvalue=** ] **'***value***'**  
 새로운 구성 설정입니다. *value* 는 **int**이며 기본값은 NULL입니다. 최대값은 개별 옵션에 따라 달라집니다.  
  
 각 옵션에 대 한 최대값을 보려면 참조는 **최대** 의 열은 **sys.configurations** 카탈로그 뷰.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 매개 변수 없이 실행 될 때 **sp_configure** 5 개의 열이 있는 결과 집합을 반환 하 고 다음 표와 같이 옵션이 알파벳 오름차순으로 정렬 합니다.  
  
 에 대 한 값 **config_value** 및 **run_value** 자동으로 같지 않습니다. 사용 하 여 구성 설정을 업데이트 한 후 **sp_configure**, 시스템 관리자가 reconfigure 또는 RECONFIGURE WITH OVERRIDE를 사용 하 여 실행 중인 구성 값을 업데이트 해야 합니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|구성 옵션의 이름입니다.|  
|**minimum**|**int**|구성 옵션의 최소값입니다.|  
|**maximum**|**int**|구성 옵션의 최대값입니다.|  
|**config_value**|**int**|에 구성 옵션 사용 하 여 설정 된 값 **sp_configure** (값 **sys.configurations.value**). 이러한 옵션에 대 한 자세한 내용은 참조 [서버 구성 옵션 &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md) 및 [sys.configurations&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
|**run_value**|**int**|현재 구성 옵션의 값을 실행 (값 **sys.configurations.value_in_use**).<br /><br /> 자세한 내용은 참조 [sys.configurations&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
  
## <a name="remarks"></a>주의  
 사용 하 여 **sp_configure** 를 표시 하거나 서버 수준의 설정을 변경 합니다. 데이터베이스 수준의 설정을 변경하려면 ALTER DATABASE를 사용합니다. 현재 사용자 세션에만 적용되는 설정을 변경하려면 SET 문을 사용합니다.  
  
## <a name="updating-the-running-configuration-value"></a>실행 중인 구성 값 업데이트  
 지정 하는 경우 새 *값* 에 대 한 프로그램 *옵션*, 결과 집합의이 값이 표시는 **config_value** 열입니다. 이 값이 처음에 값에서와 다른는 **run_value** 열을 현재 실행 중인 구성 값을 표시 합니다. 실행 중인 구성 값을 업데이트 하는 **run_value** 열 reconfigure 또는 RECONFIGURE WITH OVERRIDE 시스템 관리자를 실행 해야 합니다.  
  
 RECONFIGURE와 RECONFIGURE WITH OVERRIDE는 둘 다 모든 구성 옵션에 사용할 수 있습니다. 그러나 기본 RECONFIGURE 문은 적당한 범위 밖에 있는 옵션 값이나 옵션 간에 충돌을 일으킬 수 있는 옵션 값을 거부합니다. 경우 RECONFIGURE 오류를 생성 하는 예를 들어는 **복구 간격** 값이 60 분 보다 클 경우는 **선호도 마스크** 값과 겹치는 **선호도 I/O 마스크**값입니다. 이와 달리 RECONFIGURE WITH OVERRIDE는 데이터 형식만 맞으면 모든 옵션 값을 허용하며 지정된 값으로 다시 구성합니다.  
  
> [!CAUTION]  
>  옵션 값을 잘못 설정하면 역으로 서버 인스턴스 구성에 영향을 줄 수 있습니다. RECONFIGURE WITH OVERRIDE는 매우 주의를 기울여 사용해야 합니다.  
  
 RECONFIGURE 문은 일부 옵션을 동적으로 업데이트합니다. 그 외의 옵션을 업데이트하려면 서버를 중지하고 다시 시작해야 합니다. 예를 들어는 **최소 서버 메모리** 및 **최대 서버 메모리** 서버 메모리 옵션에서 동적으로 업데이트 되는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]; 따라서 서버를 다시 시작 하지 않고 변경할 수 있습니다. 반면, 실행 중인 값을 다시 구성는 **채우기 비율** 옵션을 사용 하려면 다시 시작은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다.  
  
 구성 옵션에서 RECONFIGURE를 실행 한 후 확인할 수 있습니다는 옵션을 실행 하 여 동적으로 업데이트 되었습니다 여부 **sp_configure'***option_name***'**합니다. 값은 **run_value** 및 **config_value** 동적으로 업데이트 되는 옵션에 대 한 열이 일치 해야 합니다. 어떤 옵션을 확인 하 여 동적 참조를 확인할 수 있습니다는 **is_dynamic** 의 열은 **sys.configurations** 카탈로그 뷰.  
  
> [!NOTE]  
>  지정 된 경우 *값* 는 옵션에 대해 너무 높기는 **run_value** 열 사실을 반영 하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 유효 하지 않은 설정을 사용 하지 않고 하지 못했습니다. 동적 메모리 합니다.  
  
 자세한 내용은 참조 [reconfigure&#40; Transact SQL &#41; ](../../t-sql/language-elements/reconfigure-transact-sql.md).  
  
## <a name="advanced-options"></a>고급 옵션  
 와 같은 일부 구성 옵션 **선호도 마스크** 및 **복구 간격**, 고급 옵션으로 지정 합니다. 기본적으로 이 옵션은 보거나 변경할 수 없습니다. 설정에서 사용할 수 있게,는 **ShowAdvancedOptions** 옵션을 1로 구성 합니다.  
  
 구성 옵션 및 해당 설정에 대 한 자세한 내용은 참조 [서버 구성 옵션 &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 실행할 **sp_configure** 구성 옵션을 변경 하거나 RECONFIGURE 문을 실행 하려면 두 매개 변수를 받아야 합니다 ALTER SETTINGS 서버 수준 사용 권한. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-the-advanced-configuration-options"></a>1. 고급 구성 옵션 나열  
 다음 예에서는 모든 구성 옵션을 설정하고 나열하는 방법을 보여 줍니다. 먼저 `show advanced option`을 `1`로 설정하면 고급 구성 옵션이 표시됩니다. 이 옵션을 변경한 다음 매개 변수 없이 `sp_configure`를 실행하면 모든 구성 옵션이 표시됩니다.  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 메시지는 다음과 같습니다: "구성 옵션을 1로 0에서 변경 'show advanced options'입니다. RECONFIGURE 문을 실행하여 설치하십시오."  
  
 `RECONFIGURE`를 실행하여 모든 구성 옵션을 표시합니다.  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>2. 구성 옵션 변경  
 다음 예에서는 시스템 `recovery interval`을 `3`분으로 설정합니다.  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>3. 모든 사용 가능한 구성 설정 나열  
 다음 예에서는 모든 구성 옵션을 나열하는 방법을 보여 줍니다.  
  
```  
EXEC sp_configure;  
```  
  
 결과로 옵션 이름과 그 뒤에 해당 옵션에 대한 최소 및 최대값이 반환됩니다. **config_value** 값인는 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 재구성이 완료 되 면 사용 됩니다. **run_value** 는 현재 사용되는 값입니다. **config_value** 및 **run_value** 는 값이 변경 중이 아니라면 일반적으로 동일합니다.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>4. 특정 구성 이름에 대한 구성 설정 나열  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>5. Hadoop 연결 설정  
 Hadoop 연결 설정 하려면 sp_configure를 실행 하는 것 외에도 몇 가지 추가 단계가 필요 합니다. 전체 프로시저에 대 한 참조 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
## <a name="see-also"></a>관련 항목:  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
