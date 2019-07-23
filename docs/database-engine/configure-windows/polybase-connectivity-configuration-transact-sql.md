---
title: PolyBase 연결 구성(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d86483245f8a4f06dfcb357d5d105539dd56f3a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997920"
---
# <a name="polybase-connectivity-configuration-transact-sql"></a>PolyBase 연결 구성(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  PolyBase Hadoop 및 Azure Blob 스토리지 연결을 위한 전역 구성 설정을 표시하거나 변경합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
--List all of the configuration options  
sp_configure  
[;]  
  
--Configure Hadoop connectivity  
sp_configure [ @configname = ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ **@configname=** ] **'** _option\_name_ **'**  
 구성 옵션의 이름입니다. *option_name* 은 **varchar(35)** 이며 기본값은 NULL입니다. 이 인수를 지정하지 않으면 옵션의 전체 목록이 반환됩니다.  
  
 [ **@configvalue=** ] **'** _value_ **'**  
 새로운 구성 설정입니다. *value* 는 **int**이며 기본값은 NULL입니다. 최대값은 개별 옵션에 따라 달라집니다.  
  
 **'hadoop connectivity'**  
 PolyBase에서 Hadoop 클러스터 또는 Azure Blob 스토리지(WASB)로의 모든 연결에 대한 Hadoop 데이터 원본 유형을 지정합니다. 이 설정은 외부 블레이드에 대한 외부 데이터 원본을 만드는 데 필요합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE(Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요.  
  
 다음은 Hadoop 연결 설정 및 지원되는 해당 Hadoop 데이터 원본입니다. 한 번에 하나의 설정만 적용할 수 있습니다. 옵션 1, 4 및 7은 서버의 모든 세션에서 여러 유형의 외부 데이터 원본을 만들고 사용할 수 있도록 허용합니다.  
  
-   옵션 0: Hadoop 연결 사용 안 함  
  
-   옵션 1: Windows Server의 Hortonworks HDP 1.3  
  
-   옵션 1: Azure Blob 스토리지(WASB[S])  
  
-   옵션 2: Linux의 Hortonworks HDP 1.3  
  
-   옵션 3: Linux에서 Cloudera CDH 4.3  
  
-   옵션 4: Windows Server의 Hortonworks HDP 2.0  
  
-   옵션 4: Azure Blob 스토리지(WASB[S])  
  
-   옵션 5: Linux의 Hortonworks HDP 2.0  
  
-   옵션 6: Linux의 Cloudera 5.1, 5.2, 5.3, 5.4, 5.5, 5.9, 5.10, 5.11, 5.12 및 5.13  
  
-   옵션 7: Linux의 Hortonworks 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 3.0  
  
-   옵션 7: Windows Server의 Hortonworks 2.1, 2.2 및 2.3  
  
-   옵션 7: Azure Blob 스토리지(WASB[S])  
  
 **RECONFIGURE**  
 구성 값(config_value)과 일치하도록 실행 값(run_value)을 업데이트합니다. run_value 및 config_value에 대한 정의는 [결과 집합](#ResultSets) 을 참조하세요. sp_configure로 설정된 새 구성 값은 RECONFIGURE 문으로 실행 값을 설정할 때까지 적용되지 않습니다.  
  
 RECONFIGURE를 실행한 후 SQL Server 서비스를 중지했다가 다시 시작해야 합니다. SQL Server 서비스를 중지할 때는 두 개의 추가 PolyBase 엔진 및 데이터 이동 서비스가 자동으로 중지됩니다. SQL Server 엔진 서비스를 다시 시작한 후 이 두 서비스를 다시 시작합니다(자동으로 시작되지 않음).  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
##  <a name="ResultSets"></a> 결과 집합  
 매개 변수 없이 실행한 경우 **sp_configure** 는 다섯 개의 열이 있는 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|구성 옵션의 이름입니다.|  
|**minimum**|**int**|구성 옵션의 최소값입니다.|  
|**maximum**|**int**|구성 옵션의 최대값입니다.|  
|**config_value**|**int**|**sp_configure**를 사용하여 설정된 값입니다.|  
|**run_value**|**int**|PolyBase에서 사용 중인 현재 값입니다. 이 값은 RECONFIGURE를 실행하여 설정합니다.<br /><br /> **config_value** 및 **run_value** 는 값이 변경 중이 아니라면 일반적으로 동일합니다.<br /><br /> 재구성이 진행 중인 경우 이 실행 값이 정확하기 위해서는 다시 시작해야 할 수 있습니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 RECONFIGURE를 실행한 후 'hadoop connectivity'의 실행 값을 적용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 다시 시작해야 합니다.  
[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 RECONFIGURE를 실행한 후 'hadoop connectivity'의 실행 값을 적용하려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 영역을 다시 시작해야 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 명시적 또는 암시적 트랜잭션에서는 RECONFIGURE가 허용되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자는 매개 변수 없이 또는 **매개 변수와 함께** sp_configure @configname 를 실행할 수 있습니다.  
  
 구성 값을 변경하거나 RECONFIGURE를 실행하려면 **sysadmin** 고정 서버 역할에 멤버 자격이나 **ALTER SETTINGS** 서버 수준 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-list-all-available-configuration-settings"></a>1\. 모든 사용 가능한 구성 설정 나열  
 다음 예에서는 모든 구성 옵션을 나열하는 방법을 보여 줍니다.  
  
```  
EXEC sp_configure;  
```  
  
 결과로 옵션 이름과 그 뒤에 해당 옵션에 대한 최소 및 최대값이 반환됩니다. **config_value** 는 재구성이 완료되면 SQL 또는 PolyBase에서 사용할 값입니다. **run_value** 는 현재 사용되는 값입니다. **config_value** 및 **run_value** 는 값이 변경 중이 아니라면 일반적으로 동일합니다.  
  
### <a name="b-list-the-configuration-settings-for-one-configuration-name"></a>2\. 특정 구성 이름에 대한 구성 설정 나열  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="c-set-hadoop-connectivity"></a>C. Hadoop 연결 설정  
 이 예에서는 PolyBase를 옵션 7로 설정합니다. 이 옵션을 사용하면 PolyBase가 Linux 및 Windows Server의 Hortonworks 2.1, 2.2, 2.3과 Azure Blob 스토리지에 외부 테이블을 만들고 사용할 수 있습니다. 예를 들어 SQL에서는 30개의 외부 테이블을 포함할 수 있습니다. 이 중 7개는 Linux의 Hortonworks 2.1에 있는 데이터를 참조하고 4개는 Linux의 Hortonworks 2.2를 참조하며 7개는 Linux의 Hortonworks 2.3을 참조하고 나머지 12개는 Azure Blob 스토리지를 참조합니다.  
  
```  
--Configure external tables to reference data on Hortonworks 2.1, 2.2, and 2.3 on Linux, and Azure blob storage  
  
sp_configure @configname = 'hadoop connectivity', @configvalue = 7;  
GO  
  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
