---
title: catalog.create_environment_variable(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f7474200fa8156ab0663540611803276375ad6b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71281187"
---
# <a name="catalogcreate_environment_variable-ssisdb-database"></a>catalog.create_environment_variable(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 환경 변수를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>인수  
 [@folder_name =] *folder_name*  
 환경이 있는 폴더의 이름입니다. *folder_name*은 **nvarchar(128)** 입니다.  
  
 [@environment_name =] *environment_name*  
 환경의 이름입니다. *environment_name*은 **nvarchar(128)** 입니다.  
  
 [@variable_name =] *variable_name*  
 환경 변수의 이름입니다. *variable_name*은 **nvarchar(128)** 입니다.  
  
 [@data_type =] *data_type*  
 변수의 데이터 형식입니다. 지원되는 환경 변수 데이터 형식은 **Boolean**, **Byte**, **DateTime**, **Double**, **Int16**, **Int32**, **Int64**, **Single**, **String**, **UInt32** 및  **UInt64**입니다. 지원되지 않는 환경 변수 데이터 형식은 **Char**, **DBNull**, **Object** 및 **Sbyte**입니다. *data_type* 매개 변수의 데이터 형식은 **nvarchar(128)** 입니다.  
  
 [@sensitive =] *sensitive*  
 변수에 중요한 값이 포함되었는지 여부를 나타냅니다. 환경 변수 값이 중요함을 나타내려면 값 `1`을 사용하고, 그렇지 않음을 나타내려면 값 `0`을 사용합니다. 중요한 값은 저장될 때 암호화되고, 중요하지 않은 값은 일반 텍스트로 저장됩니다. *sensitive*는 **bit**입니다.  
  
 [@value =] *value*  
 환경 변수의 값입니다. *value*는 **sql_variant**입니다.  
  
 [@description =] *description*  
 환경 변수에 대한 설명입니다. *value*는 **nvarchar(1024)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   환경에 대한 READ 및 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   폴더 이름, 환경 이름 또는 환경 변수 이름이 잘못된 경우  
  
-   변수 이름이 환경에 이미 있는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
## <a name="remarks"></a>설명  
 환경 변수를 사용하면 패키지 실행 시 사용할 프로젝트 매개 변수나 패키지 매개 변수에 효율적으로 값을 할당할 수 있습니다. 환경 변수는 매개 변수 값이 구성을 활성화합니다. 변수 이름은 환경 내에서 고유해야 합니다.  
  
 이 저장 프로시저는 변수의 데이터 형식에 대한 유효성을 검사하여 해당 변수가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 지원되는지 확인합니다.  
  
> [!TIP]  
>  **에서는 지원되지 않는** Sbyte[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식 대신 **Int16** 데이터 형식을 사용하는 것이 좋습니다.  
  
 *value* 매개 변수를 사용하여 이 저장 프로시저에 전달된 값은 다음 표에 따라 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환됩니다.  
  
|Integration Services 데이터 형식|SQL Server 데이터 형식|  
|------------------------------------|--------------------------|  
|**Boolean**|**bit**|  
|**Byte**|**binary**, **varbinary**|  
|**DateTime**|**datetime**, **datetime2**, **datetimeoffset**, **smalldatetime**|  
|**Double**|정밀 숫자: **decimal**, **numeric**, 근사 숫자: **float**, **real**|  
|**Int16**|**smallint**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**단일**|정밀 숫자: **decimal**, **numeric**, 근사 숫자: **float**, **real**|  
|**String**|**varchar**, **nvarchar**, **char**|  
|**UInt32**|**int**(**int**는 **Uint32**에 사용할 수 있는 가장 가까운 매핑입니다.)|  
|**UInt64**|**bigint**(**int**는 **Uint64**에 사용할 수 있는 가장 가까운 매핑입니다.)|  
  
  
