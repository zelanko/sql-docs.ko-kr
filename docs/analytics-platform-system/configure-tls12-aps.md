---
title: TLS 1.2 구성
description: AP에서 TLS 1.2 구성 권장 사항
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 988cac765a596b541d128b0b6190f6f228d95ee7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401249"
---
# <a name="configure-tls-12-in-aps"></a>AP에서 TLS 1.2 구성

TLS 1.2만 사용 하도록 AP를 보호 하려면 모든 실제 및 가상 호스트에서 다른 프로토콜을 명시적으로 사용 하지 않도록 설정 해야 합니다. 프로토콜을 사용 하지 않도록 설정 하려면 레지스트리 설정을 변경 해야 합니다. 레지스트리를 변경 하려면 가상 및 실제 호스트를 다시 부팅 해야 합니다.

> [!WARNING]
> 이 섹션, 방법 또는 태스크에는 레지스트리를 수정하는 방법을 알려 주는 단계가 포함되어 있습니다. 그러나 레지스트리를 잘못 수정 하 여 데이터 손실을 야기 하 고 운영 체제를 다시 설치 해야 하는 경우 심각한 문제가 발생할 수 있습니다. 레지스트리를 수정 하기 전에 백업 하는 것이 좋습니다. 그런 다음 문제가 발생하면 레지스트리를 복원할 수 있습니다. 레지스트리를 백업 및 복원 하는 방법에 대 한 자세한 내용은 다음 문서 번호를 클릭 하 여 Microsoft 기술 자료 문서를 참조 하십시오.<br>
[322756](https://support.microsoft.com/help/322756) Windows에서 레지스트리를 백업 및 복원 하는 방법

**하지**
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

또한 AP SSIS 대상 어댑터와 같은 도구가 설치 된 클라이언트 컴퓨터에서 다음 키를 설정 합니다.
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



