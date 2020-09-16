---
title: sqlservr 애플리케이션
description: sqlservr 애플리케이션은 명령 프롬프트에서 SQL Server 인스턴스를 시작, 중지, 일시 중지 및 계속합니다.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 36fde81f6317d45b2169282d99e4eef27b3467b3
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714271"
---
# <a name="sqlservr-application"></a>sqlservr 애플리케이션

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

**sqlservr** 애플리케이션은 명령 프롬프트에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 시작, 중지, 일시 중지 및 계속합니다.

## <a name="syntax"></a>구문

```cmd
sqlservr [-s instance_name] [-c] [-d master_path] [-f] 
     [-e error_log_path] [-l master_log_path] [-m]
     [-n] [-T trace#] [-v] [-x]
```

## <a name="arguments"></a>인수

**-s** *instance_name* 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 인스턴스를 지정합니다. 명명된 인스턴스를 지정하지 않으면 **sqlservr** 이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기본 인스턴스를 시작합니다.

> [!IMPORTANT]
>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스를 시작할 때는 해당 인스턴스에 적합한 디렉터리에 있는 **sqlservr** 애플리케이션을 사용해야 합니다. 기본 인스턴스의 경우 \MSSQL\Binn 디렉터리에서 **sqlservr** 을 실행합니다. 명명된 인스턴스의 경우 \MSSQL$ **instance_name** \Binn 디렉터리에서*sqlservr*을 실행합니다.

 **-c**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 Windows 서비스 제어 관리자와 별개로 시작됨을 나타냅니다. 이 옵션을 사용하면 명령 프롬프트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 시작하기 때문에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 시작하는 데 걸리는 시간을 줄일 수 있습니다.

> [!NOTE]
>이 옵션을 사용하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 관리자 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] net stop **명령을 사용하여** 를 중지할 수 없으며 컴퓨터에서 로그오프하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 중지됩니다.

**-d** *master_path* **master** 데이터베이스 파일의 정규화된 경로를 나타냅니다. **-d** 와 *master_path*사이에 공백이 없어야 합니다. 이 옵션이 제공되지 않으면 기존의 레지스트리 매개 변수를 사용합니다.

**-f**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 최소 구성으로 시작합니다. 예를 들어 오버 커밋 메모리 같은 구성 값의 설정 때문에 서버를 시작할 수 없을 경우에 유용합니다.

**-e** *error_log_path* 오류 로그 파일의 정규화된 경로를 나타냅니다. 지정되지 않은 경우 기본 위치는 기본 인스턴스에 대해 `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL\Log\Errorlog`, 명명된 인스턴스에 대해 `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL$*instance_name*\Log\Errorlog`입니다. **-e** 와 *error_log_path*사이에 공백이 없어야 합니다.

**-l** *master_log_path* **master** 데이터베이스 트랜잭션 로그 파일의 정규화된 경로를 나타냅니다. **-l** 와 *master_log_path*사이에 공백이 없어야 합니다.

**-m**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 단일 사용자 모드로 시작합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 단일 사용자 모드로 시작하면 한 사용자만 연결할 수 있습니다. 디스크 캐시에 있는 완료된 트랜잭션이 정기적으로 데이터베이스 디바이스에 기록되도록 하는 CHECKPOINT 메커니즘이 시작되지 않았습니다. 대개 시스템 데이터베이스에 문제가 있어서 복구해야 하는 경우 이 옵션을 사용합니다. **sp_configure allow updates** 옵션을 설정합니다. 기본적으로 **allow updates** 는 사용할 수 없습니다.

**-n** 명명된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 시작할 수 있습니다. **-s** 매개 변수를 설정하지 않으면 기본 인스턴스가 시작됩니다. **sqlservr.exe**를 시작하기 전에 명령 프롬프트에서 해당 인스턴스에 적합한 BINN 디렉터리로 전환해야 합니다. 예를 들어 Instance1이 이진 파일에 대해 \mssql$Instance1을 사용할 경우, 사용자는 \mssql$Instance1\binn 디렉터리에서 **sqlservr.exe -s instance1**을 시작해야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -n **옵션으로** 인스턴스를 시작하는 경우에는 **-e** 옵션을 함께 사용하는 것이 좋습니다. 이렇게 하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이벤트가 기록되지 않습니다.

**-T** *trace#* 지정된 추적 플래그(*trace#* ) 적용 시 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 시작해야 함을 나타냅니다. 추적 플래그는 비표준 동작으로 서버를 시작하는 데 사용합니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.

>[!IMPORTANT]
>추적 플래그를 지정할 때는 **-T** 를 사용하여 추적 플래그 번호를 전달합니다. **에서 소문자 t(** -t [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])를 사용할 수는 있습니다. 그러나 **-t** 는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 지원 엔지니어에게 필요한 다른 내부 추적 플래그를 설정합니다.

**-v** 서버 버전 번호를 표시합니다.

**-x** CPU 시간과 캐시 적중률 통계를 유지할 수 없도록 합니다. 최고의 성능을 허용합니다.

## <a name="remarks"></a>설명
대부분의 경우 sqlserver.exe 프로그램은 문제 해결이나 주요 유지 관리 작업에만 사용됩니다. sqlservr.exe를 사용하여 명령 프롬프트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 시작할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 서비스로 실행되지 않으므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] net **명령을 사용하여** 를 중지할 수 없습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결할 수 있지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구에서 서비스 상태를 표시하므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 서비스가 중지되었음을 올바르게 나타냅니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 서버에 연결할 수 있지만 마찬가지로 서비스가 중지되었음을 나타냅니다.

## <a name="compatibility-support"></a>호환성 지원
다음 매개 변수는 사용되지 않으며 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 지원되지 않습니다.

|매개 변수 | 자세한 정보|
|:-----|:-----|
|**-h** | 이전 버전 32비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 AWE가 설정된 경우 Hot Add 메모리 메타데이터에 대해 가상 주소 공간을 예약하는 데 사용됩니다. [!INCLUDE[sssql14](../includes/sssql14-md.md)]을 통해 지원됩니다. 자세한 내용은 [SQL Server 2016에서 지원되지 않는 SQL Server 기능](../database-engine/discontinued-database-engine-functionality-in-sql-server.md?view=sql-server-ver15)을 참조하세요.|
|**-g** | *memory_to_reserve*<br/><br>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 32비트 인스턴스 이전 버전에 적용됩니다. [!INCLUDE[sssql14](../includes/sssql14-md.md)]을 통해 지원됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로세스 내, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 메모리 풀 외부의 메모리 할당에 사용할 수 있도록 남겨 두는 메모리 양(MB)을 정수로 지정합니다. 자세한 내용은 [서버 메모리 구성 옵션에 관한 SQL Server 2014 설명서](/previous-versions/sql/2014/database-engine/configure-windows/server-memory-server-configuration-options?view=sql-server-2014)를 참고하세요.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>참고 항목
 [데이터베이스 엔진 서비스 시작 옵션](../database-engine/configure-windows/database-engine-service-startup-options.md)