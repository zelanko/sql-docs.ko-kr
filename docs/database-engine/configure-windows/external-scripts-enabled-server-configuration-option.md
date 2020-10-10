---
title: External Scripts Enabled 서버 구성 옵션
description: SQL Server의 외부 스크립트 사용 옵션에 대해 알아봅니다. 이 옵션을 설정하면 R 또는 Python과 같은 지원되는 언어로 외부 스크립트를 실행할 수 있습니다.
ms.date: 06/30/2020
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ec430a256e07cfee21a14bbe3fe97426b044b4fd
ms.sourcegitcommit: 71d2389cf27156fa0404a6e6f65fb7a61c40789a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91636133"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>External Scripts Enabled 서버 구성 옵션
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**external scripts enabled** 옵션을 사용하면 특정 원격 언어 확장을 사용하여 스크립트를 실행하도록 설정할 수 있습니다. 이 속성은 기본적으로 해제되어 있습니다. **Machine Learning Services**가 설치되어 있으면 설치 프로그램이 필요에 따라 이 속성을 true로 설정할 수 있습니다.

## <a name="remarks"></a>설명

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 프로시저를 사용하여 외부 스크립트를 실행하려면 외부 스크립트 사용 옵션을 사용하도록 설정해야 합니다. **sp_execute_external_script**를 사용하여 R 또는 Python과 같이 지원되는 언어로 작성된 스크립트를 실행합니다. 

+ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 R 언어와 R 워크스테이션 도구 및 연결 라이브러리 집합에 대한 지원이 포함됩니다.

    R 스크립트를 실행할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 동안 **R Services** 기능을 설치합니다.

+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] 이상

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]는 R 및 Python 언어를 모두 지원합니다.

    외부 스크립트를 실행할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 동안 **Machine Learning Services** 기능을 설치합니다. 초기 설치 과정에서 R 또는 Python 중 하나, 또는 둘다를 선택하도록 합니다.
    
+ [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)] 이상 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]의 경우 모든 R, Python, Java 및 기타 타사 언어를 지원합니다.

지원되는 모든 언어에 대해 외부 스크립트를 실행할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설정하는 동안 Machine Learning Services 및 언어 확장 기능을 설치합니다.

## <a name="additional-requirements"></a>추가 요구 사항

설치 후에 외부 스크립트를 사용하려면 다음 스크립트를 실행합니다.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

자세한 내용은 [Windows에서 SQL Server Machine Learning Services(Python 및 R) 설치](../../machine-learning/install/sql-machine-learning-services-windows-install.md) 또는 [Linux에서 SQL Server Machine Learning Services(Python 및 R) 설치](../../linux/sql-server-linux-setup-machine-learning-docker.md?toc=/sql/machine-learning/toc.json)를 참조하세요.

## <a name="see-also"></a>참고 항목

+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
+ [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
+ [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [SQL Machine Learning 설명서](../../machine-learning/index.yml)
