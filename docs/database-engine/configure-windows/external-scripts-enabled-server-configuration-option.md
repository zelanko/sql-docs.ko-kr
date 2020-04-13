---
title: External Scripts Enabled 서버 구성 옵션 | Microsoft Docs
ms.date: 11/13/2017
ms.prod: sql
ms.technology: configuration
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 14e3d788034fad9e26f8283e5155d29286ad7360
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664298"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>External Scripts Enabled 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 및 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

**external scripts enabled** 옵션을 사용하면 특정 원격 언어 확장을 사용하여 스크립트를 실행하도록 설정할 수 있습니다. 이 속성은 기본적으로 해제되어 있습니다. **고급 분석 서비스**가 설치되어 있으면 이 속성을 true로 설정할 수 있습니다.

## <a name="remarks"></a>설명

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 프로시저를 사용하여 외부 스크립트를 실행하려면 외부 스크립트 사용 옵션을 사용하도록 설정해야 합니다. **sp_execute_external_script**를 사용하여 R 또는 Python과 같이 지원되는 언어로 작성된 스크립트를 실행합니다. 

+ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 R 언어와 R 워크스테이션 도구 및 연결 라이브러리 집합에 대한 지원이 포함됩니다.

    R 스크립트를 실행할 수 있도록 설정하려면 **설치 중에** 고급 분석 확장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치합니다. R 언어는 기본적으로 설치되어 있습니다.

+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]의 경우

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]는 SQL Server 2016에서와 동일한 아키텍처를 사용하지만, Python 언어에 대한 지원을 제공합니다.

    외부 스크립트를 실행할 수 있도록 설정하려면 **설치 중에**고급 분석 확장[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치합니다. 초기 설치 과정에서 R 또는 Python 중 하나, 또는 둘다를 선택하도록 합니다. 

## <a name="additional-requirements"></a>추가 요구 사항

설치 후에 외부 스크립트를 사용하려면 다음 스크립트를 실행합니다.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

이 변경 내용을 적용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.

자세한 내용은 [SQL Server Machine Learning 설정](../../machine-learning/install/sql-machine-learning-services-windows-install.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)

[sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

[SQL Server Machine Learning 서비스](../../machine-learning/index.yml)
