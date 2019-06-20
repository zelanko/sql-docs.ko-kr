---
title: '분석 플랫폼 시스템에서 TLS 1.2를 구성 | Microsoft Docs '
description: AP에서 TLS 1.2를 구성 하는 권장 사항
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6ea2144fe333f87123abdf92e16aa7122e98b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63239462"
---
# <a name="configure-tls-12-in-aps"></a>AP에서 TLS 1.2를 구성 합니다.

TLS 1.2만 사용 하도록 AP를 보호 하려면 모든 실제 및 가상 호스트에서 다른 프로토콜을 명시적으로 사용 하지 않도록 설정 해야 합니다. 레지스트리 설정을 변경 해야 하는 프로토콜을 사용 하지 않도록 설정 합니다. 가상 및 실제 호스트를 다시 부팅을 해야 하는 레지스트리를 변경 합니다.

> [!WARNING]
> 이 섹션, 방법 또는 태스크에는 레지스트리를 수정하는 방법을 알려 주는 단계가 포함되어 있습니다. 그러나 잘못는 데이터가 손실 될 수 있습니다 및 운영 체제의 다시 설치 해야 레지스트리를 수정 하면 심각한 문제가 발생할 수 있습니다. 좋습니다 다시 레지스트리를 수정 하기 전에 합니다. 그런 다음 문제가 발생하면 레지스트리를 복원할 수 있습니다. 백업 하 고 레지스트리를 복원 하는 방법에 대 한 자세한 내용은 Microsoft 기술 자료 문서를 보려면 다음 문서 번호를 클릭 합니다.<br>
[322756](https://support.microsoft.com/help/322756) 를 백업 하 고 Windows에서 레지스트리를 복원 하는 방법

**사용 하지 않도록 설정 합니다.**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

또한 다음 키를 설정할 클라이언트 컴퓨터 AP SSIS 대상 어댑터와 같은 도구를 설치할.
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



