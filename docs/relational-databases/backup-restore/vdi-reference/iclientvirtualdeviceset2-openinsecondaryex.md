---
title: IClientVirtualDeviceSet2::OpenInSecondaryEx
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::OpenInSecondaryEx 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cd89359ecbcc920fe03ed4b2bc7d90fd01592476
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847564"
---
# <a name="iclientvirtualdeviceset2openinsecondaryex-vdi"></a>IClientVirtualDeviceSet2::OpenInSecondaryEx (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**OpenInSecondaryEx** 함수는 보조 클라이언트에서 가상 디바이스 세트를 엽니다. 기본 클라이언트는 이미 CreateEx 및 GetConfiguration을 사용하여 가상 디바이스 세트를 설정했어야 합니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::OpenInSecondaryEx (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpSetName
);
```

## <a name="parameters"></a>매개 변수

*lpInstanceName* 이 문자열은 SQL 명령이 전송될 SQL Server 인스턴스를 식별합니다.

*lpSetName* 세트를 식별합니다. 이 이름은 대/소문자를 구분하며 IClientVirtualDeviceSet2::Create를 호출할 때 기본 클라이언트에서 사용하는 이름과 일치해야 합니다.

## <a name="return-value"></a>반환 값

|반환 값 | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_PROTOCOL | 가상 디바이스 세트가 열려 있거나 가상 디바이스 세트가 보조 클라이언트의 열기 요청을 수락할 준비가 되지 않았습니다. |
| VD_E_ABORT | 작업이 중단되고 있습니다. |

## <a name="remarks"></a>Remarks

다중 프로세스 모델을 사용하는 경우 기본 클라이언트는 보조 클라이언트의 정상적인 종료와 비정상적인 종료를 탐지해야 합니다.

인스턴스 이름은 T-SQL이 발급된 인스턴스를 식별해야 합니다. NULL은 기본 인스턴스를 식별합니다. "machineName\" 접두사는 허용되지 않습니다.

OpenInSecondaryEx는 원본 SQL Server 버전 7.0 인터페이스에 정의된 원본 IClientVirtualDeviceSet::OpenInSecondary를 대체합니다. 새 개발에서는 OpenInSecondaryEx를 사용해야 합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.