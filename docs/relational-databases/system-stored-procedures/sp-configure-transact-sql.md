---
title: sp_configure (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 22d8f61af08f183e10910544e42614769b9dafd9
ms.sourcegitcommit: f6bfe4a0647ce7efebaca11d95412d6a9a92cd98
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974348"
---
# <a name="sp_configure-transact-sql"></a>sp_configure(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  현재 서버에 대한 전역 구성 설정을 표시하거나 변경합니다.

> [!NOTE]  
> 데이터베이스 수준 구성 옵션은 [ALTER DATABASE 범위 &#40;구성 transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조 하세요. 소프트 NUMA를 구성 하려면 [소프트 numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)를 참조 하세요.  
  
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
`[ @configname = ] 'option_name'`은 구성 옵션의 이름입니다. *option_name* 은 **varchar(35)** 이며 기본값은 NULL입니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 구성 이름의 일부인 고유 문자열을 모두 인식합니다. 이 인수를 지정하지 않으면 옵션의 전체 목록이 반환됩니다.  
  
 사용 가능한 구성 옵션 및 해당 설정에 대 한 자세한 내용은 [서버 구성 옵션 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)을 참조 하세요.  
  
`[ @configvalue = ] 'value'`은 새로운 구성 설정입니다. *value* 는 **int**이며 기본값은 NULL입니다. 최대값은 개별 옵션에 따라 달라집니다.  
  
 각 옵션에 대 한 최대값을 확인 하려면 **sys. 구성** 카탈로그 뷰의 **최 댓** 열을 참조 하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **Sp_configure** 는 매개 변수 없이 실행 될 때 다음 표와 같이 5 개의 열이 있는 결과 집합을 반환 하 고 옵션을 사전순으로 오름차순으로 정렬 합니다.  
  
 **Config_value** 및 **run_value** 의 값은 자동으로 동일 하지 않습니다. **Sp_configure**를 사용 하 여 구성 설정을 업데이트 한 후에는 다시 구성 또는 다시 설정 재정의를 사용 하 여 시스템 관리자가 실행 중인 구성 값을 업데이트 해야 합니다. 자세한 내용은 설명 섹션을 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|구성 옵션의 이름입니다.|  
|**minimum**|**int**|구성 옵션의 최소값입니다.|  
|**maximum**|**int**|구성 옵션의 최대값입니다.|  
|**config_value**|**int**|**Sp_configure** 를 사용 하 여 구성 옵션이 설정 된 값입니다 **(값.** 이러한 옵션에 대 한 자세한 내용은 [서버 구성 옵션 &#40;SQL Server&#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md) 및 [sys. 구성 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)을 참조 하세요.|  
|**run_value**|**int**|현재 실행 중인 구성 옵션 값 ( **value_in_use**의 값)입니다.<br /><br /> 자세한 내용은 [sys. 구성 &#40;&#41;transact-sql](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)을 참조 하세요.|  
  
## <a name="remarks"></a>설명  
 **Sp_configure** 를 사용 하 여 서버 수준 설정을 표시 하거나 변경 합니다. 데이터베이스 수준의 설정을 변경하려면 ALTER DATABASE를 사용합니다. 현재 사용자 세션에만 적용되는 설정을 변경하려면 SET 문을 사용합니다.  
  
## <a name="updating-the-running-configuration-value"></a>실행 중인 구성 값 업데이트  
 *옵션*에 새 *값* 을 지정 하면 결과 집합의 **config_value** 열에이 값이 표시 됩니다. 이 값은 처음에 현재 실행 중인 구성 값을 표시 하는 **run_value** 열의 값과 다릅니다. **Run_value** 열에서 실행 중인 구성 값을 업데이트 하려면 시스템 관리자가 RECONFIGURE 또는 RECONFIGURE WITH OVERRIDE를 실행 해야 합니다.  
  
 RECONFIGURE와 RECONFIGURE WITH OVERRIDE는 둘 다 모든 구성 옵션에 사용할 수 있습니다. 그러나 기본 RECONFIGURE 문은 적당한 범위 밖에 있는 옵션 값이나 옵션 간에 충돌을 일으킬 수 있는 옵션 값을 거부합니다. 예를 들어 **recovery interval** 값이 60 분 보다 크거나 **선호도 마스크** 값이 **affinity I/O MASK** 값과 겹치면 다시 구성에서 오류를 생성 합니다. 이와 달리 RECONFIGURE WITH OVERRIDE는 데이터 형식만 맞으면 모든 옵션 값을 허용하며 지정된 값으로 다시 구성합니다.  
  
> [!CAUTION]  
> 옵션 값을 잘못 설정하면 역으로 서버 인스턴스 구성에 영향을 줄 수 있습니다. RECONFIGURE WITH OVERRIDE는 매우 주의를 기울여 사용해야 합니다.  
  
 RECONFIGURE 문은 일부 옵션을 동적으로 업데이트합니다. 그 외의 옵션을 업데이트하려면 서버를 중지하고 다시 시작해야 합니다. 예를 들어 **min server memory** 및 **max server memory** 서버 메모리 옵션은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 동적으로 업데이트 됩니다. 따라서 서버를 다시 시작 하지 않고 변경할 수 있습니다. 반면 **채우기 비율** 옵션의 실행 값을 다시 구성 하려면-1 @no__t를 다시 시작 해야 합니다.  
  
 구성 옵션에서 RECONFIGURE를 실행 한 후 **sp_configure '***option_name***'** 를 실행 하 여 옵션이 동적으로 업데이트 되었는지 여부를 확인할 수 있습니다. **Run_value** 및 **config_value** 열의 값은 동적으로 업데이트 된 옵션에 대해 일치 해야 합니다. Is_dynamic 카탈로그 뷰의 열을 확인 하 여 동적으로 표시 되는 옵션을 확인할 수도 **있습니다.**  
 
 변경 내용은 SQL Server 오류 로그에도 기록 됩니다.
  
> [!NOTE]  
>  옵션에 대해 지정 된 *값* 이 너무 높으면 **run_value** 열에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]가 유효 하지 않은 설정을 사용 하는 것이 아니라 동적 메모리에 기본적으로 지정 되어 있다는 사실이 반영 됩니다.  
  
 자세한 내용은 [ &#40;&#41;transact-sql 다시 구성](../../t-sql/language-elements/reconfigure-transact-sql.md)을 참조 하세요.  
  
## <a name="advanced-options"></a>고급 옵션  
 **선호도 마스크** 및 **복구 간격과**같은 일부 구성 옵션은 고급 옵션으로 지정 됩니다. 기본적으로 이 옵션은 보거나 변경할 수 없습니다. 사용 가능 하도록 설정 하려면 **ShowAdvancedOptions** 구성 옵션을 1로 설정 합니다.  
  
 구성 옵션 및 해당 설정에 대 한 자세한 내용은 [서버 구성 옵션 &#40;&#41;SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md)을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경 하거나 RECONFIGURE 문을 실행 하는 두 매개 변수를 사용 하 여 **sp_configure** 를 실행 하려면 ALTER SETTINGS 서버 수준 사용 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. 고급 구성 옵션 나열  
 다음 예에서는 모든 구성 옵션을 설정하고 나열하는 방법을 보여 줍니다. 먼저 `show advanced option`을 `1`로 설정하면 고급 구성 옵션이 표시됩니다. 이 옵션을 변경한 다음 매개 변수 없이 `sp_configure`를 실행하면 모든 구성 옵션이 표시됩니다.  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 메시지는 다음과 같습니다. "구성 옵션 ' 고급 옵션 표시 '가 0에서 1로 변경 되었습니다. RECONFIGURE 문을 실행하여 설치하십시오."  
  
 `RECONFIGURE`를 실행하여 모든 구성 옵션을 표시합니다.  
  
```sql  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>2\. 구성 옵션 변경  
 다음 예에서는 시스템 `recovery interval`을 `3`분으로 설정합니다.  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>3\. 모든 사용 가능한 구성 설정 나열  
 다음 예에서는 모든 구성 옵션을 나열하는 방법을 보여 줍니다.  
  
```sql  
EXEC sp_configure;  
```  
  
 결과로 옵션 이름과 그 뒤에 해당 옵션에 대한 최소 및 최대값이 반환됩니다. **Config_value** 는 재구성이 완료 되 면 [!INCLUDE[ssDW](../../includes/ssdw-md.md)]에서 사용 하는 값입니다. **run_value** 는 현재 사용되는 값입니다. **config_value** 및 **run_value** 는 값이 변경 중이 아니라면 일반적으로 동일합니다.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>4\. 특정 구성 이름에 대한 구성 설정 나열  
  
```sql  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>5\. Hadoop 연결 설정  
 Hadoop 연결을 설정 하려면 sp_configure를 실행 하는 것 외에 몇 가지 추가 단계가 필요 합니다. 전체 절차는 [CREATE EXTERNAL DATA &#40;SOURCE transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
